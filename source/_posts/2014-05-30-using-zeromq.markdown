---
layout: post
title:  "Using ZeroMQ"
date:   2014-05-30
categories: messaging suwappu zeromq servers chef
---


Install through Chef [zeromq cookbook](https://github.com/plu/zeromq-cookbook)

This cookbook has been added to Role zeromq


ZeroMQ Version
==============

Use this C-code to get the version of ZeroMq.

  {% highlight C %}
  #include <stdio.h>
  #include "zmq.h"

  int main (int argc, char const *argv[]) {
    int major, minor, patch;
    zmq_version(&major, &minor, &patch);
    printf("Installed ZeroMQ version: %d.%d.%d\n", major, minor, patch);

    return 0;
  }

  {% endhighlight %}


Compile and run:

  {% highlight bash %}
  gcc -lzmq zeromq-verion.c -o zeromq-version
  ./zeromq-version
  Installed ZeroMQ version: 3.2.4
  {% endhighlight %}
