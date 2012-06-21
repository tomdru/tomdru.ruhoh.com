---
title: Installing Numerical Packages in Python with Pip
date: '2012-06-12'
description:
categories: installation
tags: [pandas, pip, numpy, scipy]

layout: post
---

### Prerequisites

Have [installed Xubuntu 12.04 in a Virtual Machine](/installation/installing-a-xubuntu-virtual-machine-for-developers/).

### Dependencies

One of the advantages of Python is the availability of a large number of numerical packages. Installing these, particularly pandas, can be frustrating because of certain dependencies.

To install these packages you will first need to execute the following

    sudo apt-get install libamd2.2.0 libblas3gf libc6 libgcc1 libgfortran3 liblapack3gf libumfpack5.4.0 libstdc++6 build-essential gfortran python-all-dev libatlas-base-dev libfreetype6-dev libpng12-dev

This installs

* *libamd2.2.0* - an approximate minimum degree ordering library for sparse matrices
* *libblas3gf* - the Basic Linear Algebra reference implementations, shared library
* *libc6* - the Embedded GNU C Library, shared libraries
* *libgcc1* - the Embedded GNU C Library, shared libraries
* *libgfortran3* - a runtime library for GNU Fortran applications
* *liblapack3gf* - the Library of Linear Algebra Routines 3, shared version
* *libumfpack5.4.0* - a sparse LU factorization library
* *libstdc++6* - the GNU Standard C++ Library v3
* *gfortran* - the GNU Fortran 95 compiler
* *python-all-dev* - a package depending on all supported Python development packages 
* *libatlas-base-dev* - the Automatically Tuned Linear Algebra Software, generic static
* *libfreetype6-dev* - FreeType 2 font engine, development files
* *libpng12-dev* - PNG library - development

Next, execute the following within a virtual enviroment

    pip install numpy

and then

    pip install scipy pandas matplotlib

[NumPy](http://numpy.scipy.org) handles efficient matrix- and vector-type operations. [SciPy](http://www.scipy.org/) extends many of the objects and functions in NumPy and is 
geared toward scientific computing. [Pandas](http://pandas.pydata.org/) provides data structures and data analysis tools. [Matplotlib](http://matplotlib.sourceforge.net/) provides a 
graphing capability and other tools for visualizing data.


