---
layout: post
title: "Add custom protocol handler to Iceweasel"
date: 2014-09-24 12:00:45 +0200
comments: true
categories: 
---

You may try to edit Firefox/Iceweasel configuration via about:config:

* network.protocol-handler.expose.komodo: true (This protocol should be handled either by the browser or by an external application)
* network.protocol-handler.external.komodo: true (This protocol should be handled by an external application)
* network.protocol-handler.app.komodo: python /path/to/my/script.py (Path to a program to handle the request)
