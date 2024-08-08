# Configuring DHCP and DNS Servers

Simple walk-through of configuring DHCP and DNS on the same server with Dynamic Updates for a local domain.
Assumptions: Local Linux Server such as CentOS or Fedora Server configured and updated.

## 1. Set Up DHCP Server
1.1 Install ISC DHCP Server
   
ISC has announced the end of maintenance for ISC DHCP as of the end of 2022. ISC will continue providing professional support services for existing subscribers, but does not intend to issue any further maintenance releases. Please see Kea Documentation for ISC's replacement.

### To install the DHCP server package, run:
`sudo dnf install dhcp-server`

### Start and enable the DHCP server service:
`sudo systemctl start dhcpd`

`sudo systemctl enable dhcpd`

## 1.2 Configure `dhcpd.conf`

### Edit the DHCP configuration file:
`sudo nano /etc/dhcp/dhcpd.conf`

### Add the following configuration:
```
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
}```
