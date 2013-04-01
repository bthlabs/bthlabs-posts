I'm cooking something special, here in my lab. One of things the project requires is generating random and totally fake *users*, complete with e-mail address, username and other details. Some time ago I've used `Forgery Ruby gem <http://rubygems.org/gems/forgery>`_ to generate such data and it worked quite well. So, I thought I'd port it to Python. A few hours later, here it is.

The port is mostly complete. I've skipped a few forgeries and tweaked a few other to my liking. I wouldn't be myself if I didn't change something :).

Install it with the usual:

.. sourcecode:: console

    $ pip install ForgeryPy

Learn more from the `docs <http://tomekwojcik.github.com/ForgeryPy/>`_. Get the code, fork the project and issue pull requests on the `project's repository <https://github.com/tomekwojcik/ForgeryPy>`_ on GitHub.

Have fun!

PS. This is the first piece of code I published on PyPI. Yay me!

.. meta::
    :title: ForgeryPy - An easy to use forged data generator for Python
    :tags: python
    :published_at: 2012-07-12 06:39:00
    :status: published
    :rss_guid: http://www.bthlabs.pl/forgerypy-an-easy-to-use-forged-data-generato
    :rss_published_at: Thu, 12 Jul 2012 11:39:00 -0700
