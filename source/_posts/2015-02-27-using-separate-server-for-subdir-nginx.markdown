---
layout: post
title: "Using separate server for subdir - nginx"
date: 2015-02-27 09:22:06 +0100
comments: true
categories: 
---

www.gameswap.be/* and www.gameswap.be/blog uses a different server.
To facilitate this, add location blog to configuration of the reverse proxy (nginx).


{% highlight bash %}
  location /blog {
    proxy_set_header X-Real-IP  $remote_addr;
    proxy_set_header X-Forwarded-For $remote_addr;
    proxy_set_header Host $host;
    proxy_pass http://10.1.0.22:8080;
  }
{% endhighlight %}

