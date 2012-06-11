---
title: Installing Mint within a Virtual Environment
date: '2012-06-11'
description:
categories: installation
tags: [virtualmachine, vim, xubuntu, virtualenv, pip, mint]

layout: post
---

### Fork the Mint Library

Go to BitBucket, log in to your account, and find the mint repository at [https://bitbucket.org/autonomy/mint](https://bitbucket.org/autonomy/mint). Fork the repository to your account and clone your fork to your hgdev folder by executing

    cd ~/hgdev/org.bitbucket/asmith/
    hg clone https://asmith@bitbucket.org/asmith/mint

### Dependencies

Install the mint dependencies:

    sudo apt-get install libxml2-dev
    sudo apt-get install libxslt1-dev

### Create a virtual environment for mint

You will now create a folder for your virtual environments and set this on your path

    mkdir ~/vedev

Execute the following. This will allow you to enter a virtual environment. 

    echo "source /usr/local/bin/virtualenvwrapper.sh" >> ~/.bashrc
    echo "export WORKON_HOME=~/vedev" >> ~/.bashrc
    
The *source* and *export* commands can be issued at the terminal, but will only remain in effect after your current session by appending them to .bashrc.

Make a new virtual environment:

    mkvirtualenv vemint 

This will add the virtual environment *vemint* and a corresponding folder under vedev. This virtual environment can be entered anywhere on your filesystem with the *workon* command below.

You will now be in the virtual environment. To exit

    deactivate

To enter

    workon vemint

Next, link the folder to your mint hgdev folder

    ln -s ~/hgdev/org.bitbucket/asmith/mint/ ~/vedev/vemint
    
### Mint requirements.txt

Install the mint requirements:

    cd ~/vedev/vemint/mint
    pip install -r requirements.txt

Because mint is not a finished project, we do not want to install it globally. We just want to install it in vemint where we can test it.

If the installation does not run into any errors, run the unit test

    python tests/run.py

If you get some errors, this means that the project has not been updated. It is not necessarily a problem with your setup.
