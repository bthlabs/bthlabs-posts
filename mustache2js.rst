Some time ago I started using Mustache in apps I write to make tedious task of generating HTML in JavaScript easier and more fun. Now, Mustache does the job well and fits my needs. There's one problem, however. When I first tried to use the Mustache template in browser I found that it was pretty much impossible. Somewhere in the Internets I found someone's post where he suggested we should use wrap Mustache code in ``script`` tag with ``text/html`` type. At first I was like *WTF?* but then I was like *including all the templates in every HTML? srsly?* because this method wouldn't work when loading templates from files. I was stuck.

But then an idea came - write a script that takes Mustache file, wrap it with some CoffeeScript code and compiles the CoffeeScript to JavaScript. This way I get plain old JavaScripts I can easily include in my apps. This way `mustache2js <https://github.com/tomekwojcik/mustache2js>`_ was born.

The script is pretty much functional with some rough edges (most notably almost nonexistent exceptions handling that'll cause tracebacks being written to output). It works for me. If something doesn't work for you feel encouraged to use GitHub to file an issue or fork and fix. You know the drill :).

.. meta::
    :title: mustache2js
    :tags: python,javascript
    :published_at: 2012-01-27 20:23:23
    :status: published
    :rss_guid: http://www.bthlabs.pl/mustache2js
    :rss_published_at: Sat, 28 Jan 2012 03:23:23 -0800
