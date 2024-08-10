Fedora Post Install - Terminal
==============================

.. contents::
   :local:
   :depth: 50

Set Hostname
------------

Set your device's Hostname, Replace HOSTNAME with your hostname

.. code-block:: bash

    hostnamectl set-hostname HOSTNAME

RPM Fusion
----------

Install RPM Fustion Repository

.. code-block:: bash

    sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm

Update fedora

.. code-block:: bash

    sudo dnf -y update
    sudo dnf -y upgrade --refresh

    reboot

NVIDIA Drivers - If Applicable
------------------------------

.. warning::

    Ensure Secure Boot is disabled before proceeding

Install Drivers

.. code-block:: bash
    
    sudo dnf install akmod-nvidia

Install Additional Drivers for CUDA enabled software such as Davinci, Resolve, Blender, etc...

.. code-block:: bash

    sudo dnf install xorg-x11-drv-nvidia-cuda

.. note:: 

    Let the kernel get built. So take about 5 minutes after it's installed to do additional steps.

Media Codecs
------------

Install Media Codecs

.. code-block:: bash

    sudo dnf swap 'ffmpeg-free' 'ffmpeg' --allowerasing

    sudo dnf update @multimedia --setopt="install_weak_deps=False" --exclude=PackageKit-gstreamer-plugin

    sudo dnf update @sound-and-video

    sudo dnf install Multimedia

Network Manager Wait Online Service
-----------------------------------

Disable the ``NetworkManager-wait-online.service``

.. code-block:: bash

    sudo systemctl disable NetworkManager-wait-online.service

Gnome Software Startup
----------------------

Disable the Gnome software from your startup apps

.. code-block:: bash

    sudo rm /etc/xdg/autostart/org.gnome.Software.desktop

Reboot
------

Top it all off with a reboot

.. code-block:: bash

    reboot

Dun
