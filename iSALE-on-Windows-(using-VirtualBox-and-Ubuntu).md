## iSALE on Windows (using VirtualBox and Ubuntu)

iSALE is not supported for the native Windows operating system. Windows users should consider two options:

1. Make your PC dual boot (i.e. create an additional disk partition) and install Ubuntu (or some other Linux distribution) in tandem with Windows.
2. Install VirtualBox (or some other virtual computer software) inside Windows; create a Virtual machine (VM); install Ubuntu onto this Virtual machine.

Option 1 is optimal if you want best performance, but is not easily reversible. I.e., you will permanently create a new disk partition--the contents of this can be deleted, but the partition cannot be removed without reinstalling the entire Windows OS.

Option 2 has the advantage that the entire virtual machine can be easily removed. However, running Ubuntu in this way will reduce performance.

We therefore recommend Users consider option 2 in the first instance.

### Installation instructions for VirtualBox / Ubuntu

Note that the following instructions can also be used on Mac OSX, but iSALE can be installed natively on Mac OSX.

1. Install VirtualBox (https://www.virtualbox.org/wiki/Downloads). Download the installer for the desired host system (Windows or Mac) and follow the instructions.
2. Download an Ubuntu desktop disk image (http://www.ubuntu.com/download/desktop). We recommend downloading the 64-bit, Long Term Support (LTS) version. Note where this file (ending .iso) is saved to as you will need to locate this later.
3. Start VirtualBox and create a new machine (click "New" icon in top left and complete new machine wizard).
4. Give your VM a sensible name (e.g., Ubuntu-64) and select Type: Linux / Version: Ubuntu (64 bit)
5. You can leave the remaining options as per default, although we recommend increasing the RAM to at least 2GB, if possible.
6. Once the wizard is complete, the VM that you have created should be listed in the left-hand pane of VirtualBox. Select this machine and start it using the "Start" icon.
7. You will now be prompted for a the installation disk for the OS you want to install onto the VM you just created. If you have a CD/DVD with the Ubuntu disk image on it, you can select a drive and insert this disk.  However, the easiest option is to simply locate the .iso disk image file that you downloaded from the Ubuntu website. To do this, click on the small folder icon next to the drop-down menu (and above the start button), and locate the .iso file on your hard-drive.
8. Now follow the on-screen instructions inside the Virtual Machine to install Ubuntu
9. To complete the installation you will need to restart the VM. When it is running it is recommended to Devices -> Install Guest Additions. 

### Installing iSALE and pre-requisites

Once you have successfully installed Ubuntu on a Virtual Machine on your Windows computer, you should follow the instructions for [iSALE on Ubuntu](https://github.com/isale-code/iSALE2D/wiki/iSALE-on-Ubuntu-and-Debian).

Once you have installed the Ubuntu pre-requisites, you can [install](https://github.com/isale-code/iSALE2D/wiki/Installation-instructions#installing-isale-dellen-for-scientific-use) the relevant version of iSALE.