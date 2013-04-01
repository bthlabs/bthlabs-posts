One of my projects required me to write a small Web app that informs a user about status of a long-running server process. The idea is that the user triggers the operation from Web frontend, the backend spawns a worker (implemented as a standalone program), listens to notifications from the worker and passes them to the frontend. I was thinking about implementing (almost) realtime backend and frontend communication and came up with two solutions - WebSocket and `Server-Sent DOM Events <http://www.html5rocks.com/en/tutorials/eventsource/basics/>`_. I decided to go with Server-Sent DOM Events as they're HTTP-based and one-way. While using WebSockets would be simpler (Socket.IO + TornadIO and it is on) I thought it'd be overkill for server-to-client communication.

That's (roughly) the story of `BTHEventSource <https://github.com/tomekwojcik/BTHEventSource>`_ - a cross-browser wrapper for EventSource and Server-Sent DOM Events. I created the library while coding the app mentioned above and poking the tech. It turned out that apart from Internet Explorer not supporting it there are few differences in browser implementations. Safari won't accept event stream served with ``text/event-stream;charset=utf-8`` content type and Opera requires ``application/x-dom-event-stream`` content type. Apparently browser developers take specs as *guidelines* not *specifications* :).

BTHEventSource masks those differences and provides cross-browser XHR long-polling fallback. Long-polling transport supports pretty much all of EventSource features, e.g. ``open`` and ``close`` events, event IDs, custom event types and is compatible with modern or near-to-modern browsers. I've done testing in IE 6+, Opera 11, Safari 5, Chrome 14 and FF 3.6/6/7.

The library isn't bullet-proof or flawless. However it works in my app and does the job well so I thought I'd share it with the world.

Check it out on GitHub. The repo contains the JavaScript lib itself, backend handler class for Tornado 2.x, an example chat app (again Tornado) and some docs. Chat isn't exactly the best example for Server-Sent DOM Events but it's nice to show off the lib live.

If you find any bugs or missing features feel free to use GitHub's issue tracker or fork the project and hack away whatever you need.

.. meta::
    :title: Taming EventSource
    :tags: python,web,javascript
    :published_at: 2011-10-11 21:02:00
    :status: published
    :rss_guid: http://www.bthlabs.pl/taming-eventsource
    :rss_published_at: Wed, 12 Oct 2011 02:02:00 -0700
