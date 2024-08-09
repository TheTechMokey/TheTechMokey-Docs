Configuring DHCP and DNS Servers
================================

Simple walk-through of configuring DHCP and DNS on the same server with Dynamic Updates for a local domain.

!!! admonition "Assumptions"

.. note::
    Assumptions: Local Linux Server such as CentOS or Fedora Server configured and updated.

1. Set Up DHCP Server
---------------------

1.1 Install ISC DHCP Server
~~~~~~~~~~~~~~~~~~~~~~~~~~~

!!! attention

ISC has announced the end of maintenance for ISC DHCP as of the end of 2022. ISC will continue providing professional support services for existing subscribers, but does not intend to issue any further maintenance releases. Please see Kea Documentation for ISC's replacement.

To install the DHCP server package, run::

    sudo dnf install dhcp-server

Start and enable the DHCP server service::

    sudo systemctl start dhcpd

    sudo systemctl enable dhcpd

1.2 Configure `dhcpd.conf`
~~~~~~~~~~~~~~~~~~~~~~~~~~

Edit the DHCP configuration file::

    sudo nano /etc/dhcp/dhcpd.conf

Add the following configuration::

    # Use the interim DDNS update style
    ddns-update-style interim;

    # Ignore client updates; the server will handle updates itself
    ignore client-updates;

    # Define the key for authentication with the DNS server
    key “rndc-key” {
        algorithm hmac-md5;
        secret “your-rndc-key-secret”;  # Replace with your actual key secret
    };

    # Configure DNS zones for dynamic updates
    zone YOURDOMAINNAME.lan. {
        primary 192.168.1.254;  # IP address of the DNS server
        key “rndc-key”;
    }

    zone 1.168.192.in-addr.arpa. {
        primary 192.168.1.254;  # IP address of the DNS server
        key “rndc-key”;
    }

    # Define default and maximum lease times
    default-lease-time 600;
    max-lease-time 7200;

    # Specify the domain name and DNS servers for DHCP clients
    option domain-name “YOURDOMAINNAME.lan”;
    option domain-name-servers 192.168.1.254;  # IP address of the DNS server

    # Define a subnet configuration
    subnet 192.168.1.0 netmask 255.255.255.0 {
        range 192.168.1.100 192.168.1.200;  # Range of IP addresses to assign
        option routers 192.168.1.1;  # Default gateway
        option domain-name-servers 192.168.1.254;  # DNS server IP
        option domain-name “YOURDOMAINNAME.lan”;  # Domain name for the subnet
        ddns-domainname “YOURDOMAINNAME.lan”;
        ddns-rev-domainname “in-addr.arpa”;
    }

    # Example of a static IP assignment
    host example-host {
        hardware ethernet 00:1A:2B:3C:4D:5E;  # MAC address of the client
        fixed-address 192.168.1.50;  # Fixed IP address
    }

Save and close the file.

Restart the DHCP server to apply changes::

    sudo systemctl restart dhcpd

1.3 Generate or Configure DNS Update Key
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Generate a key using OpenSSL (if not already done)::

    openssl rand -base64 32

Create or edit the key file::

    sudo nano /etc/dhcp/rndc.key

Add the following content, replacing the key secret::

    key “rndc-key” {
        algorithm hmac-md5;
        secret “your-generated-key”;
    }

Ensure correct permissions::

    sudo chown dhcp:dhcp /etc/dhcp/rndc.key
    sudo chmod 600 /etc/dhcp/rndc.key

2. Set Up DNS Server (BIND)
---------------------------

2.1 Install BIND DNS Server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Install BIND server package::

    sudo dnf install bind bind-utils

Start and enable the BIND service::

    sudo systemctl start named
    sudo systemctl enable named

2.2 Configure BIND
~~~~~~~~~~~~~~~~~~

Edit the BIND configuration file::

    sudo nano /etc/named.conf

