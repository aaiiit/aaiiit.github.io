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


