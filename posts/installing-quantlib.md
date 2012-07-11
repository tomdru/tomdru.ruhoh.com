---

title: xmldb Tutorial 
date: '2012-07-11'
description: Installing QuantLib with Python bindings 
categories: installation
tags: 
    - python
    - quantlib

layout: post

---

### QuantLib-Python

First install QuantLib with the Python bindings:

    sudo apt-get install quantlib-python

To access QuantLib in a virtual environment:

export LD_LIBRARY_PATH=/usr/lib/python2.7/dist-packages/QuantLib:$LD_LIBRARY_PATH
export PYTHONPATH=/usr/lib/python2.7/dist-packages/QuantLib:$PYTHONPATH
