Install Fedora 40
==================

Official Documentation

https://docs.fedoraproject.org/en-US/workstation-docs/

This guide is compiled information from fedoraproject and other sources.

.. attention::

    **System Requirements:**

    - 40GB SSD disk
    - 4GB RAM

Download Fedora Workstation
===========================

Go to https://fedoraproject.org/en/workstation/download

From here, you can download the Media Writer or download an ISO for installation.
For this guide, we will be focusing on Fedora Media Writer.

Please choose the Fedora Media Writer for whichever system you are using.

Run Fedora Media Writer
-----------------------

Run Fedora Media Writer and select the image source.

.. image:: /image/fmr_mediawriter.png
   :align: center
   :scale: 100%

We will be downloading it automatically.

Select Your Release
--------------------

Unlike Windows, there are many releases. You can do some research on these at https://fedoraproject.org/spins/

Personally, I use Fedora KDE Plasma Desktop. But for this guide, we will be working with the official release of Fedora Workstation.

.. image:: /image/fmr_mediawriter_release.png
   :align: center
   :scale: 100%

Version Selection
-----------------

Select Version 40.

Choose your hardware architecture. This will most likely be Intel/AMD 64-bit.

Select the USB drive.

Under Download, check "Delete download after writing."

Click "Download & Write."

Install Fedora Workstation 40
=============================

Select ``Start Fedora-Workstation 40``.

.. image:: /image/fedora_boot.png
   :align: center
   :scale: 50%

You are now on the Fedora Workstation Desktop Environment! That was EASY!! You can choose to play around in this environment. It's very lightweight and can give you a ground-level feel for it.

Select Install Fedora
----------------------

.. image:: /image/fedora_install.png
   :align: center
   :scale: 25%

Select your language and click Next/Continue.

.. image:: /image/fedora_summary.png
   :align: center
   :scale: 25%

Change your Time & Date if needed.

Select the hard drive that you want to install on.

.. image:: /image/fedora_destination.png
   :align: center
   :scale: 25%

You will notice a checkmark on the drive that you want to install on. If it's not checked, click it so it is.

Storage Configuration
---------------------

For this guide, we will not be talking about RAID configuration. So for now, click "Automatic."

Encryption
----------

You can choose to encrypt your drive... or not.

.. note:: 

    Encrypting your data will require setting a password that will be entered after the boot process and before reaching the OS.

Click "Done" at the top left.

You will be brought back to the installation summary.

Select "Begin Installation."

This will start the installation.

Once complete, click "Finish Installation."

.. image:: /image/fedora_complete.png
   :align: center
   :scale: 25%

Once complete, unplug your USB from your device and give it a restart.

.. image:: /image/fedora_restart.png
   :align: center
   :scale: 25%
