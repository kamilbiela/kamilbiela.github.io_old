---
layout: post-no-feature
title: Remote debugging PHP with Phpstorm
description: ~
category: howtos
tags: [php, xdebug, phpstorm, debugging, vagrant]
comments: true
---

I'm primary using it for debugging code on "remote" vagrant machines.

All of those instructions are for Linux/Ubuntu - for other systems I recommend getting familiar with [Vagrant](http://vagrantup.com) machines.

## Xdebug configuration

### Install xdebug php extenstion

``apt-get install php5-xdebug``

### Configure it.

Edit ``/etc/php5/mods-available/xdebug.ini``. By default it has only one line that loads extension. *Add* those lines to file:

{% highlight ini linenos %}
xdebug.remote_enable = 1
xdebug.remote_connect_back = 1
xdebug.remote_port = 9000
xdebug.remote_handler = dbgp
xdebug.remote_mode = req
{% endhighlight %}

You can read more in-depth about those settings on [xdebug docs](http://xdebug.org/docs/remote)

Xdebug module should be activated by default. You can double check it by going to ``/etc/php5/conf.d`` and checking if symlink to Your config file exists.
On ubuntu that symlink is named ``20-xdebug.ini``.

Now restart Your server.

# PhpStorm

For this configuration example, lets assume that our remote site is under http://xdebug.mega.dev/.

*PLEASE NOTE* Don't install php-xdebug extension on production servers, it has big impact on performance.

Open Project Settings 

![Drawing A]({{ site.url }}/images/posts/2013-09-22-php-remote-debugging-with-phpstorm/01_add_server.png)

Click ``+`` sign and add configuration for project. Remember to set ``absolute path on the server``.

![Drawing A]({{ site.url }}/images/posts/2013-09-22-php-remote-debugging-with-phpstorm/02_add_server_2.png)

Next, go to Run > Edit configurations

{:.img-auto}
![Drawing A]({{ site.url }}/images/posts/2013-09-22-php-remote-debugging-with-phpstorm/03_edit_configurations_menu.png)

Click ``+`` and select ``PHP Remote Debug``

![Drawing A]({{ site.url }}/images/posts/2013-09-22-php-remote-debugging-with-phpstorm/04_add_remote_debug.png)

Set Server and Ide key - choose any value You want

![Drawing A]({{ site.url }}/images/posts/2013-09-22-php-remote-debugging-with-phpstorm/05_add_remote_debug_filled.png)

Go to Run > Debug '...'

{:.img-auto}
![Drawing A]({{ site.url }}/images/posts/2013-09-22-php-remote-debugging-with-phpstorm/06_run_debug.png)

After that the debugger tab should open. Add breakpoint in Your code. Remember to always add breakpoint on line with code. Breakpoint on blank lines does not work.

![Drawing A]({{ site.url }}/images/posts/2013-09-22-php-remote-debugging-with-phpstorm/07_add_breakpoint.png)

Open project page with parameter XDEBUG_SESSION_START=``Ide key from settings``

![Drawing A]({{ site.url }}/images/posts/2013-09-22-php-remote-debugging-with-phpstorm/08_start_debugging.png)

And thats it! You should have now working xdebugger in Your PhpStorm!

![Drawing A]({{ site.url }}/images/posts/2013-09-22-php-remote-debugging-with-phpstorm/09_xdebug_working.png)