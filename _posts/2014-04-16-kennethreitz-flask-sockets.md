---
layout: post
title: "kennethreitz/flask-sockets"
date: "2014-04-16T19:27:00+05:00"
tags: 
  - python
  - flask
  - websocket
tumblr_url: "http://alixedi.tumblr.com/post/82884211028/kennethreitz-flask-sockets"
published: true
---

Check this out:

{% highlight Python %}
from flask import Flask
from flask_sockets import Sockets

app = Flask(__name__)
sockets = Sockets(app)

@sockets.route('/echo')
def echo_socket(ws):
    while True:
        message = ws.receive()
        ws.send(message)

@app.route('/')
def hello():
    return 'Hello World!'
{% endhighlight %}