---
title: Ember.js acceptance tests - how to reset db in beforeEach?
description: ~
category: javascript
tags: [emberjs, ember, javascript, testing]
---

Recently I have started working with Ember.js (2.1) and encountered problem with acceptance testing framework. My problem was, how to reset database before each test run?

### Solution 1 - Ember way?

Here is snippet from official documentation.

{% highlight javascript %} 
module('Acceptance | login', {
  beforeEach() {
    application = startApp();
  },

  afterEach() {
    Ember.run(application, 'destroy');
  }
});
{% endhighlight %} 

So You may think that natural way is to put reset db and load fixures to beforeEach function. Correct... but it won't work. **You can't because testing framework is run inside browser.**

That's a shame. Only solution that comes to my mind is to connect via websocket to node.js service which will reset db, but I think that this will be source of pain in the long run. 

Good thing is that You can use all the helpers that Ember gives You, but thats all pros I can think of.

### Solution 2 - use "normal" browser based tests.

Thats the only option to have really flexible tests and it has worked really well in project I'm working on.

There are many testing frameworks out there, but after research I decided to use [http://nightwatchjs.org](Nightwatch.js). I have also considered Casper.js, but it only works with phantom.js. 

Nightwatch.js has support for pattern called Page Objects and runs tests inside node throught Selenium WebDriver API - so it has everything You need from testing framework.

Any other ideas? Feel free to comment! :)

