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

### Python bindings

Install system-wide the python bindings. Execute:

	$ cd ~/Downloads/dbxml-2.5.16/dbxml/src/python/bsddb3-4.8.1/
	$ python setup.dbxml.py build
	$ sudo python setup.dbxml.py install

You can then build and install the dbxml module:

	$ cd ..
	$ python setup.py build
	$ sudo python setup.py install

Create two folders in /opt to house dbxml and bsddb3. First, let's move dbxml:

	$ sudo mkdir -p /opt/bbdbxml/dbxml-2.5.16

Nagivate to the dbxml files, and move them into /opt/bbdbxml/dbxml-2.5.16:

	$ cd /usr/local/lib/python2.7/dist-packages/
	$ sudo mv dbxml-2.5.16.egg-info /opt/bbdbxml/dbxml-2.5.16/
	$ sudo mv dbxml.py /opt/bbdbxml/dbxml-2.5.16/
	$ sudo mv dbxml.pyc /opt/bbdbxml/dbxml-2.5.16/
	$ sudo mv _dbxml.so /opt/bbdbxml/dbxml-2.5.16/

Next, move bsddb3:

	$ sudo mkdir /opt/bbbsddb3/
	$ cd /opt/bbbsddb3/
	$ sudo mv /usr/local/lib/python2.7/dist-packages/bsddb3-4.8.1-py2.7-linux-x86_64.egg/ .

Create two symlinks:

	$ sudo ln -s /opt/bbdbxml/dbxml-2.5.16 /opt/bbdbxml/current
	$ sudo ln -s /opt/bbbsddb3/bsddb3-4.8.1-py2.7-linux-x86_64.egg/ /opt/bbbsddb3/current

You will need to modify your *PYTHONPATH* and *LD\_LIBRARY\_PATH* to point to the new folders you created in /opt. Create a script with the following content to launch iPython.

	#!/usr/bin/env bash
	
	export PYTHONPATH=$PYTHONPATH:/opt/bbdbxml/current:/opt/bbbsddb3/current
	export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/bbdbxml/current:/opt/bbbsddb3/current
	
	ipython


