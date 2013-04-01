Imagine you'd like to publish a live stream from an event, say your dog's first birthday. What tool would you use? You could set up a WordPress instance and publish the stream using it. That would do but wouldn't be cool - people reading the stream would have to refresh the whole page and you'd have to mess with heavy CMS. You could use Twitter and publish the stream using a hash tag. That wouldn't be cool either since your friends watching the event would have to be familiar with Twitter and anyone could tweet using the hash tag. What would really be cool is a dedicated app, that uses some sort of push technology to deliver your updates to all the users once you post them. Now that's interesting, right? But coding such an app takes time and requires messing with browser quirks, setting up server and doing many things. And you haven't got that much time - you have to prepare party for your doggy. This is exactly where Pusher kicks in. They provide you with backend for your live stream and a client lib that's very easy to use and deals with all the dirty stuff for you. What you have to do is write an app that you'll use to deliver messages to people and code some JavaScript that'll handle incoming messages. That's an easy task, isn't it?

That was the story behind PusherCast. Well, not exactly because I wasn't (and am not) going to stream any dog's birthday in the Net ;). I was just searching for a real-world example of Pusher's use and this idea popped into my head. I decided to write it adding one thing - local MongoDB storage. Why? Firstly to provide users that join the event after it started with history of what's been already posted. Secondly to ease creating post-event log - reading the stream from Mongo and rendering it as a static HTML is a matter of one small Python script.

The app uses Tornado as a backend server. Why? Because Tornado provides non-blocking HTTP requests. That's a cool feature that gives a lot of power. PusherCast uses this feature to post messages to Pusher backend. In order to do that I had to patch Pusher's Python library replacing it's blocking HTTP connection with Tornado's mechanisms. The patched library is available `here <https://github.com/tomekwojcik/pusher_client_python>`_. If you'd prefer using not modified library then you'd have to add the TornadoChannel to the app manually.

The backend also serves HTML file for the client app. The client app is dead simple and minimal. It sets up Pusher client and allows publishing new messages. In a production app you'd want to implement some sort of auth mechanism so that only certain people can publish. You could also think of a few other features, e.g. photo attachments and better message parsing to enable links etc. But that's not a production app so if you want those features consider forking it and implementing them. This is just a demo thingy.

Pusher is an awesome project. They provide hassle free service that's very easy to implement. It took me about 2 hours to code backend posting and client handling of messages. I was really amazed, given the feature they provide. I tested the app with a bunch of friends and none of us experienced any problems. That's really cool.

PusherCast is available on `GitHub <https://github.com/tomekwojcik/PusherCast>`_ for anybody interested in the code. The app is also available `live <http://pushercast.bthlabs.pl/>`_ for anybody who'd like to see it in action.

Have fun :).

.. meta::
    :title: PusherCast - Pusher in action
    :tags: python,tornado,cloud,web
    :published_at: 2011-05-15 19:04:55
    :status: published
    :rss_guid: http://www.bthlabs.pl/pushercast-pusher-in-action
    :rss_published_at: Mon, 16 May 2011 00:04:55 -0700
