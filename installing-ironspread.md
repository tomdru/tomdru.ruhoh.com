---

title: Installing IronSpread - Python Driven Excel
date: '2012-07-16'
description: Instructions for setting up IronSpread
categories: installation 
tags: 
    - windows-7
    - excel
    - python
    - ironspread

layout: post

---

### Prerequisites

Have installed Windows 7, its updates, and Microsoft Office.

### Python(x,y) and lxml

Download and install [Python(x,y)](http://code.google.com/p/pythonxy/wiki/Downloads) (currently version 2.7.2.3). Use the default recommendations in the installer. Additional Python plugins are available [here](http://code.google.com/p/pythonxy/wiki/AdditionalPlugins). In particular, download and install `lxml`.

### Notepad++

A nice free text editor for editing Python code is [Notepad++](http://notepad-plus-plus.org/). Download and install it.

### Mercurial

Download and install [Mercurial](http://mercurial.selenic.com/wiki/Download). Download the 32-bit installer that does not need admin rights to install.

### Clone mint and clove

Setup a directory structure to store our Python projects. Open the Command Prompt by going to the Start Menu --> All Programs --> Accessories. The directory structure is

	C:\Users\winuser\hgdev\org.bitbucket\

Make a folder called `autonomy` and clone the golden repositories of `clove` and `mint`
	
	C:\Users\winuser\hgdev\org.bitbucket\autonomy>hg clone https://bitbucket.org/autonomy/mint
	C:\Users\winuser\hgdev\org.bitbucket\autonomy>hg clone https://bitbucket.org/autonomy/clove

### Modify PythonPath

We need to modify our `PYTHONPATH` to inform python of the location of our Python projects. Open up the Control Panel by going to Start Menu --> Control Panel. Click on System and Security --> System. On the left side, click on Advanced system settings. Click on the Environment Variables button. In the lower half of the window, under System variables, click New and enter a new System variable.

	Variable name: PythonPath
	Variable value: C:\Users\winuser\hgdev\org.bitbucket\autonomy\mint;C:\Users\winuser\hgdev\org.bitbucket\autonomy\clove

Click OK to save the new settings. To test that the changes have taken effect, open up a new instance of the Command Prompt, and execute the following.

	C:\Users\winuser\>python
	>>> import clove

If you get no errors, you've successfully set up your project.

### IronSpread

Follow the installation instructions in the QuickStart section of [IronSpread](http://www.ironspread.com/quickstart.html). You'll need to first install .NET Framework 4.

### Install Pip

To run the demo project, we'll need to install Pip. First, download the 32-bit version of [7-zip](http://7-zip.org/). Then follow the instructions [detailed here](http://stackoverflow.com/a/4921215).

After pip is installed, install `requests` and `xlrd` via the Commpand Prompt:

	>pip install requests
	>pip install xlrd

These two packages are required for running time-series-demo.xls