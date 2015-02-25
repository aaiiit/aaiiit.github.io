---
layout: post
title: "install-appserver-internal"
date: 2014-09-02 09:41:55 +0200
comments: true
categories: 
---

Howto install an application server @ Suwappu
---------------------------------------------

  * Add container to data bag openvz-instances hw-node

    {% highlight bash %}
    knife data bag edit openvz-instances hw-node -e vim
    {% endhighlight %}

  * Create specified container on openvz hardware node

    {% highlight bash %}
    knife bootstrap hw-node -r 'suwappu::openvz-instances'
    {% endhighlight %}

  * Install base software that all containers need

    {% highlight bash %}
    knife bootstrap container -r 'suwappu::base'
    {% endhighlight %}

  * Configure node
    node['app']['name']

    {% highlight bash %}
    1 {
    2   "name": "ws1.suwappu.net",
    3   "chef_environment": "_default",
    4   "normal": {
    5     "tags": [
    6 
    7     ],
    8     "app": {
    9       "name": "sdn",
   10       "path": "/u/apps/sdn_production",
   11       "username": "sdn",
   12       "password": "YOURMOMMA"
   13     },
   14     "mysql": {
   15       "server_root_password": "YOURMOMMA"
   16     },
   17     "unicorn-ng": {
   18       "service": {
   19         "environment": "production",
   20         "user": "deploy"
   21       }
   22     },
   23     "nginx": {
   24       "user": "deploy"
   25     },
   26     "rvm": {
   27       "install_pkgs": [
   28         "sed",
   29         "grep",
   30         "tar",
   31         "gzip",
   32         "bzip2",
   33         "bash",
   34         "curl",
   35         "git-core"
   36       ]
   37     }
   38   },
   39   "run_list": [
   40     "recipe[suwappu::appserver]"
   41   ]
   42 }
    {% endhighlight %}

  * Install appserver

    {% highlight bash %}
    knife bootstrap container -r 'suwappu::appserver'
    {% endhighlight %}

  * Install correct ruby version

    {% highlight bash %}
    rvm install rbx-2.2.10
    {% endhighlight %}

  * Capify application
  * Run bundle on server
  * Add SQL db to data bag sql-databases mysql-node

    {% highlight bash %}
    knife data bag edit sql-databases mysql-node -e vim
    {% endhighlight %}

  * Create specified SQL DB

    {% highlight bash %}
    knife bootstrap mysql-node -r 'suwappu::sql-databases'
    {% endhighlight %}

  * Add reverse proxy to data bag nginx-reverse-proxies nginx-node

    {% highlight bash %}
    knife data bag edit nginx-reverse-proxies nginx-node -e vim
    {% endhighlight %}

  * Create specified Reverse Proxy

    {% highlight bash %}
    knife bootstrap nginx-node -r 'suwappu::nginx-reverse-proxies'
    {% endhighlight %}


EDIT: Added node example data
