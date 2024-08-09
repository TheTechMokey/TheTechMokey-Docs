Setup Fedora Workstation 40
===========================

Now we're ready to set up Fedora Workstation 40!

Click "Start Setup."

.. image:: /image/fedora_start.png
   :align: center
   :scale: 25%

Privacy is up to you. Remember that Linux is open-source, meaning everyone contributes to make an awesome experience.

Click "Next" after your selection.

You're going to want to enable Third Party Repositories for ease of use.

Click ``Enable Third-Party Repositories``

Click ``Next``.

The "About You" section is what you will log in with.

Put your name in, and then type in a username for this device.

.. image:: /image/fedora_about_you.png
   :align: center
   :scale: 25%

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
   :scale: 100%

Click on "Software."

Go to "Updates."

.. image:: /image/fedora_software_center.png
   :align: center
   :scale: 25%

Then you're going to install updates, then restart & update.

Click "Restart and Install."

Alternatively, you can use the below in the terminal::

    sudo dnf -y update
    sudo dnf -y upgrade --refresh

Then top it off with a::

    reboot

.. image:: /image/fedora_restart_install.png
   :align: center
   :scale: 25%

Your system will restart and install updates.

.. image:: /image/fedora_update.png
   :align: center
   :scale: 25%

Congratulations! You have installed Fedora 40 Workstation.
