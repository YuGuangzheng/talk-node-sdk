Talk-Node-Sdk
======

[![NPM version][npm-image]][npm-url]
[![Build Status][travis-image]][travis-url]

# Usage

```coffeescript
talk = require 'talk-node-sdk'

config =
  appToken: 'yyyyyy-ffff-gggg-hhhh-aaaaaaaaaaa'
  apiHost: 'http://localhost:7001'

talk.init(config)

# Initialize a webhook reciever service
app = require('express')()
service = talk.service app, prefix: '/'

# Initialize a worker
worker = talk.worker
  interval: 100
  runner: (task) ->  # Call the runner when the task executed

# OR
# Use the cron pattern to define the interval of ticks
worker = talk.worker
  cron: '* * * * * *'
  runner: (task)->

## An 'execute' event will be emitted when a task executed
worker.on 'execute', (task) ->

## Bind the worker to the service
worker.watch service

# Initialize another client
client = talk.client(token)

```

# TODO
- Use cron to execute worker

# Events

- `*` listen to all event
- `message.create` message create event

# Apis

# ChangeLog

## 0.4.7
- Use the cron pattern to define interval of ticks

## 0.4.1
- execute jobs parallelly, set the default concurrency to 5

## 0.4.0
- add worker in sdk
- use promise
- remove `express` dependency

## 0.3.0
- move event emitter to service
- reconnect the api server when the discover api failed

## 0.2.0

- bump to new version

## 0.1.1

- Use methods from `discover` api
- Add support for 'GET', 'PUT', 'POST', 'DELETE' methods
- Replace url params with the correct value

[npm-url]: https://npmjs.org/package/talk-node-sdk
[npm-image]: http://img.shields.io/npm/v/talk-node-sdk.svg

[travis-url]: https://travis-ci.org/jianliaoim/talk-node-sdk
[travis-image]: http://img.shields.io/travis/jianliaoim/talk-node-sdk.svg
