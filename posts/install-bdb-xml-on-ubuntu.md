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

layout: post

---

### Prerequisites

Have [installed Xubuntu 12.04 in a Virtual Machine](/installation/installing-a-xubuntu-virtual-machine-for-developers/).

### Introduction

Read [this](http://zeth.net/post/350/) for a little introduction to BDB XML.

### Download and install

Execute

    sudo apt-get install bbdbxml

You will need to modify your *PYTHONPATH* and to point to `/opt/bbdbxml/current/lib`. Create a script with the following content to launch iPython.

	#!/usr/bin/env bash
	
	export PYTHONPATH=/opt/bbdbxml/current/lib:$PYTHONPATH
	
	ipython


