librato-node is a client for Node.js and Librato (http://librato.com/)

[![Build Status](https://travis-ci.org/goodeggs/librato-node.png)](https://travis-ci.org/goodeggs/librato-node)

Getting Started
---------------

### Install

    $ npm install librato-node

### Setup

Once `librato.start` is called, a worker will send aggregated stats to librato once every 60 seconds.

``` coffee
librato = require 'librato-node'
librato.configure email: 'foo@example.com', token: 'ABC123'
librato.start()

process.once 'exit', ->
  librato.stop()
```

### Increment

Use `librato.increment` to track counts in librato.  On each flush, the incremented total for that period will be sent.

``` coffee
librato = require 'librato-node'

librato.increment 'foo'

### Timing

Use `librato.timing` to track durations in librato.  On each flush, the count, max, min and 90th percentile mean for that period will be sent.

``` coffee
librato = require 'librato-node'

librato.measure 'foo', 500

### Express

librato-node includes Express middleware to log the request count and response times for your app.  It also works in other Connect-based apps.

``` coffee
express = require 'express'
librato = require 'librato-node'

app = express()
app.use librato.middleware()
```

The key names the middleware uses are configurable by passing an options hash with `requestCountKey` and `responseTimeKey` values into `librato.middleware`.

Contributing
-------------

```
$ git clone https://github.com/goodeggs/librato-node && cd librato-node
$ npm install
$ npm test
```

