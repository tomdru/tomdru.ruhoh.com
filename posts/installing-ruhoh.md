---
title: Installing Ruhoh 
date: '2012-06-12'
description:
categories: installation
tags: [ruhoh, ssh]

layout: post
---

Ruhoh is a blogging platform based on Markdown.

### Prerequisites

Have [installed Xubuntu 12.04 in a Virtual Machine](/installation/installing-a-xubuntu-virtual-machine-for-developers/).

Have [version control software installed](/installation/installing-version-control-software/).

### Ruby

Install Ruby, using the instructions [here](http://lenni.info/blog/2012/05/installing-ruby-1-9-3-on-ubuntu-12-04-precise-pengolin/). You will also need to add libyaml

    sudo apt-get install libyaml-dev
    
The following assumes that you already have a GitHub account and an SSH key associated with it. If you do not have an SSH key, follow the instructions [here](http://help.github.com/linux-set-up-git/).

Make sure that any SSH keys you make will be saved by moving them to the Dropbox config folder and replacing their folder with a link

    mkdir ~/Dropbox/config/ssh
    mv ~/.ssh/ ~/Dropbox/config/ssh
    ln -s ~/Dropbox/config/ssh/.ssh ~
    
### Setting up a Ruhoh repository

Now follow the instructions for setting up your ruhoh repository at [ruhoh.com](http://www.ruhoh.com). You will be cloning the ruhoh repository and then installing ruhoh. The instructions will guide you through the process of testing and drafting posts. To actually push a post to the web, you will have to use git

    git add .
    git commit

You will then be prompted for a message. Provide this, save, and close the file. Finally, push the change

    git push

You will use for updating any posts or pages, or to change your configurations. For example, this blog uses a customized version of the *sunburst* theme, which comes with ruhoh. Edit the *config.yml* file and change the *theme* under *google_prettify*. Commit and push this change.


