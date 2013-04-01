Flask itself doesn't come with forms library bundled. However there's an extension available that offers WTForms integration. I used it in my Flask training app and had some tough time trying to reuse a form on a single view. The idea was simple - I'd put a comment form in a single post view, point the form to the view itself and handle the form in it if needed. The problem was trying to reset the form after successful posting so that the user wouldn't see their last comment in it while keeping the default CSRF protection intact. The solution is pretty simple yet not that obvious. Take a look at the code below.

.. gist:: https://gist.github.com/953046

The magic happens in ``ReusableForm.reset()`` method - here we populate the form with data set containing only one field - the CSRF field which is reset to a new value after every successful posting.

Believe it or not but it took me some time to figure it out :).

.. meta::
    :title: Reusing Flask-WTF forms.
    :tags: flask,python
    :published_at: 2011-05-02 21:11:00
    :status: published
    :rss_guid: http://www.bthlabs.pl/reusing-flask-wtf-forms
    :rss_published_at: Tue, 03 May 2011 02:11:00 -0700
