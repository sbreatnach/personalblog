---
title: "Serving Python: WSGI"
date: 2018-08-25T13:44:50+01:00
tags:
  - Python
  - WSGI
  - Django
  - Performance
categories:
  - Technical
---

When developing a website in Python, you must make a number of decisions. What framework to use is one: will it be the extremely lightweight approach of [Werkzeug](http://werkzeug.pocoo.org/) or [Bottle](http://bottlepy.org/docs/dev/) to the big heavyweights such as [Django](https://www.djangoproject.com/) or [Turbogears](www.turbogears.org)? Will it process requests using the simple synchronous threads or take advantage of asynchronous approaches like [Tornado](www.tornadoweb.org/en/stable/) or [aiohttp](https://aiohttp.readthedocs.io/en/stable/index.html)? These are all important decisions that will effect how you write the code and limit you in some crucial ways. But what about the WSGI layer? 

<!--more-->

The [WSGI protocol](https://wsgi.readthedocs.io/en/latest/) is sychronous by design so depending on your previous choices it may not be a consideration. For example, Tornado is designed to primarily serve content directly and not via a proxy web server like [Nginx](https://nginx.org/en/) or [Apache](https://httpd.apache.org/). If you do require a WSGI layer (Django being the best-known example) it's all too easy to simply fire up [gunicorn](http://gunicorn.org/) or [something](https://uwsgi-docs.readthedocs.io/en/latest/) [similar](https://cherrypy.org/) and move on.

And if your website doesn't get much use, you are done. End of blog post, right? Well, this was the case where I work up until very recently. Then we turned on a single feature in our backend and now, from time to time, the website is hit with approximately 50+ concurrent, heavy API requests. Cue big blobs of error messages in my inbox. Time to revisit those choices.

We use Django, a choice I didn't make but not necessarily a choice I disagree with. It's a big framework with a huge number of features but it is designed to be a synchronous WSGI server. Thus, performance can be harder to scale. In our case, it was a very common problem we had to solve: database connections. By default in Django, each request opens a DB connection, processes and then closes the connection on request end. This is slow under heavy load and doesn't allow many concurrent requests.

We also used Heroku for quick and easy deployment and scaling. Again, not a decision I disagree with but it does mean we don't have a proxy web server we control in front of our service. This rules out a number of potential optimisations.

So what did we do? In order of changes applied:

* Used gunicorn with [gevent](http://www.gevent.org/) and the recommended number of workers based on CPU cores (on our production environment, about 3). This removed the limit on the number of concurrent requests but it was blowing the DB connection limit for our cluster quite quickly under heavy load. Not good!
* Introduced [pgbouncer](http://pgbouncer.github.io/), a connection pooler. Assigning a max number of DB connections limited the damage to the website but we were still confined.
* Applied gevent and [psycogreen](https://pypi.org/project/psycogreen/) patches for true asynchronous behaviour of the Python code. Now there was less blocking of requests but that darn DB connection limit still persisted under very heavy load.
* Used the [worker-connections](http://docs.gunicorn.org/en/latest/settings.html#worker-connections) option for gunicorn to limit the number of alive connections allowed to some factor based on the DB connection pool size. This meant we weren't hitting the DB connection limit, but instead the clients would get rejected immediately if all workers were busy. Not a significant issue, since our backend has a retry mechanism built-in.

An alternative to all this is [waitress](https://docs.pylonsproject.org/projects/waitress/en/latest/), a WSGI server from the Pylons project. Instead of trying to convert Django into something it isn't, waitress embraces the limits of the WSGI protocol and keeps the synchronous behaviour. Instead, it asynchronously buffers incoming requests and waits until one of the synchronous workers becomes available before passing it on. This would naturally have worse performance under heavy load because the throughput is limited to the number of synchronous workers configured. But it is predictable and easily scalable by throwing more CPU cores and other machines into the cluster.

In the end, we persisted with Gunicorn and it's asynchronous feature set. Not necessarily a bad idea since we now have a website that can take some very heavy load and is somewhat predictable in terms of scaling. But these are the choices and trade-offs that you make, even if you might not carefully consider them at first!