Add the following configuration::

    options {
        listen-on port 53 { 192.168.1.254; };  # IP address of the DNS server
        listen-on-v6 { none; };  # Disable IPv6
        directory "/var/named";  # Directory for zone files
        dump-file "/var/named/data/cache_dump.db";  # Cache dump file
        statistics-file "/var/named/data/named_stats.txt";  # Statistics file
        memstatistics-file "/var/named/data/named_mem_stats.txt";  # Memory stats file
        allow-query { any; };  # Allow queries from any IP address
        recursion yes;  # Enable recursion
        forwarders {
            8.8.8.8;  # Google Public DNS
            8.8.4.4;  # Google Public DNS
            # Add other external DNS servers here
        };
        dnssec-enable yes;  # Enable DNSSEC
        dnssec-validation auto;  # Enable automatic DNSSEC validation
        auth-nxdomain no;  # Suppress authoritative NXDOMAIN responses
        listen-on-v6 { any; };  # Enable listening on IPv6
    };

# Include the key for DNS updates
include "/etc/named.rfc1912.zones";
include "/etc/named.default-zones";

Create or edit the zone files:

**Forward Zone File**::

    sudo nano /var/named/YOURDOMAINNAME.lan.db

Add the following configuration::

    $TTL 86400
    @   IN  SOA ns1.YOURDOMAINNAME.lan. admin.YOURDOMAINNAME.lan. (
                2024080501  ; Serial
                3600        ; Refresh
                1800        ; Retry
                1209600     ; Expire
                86400 )     ; Negative Cache TTL

    ; Name servers
    @   IN  NS  ns1.YOURDOMAINNAME.lan.

    ; A records for name servers
    ns1 IN  A   192.168.1.254

    ; A records for other hosts
    @   IN  A   192.168.1.254

**Reverse Zone File**::

    sudo nano /var/named/1.168.192.rev

Add the following configuration::

    $TTL 86400
    @   IN  SOA ns1.YOURDOMAINNAME.lan. admin.YOURDOMAINNAME.lan. (
                2024080501  ; Serial
                3600        ; Refresh
                1800        ; Retry
                1209600     ; Expire
                86400 )     ; Negative Cache TTL

    ; Name servers
    @   IN  NS  ns1.YOURDOMAINNAME.lan.

    ; PTR records
    254 IN  PTR  ns1.YOURDOMAINNAME.lan.

Update the `named.conf` file to include these zone files::

    zone "YOURDOMAINNAME.lan" IN {
        type master;
        file "/var/named/YOURDOMAINNAME.lan.db";
    };

    zone "1.168.192.in-addr.arpa" IN {
        type master;
        file "/var/named/1.168.192.rev";
    };

Restart the BIND service to apply changes::

    sudo systemctl restart named

Verify BIND is running and the configurations are correct::

    sudo systemctl status named

Test DNS resolution::

    dig @192.168.1.254 example.YOURDOMAINNAME.lan

3. Configure Webmin for GUI Management
--------------------------------------

3.1 Install Webmin
~~~~~~~~~~~~~~~~~~

Create a repository file for Webmin::

    sudo nano /etc/yum.repos.d/webmin.repo

Add the following content::

    [Webmin]
    name=Webmin Distribution
    baseurl=http://download.webmin.com/download/yum
    enabled=1
    gpgcheck=1
    gpgkey=http://www.webmin.com/jcameron-key.asc

Install Webmin::

    sudo dnf install webmin

Start and enable the Webmin service::

    sudo systemctl start webmin
    sudo systemctl enable webmin

Access Webmin via your web browser:

Open `https://192.168.1.254:10000` and log in with your root or administrative user credentials.

3.2 Configure Webmin for DHCP and DNS Management
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Log in to Webmin.
2. Navigate to the “Servers” section and select “BIND DNS Server” and “DHCP Server”.
3. Configure DHCP and DNS settings as needed through the Webmin interface.
