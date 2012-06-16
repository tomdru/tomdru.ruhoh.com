---

title: Installing BDB XML
date: '2012-06-12'
description: Installing BDB XML
categories: installation 
tags: 
    - ubuntu
    - precise
    - bdb
    - xml
    - rlwrap

layout: post

---

Installing BDB XML
------------------

### Prerequisites

Have [installed Xubuntu 12.04 in a Virtual Machine](/installation/installing-a-xubuntu-virtual-machine-for-developers/).

### Introduction

Read [this](http://zeth.net/post/350/) for a little introduction to BDB XML.

### Download and install

Download BDB XML from [Oracle's web site](http://www.oracle.com/technetwork/products/berkeleydb/downloads/index.html). You'll need to create a login (free) if you don't have one already.

Decompress the downloaded file:

	cd ~/Downloads
	tar xvfz dbxml-2.5.16.tar.gz

Before building the source, modify one of the files:

	~/Downloads/dbxml-2.5.16/xqilla/include/xqilla/framework/XPath2MemoryManager.hpp

In the file, after line 26 add a line with

	#include <cstddef>

After which you can now build:

	cd dbxml-2.5.16/
	sh buildall.sh

More build options can be [found here](http://docs.oracle.com/cd/E17276_01/html/ref_xml/xml_unix/intro.html).

Once compilation is complete, the dbxml binary is located in

	~/Downloads/dbxml-2.5.16/install/bin/

I suggest either moving the binary, or making a symlink:

	ln -s ~/Downloads/dbxml-2.5.16/install/bin/dbxml ~/bin/dbxml

and make sure that ~/bin is in your PATH:

    export PATH=$PATH:$HOME/bin

### Rlwrap

I recommend using rlwrap to add input history and command completion.

Install rlwrap

	sudo apt-get install rlwrap

Create a script in ~/bin called "start_dbxml.sh" to start dbxml:

	#!/usr/bin/env bash
	
	mkdir -p $HOME/.rlwrap/dbxml/"`date +%Y%m%d`"
	
	rlwrap -rcl $HOME/.rlwrap/dbxml/`date +%Y%m%d`/`date +%H%M%S-%N`.log dbxml

### Python bindings

Install system-wide the python bindings. Execute:

	$ cd ~/Downloads/dbxml-2.5.16/dbxml/src/python/bsddb3-4.8.1/
	$ python setup.dbxml.py build
	$ sudo python setup.dbxml.py install

You can then build and install the dbxml module:

	$ cd ..
	$ python setup.py build
	$ sudo python setup.py install

If you're going to work in a virtual enviroment, you need to symlink the installed resources. Let's say your virtual environment has its python packages installed in the following directory:

    ~/vedev/veclove/local/lib/python2.7/site-packages

Navigate into this folder, then execute:

    ln -s /usr/local/lib/python2.7/dist-packages/dbxml.py .
    ln -s /usr/local/lib/python2.7/dist-packages/dbxml.pyc .
    ln -s /usr/local/lib/python2.7/dist-packages/_dbxml.so .


