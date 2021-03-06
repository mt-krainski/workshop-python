******************
Programowanie HTTP
******************

Biblioteki standardowe
======================

``http``
--------

``urllib``
----------

Biblioteki zewnętrzne
=====================

``suds``
--------

``requests``
------------

.. code-block:: python

    >>> import requests

    >>> requests.put('http://httpbin.org/put', data = {'key':'value'})
    >>> requests.delete('http://httpbin.org/delete')
    >>> requests.head('http://httpbin.org/get')
    >>> requests.options('http://httpbin.org/get')

.. code-block:: python

    >>> payload = {'key1': 'value1', 'key2': 'value2'}
    >>> r = requests.get('http://httpbin.org/get', params=payload)
    >>> print(r.url)
    http://httpbin.org/get?key2=value2&key1=value1

    >>> payload = {'key1': 'value1', 'key2': ['value2', 'value3']}
    >>> r = requests.get('http://httpbin.org/get', params=payload)
    >>> print(r.url)
    http://httpbin.org/get?key1=value1&key2=value2&key2=value3

.. code-block:: python

    >>> import requests

    >>> r = requests.get('https://api.github.com/user', auth=('user', 'pass'))
    >>> r.status_code
    200
    >>> r.headers['content-type']
    'application/json; charset=utf8'
    >>> r.encoding
    'utf-8'
    >>> r.text
    u'{"type":"User"...'
    >>> r.json()
    {u'private_gists': 419, u'total_private_repos': 77, ...}

.. code-block:: python

    >>> url = 'https://api.github.com/some/endpoint'
    >>> headers = {'user-agent': 'my-app/0.0.1'}

    >>> r = requests.get(url, headers=headers)

.. code-block:: python

    >>> payload = {'key1': 'value1', 'key2': 'value2'}

    >>> r = requests.post("http://httpbin.org/post", data=payload)
    >>> print(r.text)
    {
      ...
      "form": {
        "key2": "value2",
        "key1": "value1"
      },
      ...
    }

.. code-block:: python

    >>> r = requests.head('http://github.com', allow_redirects=True)

    >>> r.url
    'https://github.com/'

    >>> r.history
    [<Response [301]>]

.. code-block:: python

    >>> import json

    >>> url = 'https://api.github.com/some/endpoint'
    >>> payload = {'some': 'data'}

    >>> r = requests.post(url, data=json.dumps(payload))

.. code-block:: python

    >>> url = 'https://api.github.com/some/endpoint'
    >>> payload = {'some': 'data'}

    >>> r = requests.post(url, json=payload)

* http://docs.python-requests.org/en/master/user/quickstart/#json-response-content
* http://docs.python-requests.org/en/master/dev/contributing/#kenneth-reitz-s-code-style


HTML Scrapping i ``BeautifulSoup``
----------------------------------

.. code-block:: console

    $ pip install beautifulsoup4

.. code-block:: python

    html_doc = """
    <html><head><title>The Dormouse's story</title></head>
    <body>
    <p class="title"><b>The Dormouse's story</b></p>

    <p class="story">Once upon a time there were three little sisters; and their names were
    <a href="http://example.com/elsie" class="sister" id="link1">Elsie</a>,
    <a href="http://example.com/lacie" class="sister" id="link2">Lacie</a> and
    <a href="http://example.com/tillie" class="sister" id="link3">Tillie</a>;
    and they lived at the bottom of a well.</p>

    <p class="story">...</p>
    """

.. code-block:: python

    soup.title
    # <title>The Dormouse's story</title>

    soup.title.name
    # u'title'

    soup.title.string
    # u'The Dormouse's story'

    soup.title.parent.name
    # u'head'

    soup.p
    # <p class="title"><b>The Dormouse's story</b></p>

    soup.p['class']
    # u'title'

    soup.a
    # <a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>

    soup.find_all('a')
    # [<a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>,
    #  <a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>,
    #  <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>]

    soup.find(id="link3")
    # <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>


