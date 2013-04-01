I was asked by one of fellow devs why I use accessors for instance vars in Python. *Because I'm used to accessors after coding in Ruby and Objective-C*, I replied and went with my own business. But today `a post by Dropbox about optimizing Python code <http://tech.dropbox.com/?p=89>`_ popped into my head. It states that Python function calls are slow. I coded a small snippet to see how accessors perform compared to just accessing an instance variable. Here it is:

.. gist:: https://gist.github.com/2654619

The results are shocking:

.. sourcecode:: console

    Shire:proptest bilbo$ python proptest.py 
    Without accessor: 0.0742480754852
    With accessor: 0.279271841049

**Accessor function is about 3.75 times slower than direct access.** Now, while this may not matter in many cases I think this matters in case of a Web app, especially one written to handle heavy load. A millisecond more per request multiplied by a thousand of requests turns to a second. Funny that `Tornado example code <https://github.com/facebook/tornado/blob/master/demos/blog/blog.py#L68>`_ suggests using ``@property`` accessor function for DB connection in request handlers.

.. meta::
    :title: A case against accessors in Python
    :tags: python,performance,web
    :published_at: 2012-05-10 05:45:00
    :status: published
    :rss_guid: http://www.bthlabs.pl/a-case-against-accessors-in-python
    :rss_published_at: Thu, 10 May 2012 10:45:00 -0700
