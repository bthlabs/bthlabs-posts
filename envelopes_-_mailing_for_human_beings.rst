Envelopes - Mailing for human beings
====================================

Envelopes is a tiny library I wrote to make working with Python's *email* and
*smptlib* packages simple and fun.

Envelopes abstracts all the weird stuff about Python's outgoing e-mail tools
and makes composing and sending e-mails simple. It supports all the features
you'd expect it to support - long and short e-mail addresses, text and HTML
bodies, CC and BCC fields, standard and custom headers, file attachments and
charsets. Envelopes can be used in Web apps, queue workers and pretty much
anywhere you'd use *email* and *smptlib* to send e-mails.

Just look at the following example:

.. sourcecode:: python

    from envelopes import Envelope

    envelope = Envelope(
        from_addr=u'from@example.com',
        from_name=u'From Example',
        to_addr=u'to@example.com',
        to_name=u'To Example',
        subject=u'Envelopes demo',
        text_body=u"I'm a helicopter!"
    )
    envelope.add_attachment('/Users/bilbo/Pictures/helicopter.jpg')
    envelope.send('smtp.googlemail.com', login='from@example.com',
                  password='password', tls=True)

All the dirty work is done for you :).

Install it with the usual:

.. sourcecode:: console

    $ pip install Envelopes

Learn more from the `docs <http://tomekwojcik.github.io/envelopes/>`_. Get the code, fork the project and issue pull requests using the `project's repository <https://github.com/tomekwojcik/envelopes>`_ on GitHub.

Have fun!

.. meta::
    :title: Envelopes - Mailing for human beings
    :tags: python
    :published_at: 2013-08-07 17:20:00
    :status: published
