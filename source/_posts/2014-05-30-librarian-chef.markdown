---
layout: post
title:  "Using Librarian Chef"
date:   2014-05-30
categories: servers chef librarian devops
---

Chef Repo should have Cheffile.  
Seems to work like bundler and stuff.

Add needed cookbooks to file

  cookbook 'zeromq',:git => 'https://github.com/plu/zeromq-cookbook'  


Run librarian-chef install to install new cookbooks



Roles
=====

  * base

    - add deployer user with ssh key
    - apt-get update


  * zeromq

    - install zeromq


  * ruby-zeromq

    - install ruby (Rubinius 2.2.6)
    - install Ruby zmq library

