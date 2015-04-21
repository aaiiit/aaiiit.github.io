---
layout: post
title: "Daemonizing a script within Suwappu with Chef"
date: 2015-04-21 15:01:17 +0200
comments: true
categories: 
---

The Suwappu network consists of multiple web apps and other scripts.
All those should start when the machine is booted.  Webapps use the puma daemon script for now.

With Chef we can create a bootscript on every Suwappu appserver by running 'suwappu::appserver-bootscript'.
The node should contain following information : 

{% highlight json %}
{
  "name": "qualitycontrol.suwappu.net",
  "chef_environment": "_default",
  "normal": {
    "tags": [

    ],
    "rvm": {
      "install_pkgs": [
        "sed",
        "grep",
        "tar",
        "gzip",
        "bzip2",
        "bash",
        "curl",
        "git-core"
      ]
    },
    "app": {
      "name": "qualitycontrol"
    },
    "boot": [
      {
        "name": "quality_control",
        "command": "cd /nfs/apps/qualitycontrol_production/current; nohup bundle exec script/quality_control production > log/quality_control.out 2> log/quality_control.err &"
      }
    ]
  },
  "run_list": [
    "recipe[suwappu::backup_install]"
  ]
}
{% endhighlight %}

