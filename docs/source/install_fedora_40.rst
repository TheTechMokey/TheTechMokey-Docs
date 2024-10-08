Install and Setup Fedora 40 Workstation
=======================================

.. contents::
   :local:
   :depth: 50

`Official Documentation <https://docs.fedoraproject.org/en-US/workstation-docs/>`_

This guide is compiled information from fedoraproject and other sources.

.. attention::

    **System Requirements:**
    
    - 40GB SSD disk
    - 4GB RAM

Download Fedora Workstation
---------------------------

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

Personally, I use `Fedora KDE Plasma Desktop <https://fedoraproject.org/spins/kde/>`_. But for this guide, we will be working with the official release of Fedora Workstation.

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
-----------------------------

Select ``Start Fedora-Workstation 40``.

.. image:: /image/fedora_boot.png
   :align: center
   :scale: 50%

You are now on the Fedora Workstation Desktop Environment! That was EASY!! You can choose to play around in this environment. It's very lightweight and can give you a ground-level feel for it.

Select Install Fedora

.. image:: /image/fedora_install.png
   :align: center
   :scale: 20%

Select your language and click Next/Continue.

.. image:: /image/fedora_summary.png
   :align: center
   :scale: 20%

Change your Time & Date if needed.

Select the hard drive that you want to install on.

.. image:: /image/fedora_destination.png
   :align: center
   :scale: 20%

You will notice a checkmark on the drive that you want to install on. If it's not checked, click it so it is.

Storage Configuration
---------------------

For this guide, we will not be talking about RAID configuration. So for now, click "Automatic."

Encryption

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
   :scale: 20%

Once complete, unplug your USB from your device and give it a restart.

.. image:: /image/fedora_restart.png
   :align: center
   :scale: 20%

Setup Fedora Workstation 40
--------------------------- 

Now we're ready to set up Fedora Workstation 40!

Click "Start Setup."

.. image:: /image/fedora_start.png
   :align: center
   :scale: 20%

Privacy is up to you. Remember that Linux is open-source, meaning everyone contributes to make an awesome experience.

Click "Next" after your selection.

You're going to want to enable Third Party Repositories for ease of use.

Click ``Enable Third-Party Repositories``

Click ``Next``.

The "About You" section is what you will log in with.

Put your name in, and then type in a username for this device.

.. image:: /image/fedora_about_you.png
   :align: center
   :scale: 20%

Click ``Next``.

Type in your password.

.. note:: 

    If you encrypted your hard drive, do not use the same password. It only makes sense.

All Done

Select ``Start Using Fedora``.

Take a tour if you'd like, or skip the tour and get down to it.

Now, before you get into it, just like any OS, you're going to want to update.

Click the overview button.

.. image:: /image/fedora_overview.png
   :align: center
   :scale: 50%

Click on "Software."

Go to "Updates."

.. image:: /image/fedora_software_center.png
   :align: center
   :scale: 20%

Then you're going to install updates, then restart & update.

Click "Restart and Install."

Alternatively, you can use the below in the terminal::

    sudo dnf -y update
    sudo dnf -y upgrade --refresh

Then top it off with a::

    reboot

.. image:: /image/fedora_restart_install.png
   :align: center
   :scale: 20%

Your system will restart and install updates.

.. image:: /image/fedora_update.png
   :align: center
   :scale: 20%

Congratulations! You have installed Fedora 40 Workstation.