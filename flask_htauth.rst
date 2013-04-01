How often do you need to limit access to a Web app to few people? Very often, right? Sometimes it doesn't make sense to implement full-blown users management and authorization. All you need is login and password prompt and credentials storage for a few people. I faced the same problem in an ongoing pet project of mine and decided to go with basic HTTP auth with a plain old htpasswd file storing user credentials.

I did some research followed by some hacking and decided to package my code into a Flask extension so I can reuse the solution in other apps. Flask-HTAuth is the result of my development.

The extension is dead simple to integrate, supports Apache htpasswd files (minus plaintext passwords) and allows an app to choose which view functions should be protected. Exactly what my case required.

Install it with the usual:

.. sourcecode:: console

    $ pip install flask-htauth

Learn more from the `docs <http://tomekwojcik.github.com/flask-htauth/>`_. Get the code, fork the project and issue pull requests on the `project's repository <https://github.com/tomekwojcik/flask-htauth>`_ on GitHub.

Have fun!

.. meta::
    :title: Flask-HTAuth
    :tags: 
    :published_at: 2012-09-14 21:31:00
    :status: published
    :rss_guid: http://www.bthlabs.pl/flask-htauth
    :rss_published_at: Sat, 15 Sep 2012 02:31:00 -0700
