One of my last tasks before leaving Weeby was to release `StatusBoard on GitHub <https://github.com/weeby/StatusBoard>`_. I was very happy to see the app being open-sourced as I had a lot of fun (and did some magic) during its development and wanted to use it outside the company. For more info please see the app's GithHub page.

I forked the app and started to tweak it to make it more suitable for general use. Here's a small roundup of changes I made.

**Rewrite JavaScript code**

I decided to rewrite the JavaScript part of the app to use jQuery (instead of MooTools) and to make possible its use in themes.

**Theming**

Themes allow users to change the app's look and feel without touching the original source. Just code your own HTML file, JavaScript code (to handle events and other things), throw some CSS and other resources and you're good to go :). During development of this feature I came up with *Bootstrapped* theme that uses, well, Twitter's Bootstrap and supports exactly the same channels as the built-in theme.

**New workers, changed workers and reworked channels**

There are two new workers - ``FeedWorker`` and ``TwitterWorker``. They allow the app to pull data from RSS/Atom/CDF feeds and Twitter timelines. As for Twitter - the app uses public Twitter timelines so it won't work with protected accounts. I did so to avoid using OAuth. Also, by default the app reads tweets every ten minutes. Feel free to change that interval but tweak it carefully to avoid being rate-limited by Twitter. Twitter worker will automagically adjust interval if rate-limited but please play nice with Twitter so they don't ban your IP ;).

From now on the XMPPBot uses Redis (more on that later) instead of SQLite DB to store messages it processes.

Channel definitions have been reworked to support many instances of one worker. My fork's README file discusses these changes.

**Master/slave modes powered by Redis PubSub**

This is probalby the biggest change. The app now supports two operation modes - master or slave. The master instance runs workers, writes to Redis DB and broadcasts events to slaves. Slaves on the other hand are read-only and only listen to notifications sent by the master.

I implemented this feature to make scaling easier. You can run many as many slaves as you need and only one master. This way you can handle lots of connections and you don't have to worry about syncing instances - it's all done for you under the hood.

This functionality is powered by Redis PubSub and `brukva <https://github.com/evilkost/brukva>`_ - an asynchronous Redis client for Tornado.

You can get the code for this version from `my fork on GitHub <https://github.com/tomekwojcik/StatusBoard>`_. I'd like to say *Thanks* to Weeby team for releasing the app for our fun and profit :).

.. meta::
    :title: Weeby StatusBoard: Reloaded
    :tags: python,weeby,web
    :published_at: 2012-06-18 05:51:54
    :status: published
    :rss_guid: http://www.bthlabs.pl/weeby-statusboard-reloaded
    :rss_published_at: Mon, 18 Jun 2012 10:51:54 -0700
