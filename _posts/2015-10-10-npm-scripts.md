---
title: Using npm scripts in Your development workflow
description: ~
category: javascript
tags: [javascript, npm, build]
---

While developing node / javascript application, You usually use build tools like grunt or gulp. Those are endlessly useful, but what when You often run complicated commands like:

{% highlight bash %}
npm run ember -- serve --proxy http://vagrant-host-api.local/
{% endhighlight %}

Those are hard to remember and it's something that You don't want to retype.

### package.json & npm to the rescue

You could change above command to `npm run-script proxy` by adding "scripts" property to package.json like this:

{% highlight json %}
{
  "name": "your package name",

  ...

  "scripts": {
    "proxy": "npm run ember -- serve --proxy http://vagrant-host-api.local/"
  }
}
{% endhighlight %}

Best thing that You can add many of those and run it like this:

{% highlight bash %}
npm run-script proxy
{% endhighlight %}

### special name script

There are few of "scripts" that have special meaning and are run automatically when running various npm commands. You can find a full list here: [https://docs.npmjs.com/misc/scripts](). Most interesting are:

#### start, prestart, poststart

The content of "start" script is executed when You type `npm start`. It's awesome for specifying how to actually start Your program.

#### install

I tend to use it (for non-public) projects that aren't meant to be a package and put there a "bower install". It's super useful and You don't need to explain Your team (which don't necessarily know much about node) how to make app working. They just run npm install and everything is magically done for them.

Also, read [https://docs.npmjs.com/misc/scripts#best-practices]() which will give You some more insight about using it.

#### test

Awesome way of specifying how to run app tests.

### Big gain

The biggest gain of using "script" field is that all the commands are in one, well-organized place. Other team members will surely be thankful for this :).

### Further read

* [npm docs entry on "script" field](https://docs.npmjs.com/misc/scripts)
* [Usage of scripts with build tools like grunt/gulp](http://engineering.hobsons.com/2015/06/26/build-tools-vs-npm-scripts-why-not-both/)
* [example of package.json with many custom scripts](https://github.com/keithamus/npm-scripts-example/blob/master/package.json)
* [npm blog post focusing on using "test" script field.](http://blog.npmjs.org/post/127671403050/testing-and-deploying-with-ordered-npm-run-scripts)