.. code-block:: python

    for link in soup.find_all('a'):
        print(link.get('href'))

    # http://example.com/elsie
    # http://example.com/lacie
    # http://example.com/tillie

.. code-block:: python

    print(soup.get_text())
    # The Dormouse's story
    #
    # The Dormouse's story
    #
    # Once upon a time there were three little sisters; and their names were
    # Elsie,
    # Lacie and
    # Tillie;
    # and they lived at the bottom of a well.
    #
    # ...

Standard WSGI
=============

Frameworki i technologie webowe
===============================

Google App Engine
-----------------

* https://cloud.google.com/appengine/

A powerful platform to build apps and scale automatically

- **Popular Languages** - Build your application in Node.js, Java, Ruby, C#, Go, Python, or PHP—or bring your own language runtime
- **Open & Flexible** - Custom runtimes allow you to bring any library and framework to App Engine by supplying a Docker container
- **Fully Managed** - A fully managed environment lets you focus on code while App Engine manages infrastructure concerns
- **Monitoring, Logging & Diagnostics** - Google Stackdriver gives you powerful application diagnostics to debug and monitor the health and performance of your app
- **Application Versioning** - Easily host different versions of your app, easily create development, test, staging, and production environments
- **Traffic Splitting** - Route incoming requests to different app versions, A/B test and do incremental feature rollouts
- **Services Ecosystem** - Tap a growing ecosystem of GCP services from your app including an excellent suite of cloud developer tools

``django``
----------

* https://www.djangoproject.com/
* https://github.com/django/django

Django is a high-level Python Web framework that encourages rapid development and clean, pragmatic design. Built by experienced developers, it takes care of much of the hassle of Web development, so you can focus on writing your app without needing to reinvent the wheel. It’s free and open source.

- **Ridiculously fast** - Django was designed to help developers take applications from concept to completion as quickly as possible.
- **Reassuringly secure** - Django takes security seriously and helps developers avoid many common security mistakes.
- **Exceedingly scalable** - Some of the busiest sites on the Web leverage Django’s ability to quickly and flexibly scale.

.. code-block:: console

    $ pip install django

``flask``
---------

* http://flask.pocoo.org/

Flask is a microframework for Python based on Werkzeug, Jinja 2 and good intentions. And before you ask: It's BSD licensed!

.. code-block:: console

    $ pip install Flask
    $ python hello.py
     * Running on http://localhost:5000/

.. code-block:: python

    from flask import Flask
    app = Flask(__name__)

    @app.route("/")
    def hello():
        return "Hello World!"

    if __name__ == "__main__":
        app.run()


``webapp2``
-----------

* https://webapp2.readthedocs.io/en/latest/
* https://github.com/GoogleCloudPlatform/webapp2

webapp2 is a lightweight Python web framework compatible with Google App Engine’s webapp.

- **webapp2 is a simple** - it follows the simplicity of webapp, but improves it in some ways: it adds better URI routing and exception handling, a full featured response object and a more flexible dispatching mechanism.
- **webapp2 also offers the package webapp2_extras** - with several optional utilities: sessions, localization, internationalization, domain and subdomain routing, secure cookies and others.
- **webapp2 can also be used outside of Google App Engine**, independently of the App Engine SDK.

.. code-block:: yaml

    application: helloworld
    version: 1
    runtime: python27
    api_version: 1
    threadsafe: true

    handlers:
    - url: /.*
      script: main.app

.. code-block:: python

    import webapp2

    class HelloWebapp2(webapp2.RequestHandler):
        def get(self):
            self.response.write('Hello, webapp2!')

    app = webapp2.WSGIApplication([
        ('/', HelloWebapp2),
    ], debug=True)

``tornado``
-----------

* http://www.tornadoweb.org/en/stable/
* https://github.com/tornadoweb/tornado

