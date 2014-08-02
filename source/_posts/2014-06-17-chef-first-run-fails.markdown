---
layout: post
title:  "Chef fails on bootstrapping the first time"
date:   2014-06-17
categories: server chef
---

= Problem

{% highlight bash %}
shops.suwappu.net Installing Chef Client...
shops.suwappu.net --2014-06-17 10:12:40--
https://www.opscode.com/chef/install.sh
shops.suwappu.net Resolving www.opscode.com (www.opscode.com)... 184.106.28.90
shops.suwappu.net Connecting to www.opscode.com
(www.opscode.com)|184.106.28.90|:443... connected.
shops.suwappu.net ERROR: The certificate of `www.opscode.com' is not trusted.
shops.suwappu.net Starting first Chef Client run...
shops.suwappu.net bash: line 85: chef-client: command not found
[master][/Code/suwappu/chef-resto/chef-repo-new] librarian-chef 
{% endhighlight %}
