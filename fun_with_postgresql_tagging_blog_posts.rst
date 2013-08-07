Fun with PostgreSQL: Tagging blog posts
=======================================

The other day I was tasked with adding tagging functionality to one of the
projects I'm working on. While this is quite basic functionality it comes with
a few challenges - from properly configuring relations in the DB and the ORM,
through properly handling operations on tags to properly handling
connections between tags and tagged entities.

How tagging (usually) works?
----------------------------

If I were writing a blogging platform I'd do the following to implement
tagging posts:

1. Create ``posts`` table,
2. Create ``tags`` table to store all the tags,
3. Create ``posts_to_tags`` table to store connections between posts and tags,
4. Configure the ORM to see many-to-many relationship between posts and tags,
5. Write application code to handle tags and post-to-tags connections.

To do this right, I'd have to put a lot of consideration and care into managing
tags (e.g. handling duplicate tags) and post-to-tags connections (e.g. removing
the existing connections when updating a post).

When displaying posts I'd have to issue a separate query to load tags for
each post I'd like to display. That'd require more resources for my app and put
the DB server(s) under heavier load.

When searching for posts by tag I'd have to issue quite an expensive query with
two joins in it.

Caching posts with their tags and search by tag results would require writing
additional glue code in the application.

There must be an easier way to achieve this.

How tagging could work while being simple?
------------------------------------------

How about saving tags with every post? Here's where PostgreSQL's ``ARRAY`` data
type comes into play. To add tags to posts I'd just add ``tags`` column to
``posts`` table and set it to store an array of strings. Then, when saving a
post I'd simply take whatever tags the user entered and save them in the
array.

When displaying posts I'd simply display the array of tags stored in the
column.

When searching for posts by tag I'd simply add a ``WHERE`` condition to the
query.

Caching posts and search by tag results would be no different from caching any
other query results.

Sounds nice and easy but would it work? How would it affect the performance?

Relational tags vs array based tags - the test
----------------------------------------------

I decided to test the performance of both solutions.

**NOTE**: This test has nothing to do with real-world benchmark. Please **do
not** treat what you're going to read as an ultimate answer to the performance
difference question. I'm yet to use PostgreSQL array columns in production.

**The test setup**

I created a few tools to set up and populate the tables with some pseudorandom
data. The idea wass to create 10000 posts and tag each one with 5 randomly
chosen tags. I also created three posts which I tagged with pre-defined tags to
make testing queries simpler. You can download the tools from `this gist`_.

**The test queries**

Test query for relational tags:

.. sourcecode:: postgres

    select posts.*
    from tags
    left join posts_to_tags on posts_to_tags.tag_id = tags.id
    left join posts on posts.id = posts_to_tags.post_id
    where tags.name = 'lorem'
    order by posts.id asc;

Test query for array based tags:

.. sourcecode:: postgres

    select * from flat_posts where tags @> ARRAY['lorem'] order by id asc;

**The test environment and procedure**

I performed the test using PostgreSQL 9.2.4 running on my MacBook Pro (2 x i5
at 2.3GHz, 8GB RAM, Samsung 830 SSD, OS X 10.8.2). Since the MacBook is my
primary work and play machine, the OS environment wasn't exactly
benchmark-friendly. In fact, it wasn't benchmark friendly at all since while
testing the performance I had a number of other apps and services running :).

I tested the performance using the following procedure:

1. Stop the PostgreSQL server,
2. Start the server,
3. ``$ psql``
4. ``\pset pager``,
5. ``\timing``
6. Execute the query and take a note of its execution time,
7. Repeat step 6 fourteen more times,
8. Calculate the mean execution time.

**The test results**

Median query execution time for relational tags: **17.613** ms

Median query execution time for array based tags: **7.891** ms

Final thoughts
--------------

Turns out array based tags performed better in my totally unreliable test. To
be honest, I was a bit suprised when I saw how good the array filtering
performance was. I expected the result to be quite the opposite.

``ARRAY`` data type in PostgreSQL is a nice thing to have and to use. If I were
to implement the tagging functionality I mentioned in the beggining of this
post again I'd use an array columns. If I were to write, say, an Instagram
clone I'd go with different tagging implementaion. The thing is that array column would
work until there's a small number of entries. In the tests I performed while
playing around I found that 20+ items in the tags array caused a major
performance hit.

Discuss this post on `Reddit`_.

.. _this gist: https://gist.github.com/tomekwojcik/9015b7213179cae06b7c#file-readme-rst

.. _Reddit: http://www.reddit.com/r/programming/comments/1gyv2y/fun_with_postgresql_tagging_blog_posts/

.. meta::
    :title: Fun with PostgreSQL: Tagging blog posts
    :tags: postgresql
    :status: published