Tornado is a Python web framework and asynchronous networking library, originally developed at FriendFeed. By using non-blocking network I/O, Tornado can scale to tens of thousands of open connections, making it ideal for long polling, WebSockets, and other applications that require a long-lived connection to each user.

.. code-block:: python

    import tornado.ioloop
    import tornado.web

    class MainHandler(tornado.web.RequestHandler):
        def get(self):
            self.write("Hello, world")

    def make_app():
        return tornado.web.Application([
            (r"/", MainHandler),
        ])

    if __name__ == "__main__":
        app = make_app()
        app.listen(8888)
        tornado.ioloop.IOLoop.current().start()

Utils
=====

``atlassian-python-api``
------------------------

* https://github.com/AstroTech/atlassian-python-api

.. code-block:: python

    from atlassian import Confluence
    from atlassian import Jira


    jira = Jira(
        url='http://localhost:8080',
        username='admin',
        password='admin')

    confluence = Confluence(
        url='http://localhost:8090',
        username='admin',
        password='admin')


    JQL = 'project = DEMO AND status NOT IN (Closed, Resolved) ORDER BY issuekey'
    data = jira.jql(JQL)

    status = confluence.create_page(
        space='DEMO',
        title='This is the title',
        body=f'This is the body. You can use <strong>HTML tags</strong>!<div>{data}</div>')

    print(status)


Template
========

``Jinja2``
----------

.. code-block:: html

    <title>{% block title %}{% endblock %}</title>
    <ul>
    {% for user in users %}
      <li><a href="{{ user.url }}">{{ user.username }}</a></li>
    {% endfor %}
    </ul>

Przykłady praktyczne
====================

Prosty serwer HTTP
------------------

.. code-block:: console

    $ python -m http.server 8000 --bind 127.0.0.1

.. code-block:: python

    from http.server import BaseHTTPRequestHandler
    from http.server import HTTPServer

    class testHTTPServer_RequestHandler(BaseHTTPRequestHandler):

        def do_GET(self):
            self.send_response(200)

            # Send headers
            self.send_header('Content-type','text/html')
            self.end_headers()

            # Send message back to client
            message = "Hello world!"

            # Write content as utf-8 data
            self.wfile.write(bytes(message, "utf8"))


    if __name__ == '__main__':
      print('starting server...')

      # Server settings
      # Choose port 8080, for port 80, which is normally used for a http server, you need root access
      server_address = ('127.0.0.1', 8081)
      httpd = HTTPServer(server_address, testHTTPServer_RequestHandler)

      print('running server...')
      httpd.serve_forever()

Zadania kontrolne
=================


REST API
--------

Używając biblioteki standardowej w Pythonie zaciągnij informacje o repozytoriach użytkownika Django na https://github.com

* w przeglądarce internetowej wygeneruj w swoim profilu token https://github.com/settings/tokens

* Następnie z przeglądnij listę z poziomu Pythona i znajdź URL dla repozytorium ``django``.

.. code-block:: python

    "name": "django",
    "full_name": "django/django",

    # wyszukaj "commits_url": ???

* Przeglądnij to repozytorium i jego listę commitów.
* Podaj datę i opis ostatniego commita
* Znajdź numery ID ticketów (``Fixed #...``) z issue trackera, które zostały rozwiązane w ostatnim miesiącu
* Spróbuj skorzystać zamiast biblioteki standardowej z pakietu ``requests``

.. code:: REST

    https://api.github.com/

    GET /orgs/django/repos
    GET /repos/dajngo/django/commits


.. code:: console

    $ curl https://api.github.com/orgs/django/repos


.. code-block:: python

    >>> auth = b'username:token'
    >>> headers={
    ...     'Authorization': 'Basic {}'.format(base64.b64encode(auth).decode('ascii')),
    ...     'User-Agent': 'Python HTTP',
    ...}

    # ...

    >>> body = resp.read().decode()
    >>> data = json.loads(body)
