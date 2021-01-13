# How to use gevent and Flask on Windows

Origin Post: [How to use gevent and Flask on Windows](http://www.danieleteti.it/gevent-and-flask-on-windows.html)

## Flask

Flask is one of most popular python framework for web solution. It is a non-opinionated framework, an I really like it. Flask contains also a nice and useful development web server with automatic reloading. However, when you have to deploy a Flask application you cannot rely on the development web server, you need a production ready system.

## gevent

gevent is a coroutine-based Python networking library that uses greenlet to provide a high-level synchronous API on top of libev event loop. More info about gevent here.

Being WSGI compliant, gevent can be used to serve your Flask application in a professional way. But How should be configured these two guys to work together?

## Serving Flask from gevent

Let's say that you have the following Flask application (file: flask_app.py):

```python
# file: flask_app.py
from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
    return "Hello World"

@app.route('/home')
def home():
    return "This is the home page"
```

To serve this simple application you should, as usual, use the following command line.

```batch
C:/DEV>set FLASK_APP=flask_app.py
C:/DEV>flask run
 * Running on http://localhost:5000/
```

To serve this Flask app using gevent, you can use the following snippet (file: gevent_app.py).

```python
# file: gevent_app.py
from flask_app import app
from gevent.pywsgi import WSGIServer

http_server = WSGIServer(('0.0.0.0', 80), app)
http_server.serve_forever()
```

This snippet creates an instance of the WSGI server provided by gevent and configures the instance to binds to all the available network interfaces ('0.0.0.0') on port 80.

Running the usual `python gevent_app.py` you have a production ready web service.

## Using HTTPS

What about service your service through HTTPS? Quite simple. You have just to configure gevent' WSGI to use the proper certificates. The certificates can be self-signed (the browser will identify your site as "Not Secure") or provided by one of the certified certification authorities.

```python
# file: gevent_app_https.py
from flask_app import app
from gevent.pywsgi import WSGIServer

http_server = WSGIServer(('0.0.0.0', 443), app, keyfile='privkey.pem', certfile='cacert.pem')
http_server.serve_forever()
```

Running the usual `python gevent_app_https.py` you have a production ready HTTPS web service.
