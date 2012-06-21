---
title: Installing a Xubuntu Virtual Machine for Developers
date: '2012-06-11'
description:
categories: installation
tags: [virtualmachine, vim, xubuntu, virtualenv, pip]

layout: post
---

The following is a guided installation of a Xubuntu 12.04 virtual machine with the following capabilities

* File sharing using Dropbox
* Source control
* Virtual environments

### Install VirtualBox

Download the latest VirtualBox package for [your host system](https://www.virtualbox.org/wiki/Downloads). Run the installer.

Download the 64bit Desktop version of Xubuntu from [http://xubuntu.org/getxubuntu/](http://xubuntu.org/getxubuntu/)

Open VirtualBox, and click the "New" button in the upper left hand corner.
Use the following settings:

* **Name**: *stemcell*
* **Operating System**: *Linux*
* **Version**: *Ubuntu (64 bit)*
* **Memory**: *2048 MB*
* **Hard disk**: *VDI, Dynamically allocated, 500 GB*

In Settings -> Display, change Video Memory to 128 MB.

In Settings -> Storage, click Plus Sign button, Add CD/DVD device, Choose disk and locate the Xubuntu ISO in the Downloads folder.

In Settings -> Network, choose Attached to: Bridged Adapter.

Now ***Start*** your virtual machine.

### Install Xubuntu Desktop 12.04

You will first need to install Xubuntu on your empty virtual machine. This is done through a series of graphical menus:

* **Welcome** - The default language is *English*. Select *Install Xubuntu*.

* **Preparing to install Xubuntu** - Check *Download updates while installing* and *Install this third-party software*. Select *Continue*.

* **Installation type** - Check *Erase disk and install Xubuntu*. Select *Continue*.

* **Erase disk and install Xubuntu** - Use the default for *Select drive*. Select *Install now*.

* **Where are you?** - Use *New York*. Select *Continue*.

* **Keyboard layout** - For keyboard layout, choose *English (US)*. Select *Continue*.

* **Who are you?** - Assume the user's name is Alice Smith. She would fill in the following
 * Your name: *Alice Smith*
 * Your computer's name: *xubuntu*
 * Pick a username: *ubuntu*
 * Choose a password: *secret*
 * Confirm your password: *secret*
 * Choose whether you would like to log in automatically or always be prompted for your password. The system will begin installing.

* **Installation Complete** - Select *Restart Now*.

The .iso will be ejected automatically. Press ENTER and the system will reboot.

### Snapshot

After the system has rebooted, choose Shut Down with the operating system (in the upper right hand menu.) In the Oracle VM VirtualBox Manager window, click on the Snapshots tab, and click the camera icon to make a snapshot of the fresh install. Call it "fresh-install".

### Install software updates

Open *Accessories > Terminal Emulator*. Execute the following commands:

    wget https://raw.github.com/gist/2703110/25dd6b7be4752b2d3c5932ac1f9e30f38b401139/sources.list
    sudo cp sources.list /etc/apt/
    sudo apt-get update
    sudo apt-get upgrade

You will now be installing a series of packages.

### Install VirtualBox Guest Additions

Open the Terminal Emulator from the top left menu -> Accessories. First install dkms

    sudo apt-get install dkms

Mount the Guest Additions CD by selecting Devices > Install Guest Additions. Move to the folder on the CD and execute a script

    cd /media/VBOXADDITIONS
    sudo ./VBoxLinuxAdditions.run
    
### Snapshot

Once installation is done, shut down and make a new snapshot. Call it "after-upgrade-and-vbox-guest-additions".

Start up your VM and eject the Guest Additions CD. To resize your window, click the + in the upper-left-hand corner. The virtual machine should be in fullscreen mode.

### Install Dropbox

Execute

    sudo apt-get install nautilus-dropbox
    dropbox start -i

Then enter your login and password information. You will be prompted to install the latest version. Do not select this. Select "Don't Ask Again". Choose the "Typical" installation.

You will also need a location for your configuration files, the first of which is .bashrc. Create the folder, move .bashrc and replace it with a link.

    mkdir -p ~/Dropbox/config/bash
    mv ~/.bashrc ~/Dropbox/config/bash
    ln -s ~/Dropbox/config/bash/.bashrc ~
    
The command *ln -s* places a symbolic link to a file or folder wherever you want. You will be able to reference and edit the file as though it were in the target location, although it is actually stored somewhere else.

### Install vim

Xubuntu automatically comes with vi, a powerful text editor. Vi can be used to write any kind of text document. Vim makes the editor ideal for coding, as it adds features like syntax highlighting.

To install execute

    sudo apt-get install vim

You should also edit the .vimrc, which should be empty. Download the recommended configuration from Praxis

    mkdir ~/Dropbox/config/vim
    wget https://raw.github.com/gist/1295884/d786bbd469cb700666daad5d21d26ca3eeb9b6be/.vimrc
    ln -s ~/Dropbox/config/vim/.vimrc ~

One useful feature of this configuration is that it substitutes four spaces for a tab when you hit the tab key. Tabs can be difficult to work with and is considered bad style.

### Snapshot

Finally, shut down and make a snapshot called "after-dropbox-and-vim".
