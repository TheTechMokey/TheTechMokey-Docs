Install Proxmox
================

Donload ISO from

Installing with ``dd`` command

Locate your drive you want to install the ISO to.

.. code:: bash

    lsblk

Unmount the USB Drive: If the USB drive is mounted, unmount it. Replace /dev/sdX1 with the correct partition identifier (e.g., /dev/sda1).

.. code:: bash
    
    sudo umount /dev/sdX1

Create the Bootable USB: Use the ``dd`` command to write the ISO image to the USB drive. Replace /path/to/image.iso with the path to your ISO file and /dev/sdX with the USB drive (e.g., /dev/sdb).

.. code:: bash

    sudo dd if=/path/to/image.iso of=/dev/sdX bs=4M status=progress


- ``if`` = specifies the input file (the ISO image).
- ``of`` = specifies the output file (the USB drive).
- ``bs`` = 4M sets the block size to 4 megabytes for faster writing.
- ``status`` = progress provides progress information during the operation.

.. important:: 

Be absolutely certain that of= points to the USB drive and not a partition (e.g., /dev/sdX and not /dev/sdX1). Using the wrong device can result in data loss.

Sync and Eject: After the dd command finishes, ensure all data is written to the USB drive and then safely eject it.

.. code:: bash

    sudo sync


You can then physically remove the USB drive or use a tool to safely eject it.

