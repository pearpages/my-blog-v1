---
layout: post
title: "Building a simple node API"
categories: javascript node api
date:  2016-03-12 19:40:22
author: Pere Pages
---

#### Contents

{:.no_toc}
* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

## Some quick examples

### With Node and http module

```javascript
var http = require('http');

http.createServer(function (req,res) {
    res.writeHead(200, {
        'Content-Type': 'text/plain'
    });
    res.end('Hello World\n');
}).listen(3000,'127.0.0.1');

console.log('Server running at http://localhost:3000/');
```

```javascript
var http = require('http');

http.createServer(function (req,res) {
    res.writeHead(200, {
        'Content-Type': 'application/json'
    });
    res.end('{"id":1,"name": "Pere Pages"}');
}).listen(3000,'127.0.0.1');

console.log('Server running at http://localhost:3000/');
```

### With Express

```javascript
var express = require('express');

var app = express();

app
.get('/', function (req,res) {
    res.send('Hello World!');
})
.get('/json', function (req,res) {
    res.json({"hello":"world"});
});

var server = app.listen(3000, function () {
    console.log('Server running at http://127.0.0.1:3000/');
});
```

## Tools

### Nodemon

Node monitor

```bash
sudo npm install -g nodemon
```

### lodash

Utility class, before everybody was using underscore.

```bash
npm install --save lodash
```

```javascript
var _ = require('lodash');
```

### body-parser

This module helps dealing with cookies and bodies.

> The bodyParser object exposes various factories to create middlewares. All middlewares will populate the req.body property with the parsed body, or an empty object ({}) if there was no body to parse (or an error was returned).

```bash
npm install --save body-parser
```

### Creating a npm script

```json
{
  "scripts": {
"start":"nodemon index.js"
  }
}
```

## Dummy API

**index.js**

```javascript
var express = require('express');
var app = express();

var bodyParser = require('body-parser');

// middleware
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));

var cats = require('./cat.js')(app);

var server = app.listen(3000, function() {
    console.log('Server running at http://127.0.0.1:3000/');
});

```

**cat.js**

```javascript
var _ = require('lodash');

module.exports = function(app) {

    _cats = [];

    /* Create */
    app.post('/cat', function(req, res) {
        _cats.push(req.body);
        res.json({ info: 'cat created successfully' });
    });

    /* Read */
    app.get('/cat', function(req, res) {
        res.send(_cats);
    });

    app.get('/cat/:id', function(req, res) {
        res.send(_.find(_cats, { name: req.params.id }));
    });

    /* Update */
    app.put('/cat/:id', function(req,res) {
        var index = _.findIndex(_cats, {name:req.params.id});
        _.merge(_cats[index], req.body);
        res.json({info: 'cat updated successfully'});
    });

    /* Delete */
    app.delete('/cat/:id', function (req,res) {
        _.remove(_cats, function (cat) {
            return cat.name === req.params.id;
        });
        res.json({info: 'cat removed successfully'});
    });
};

```

## Using Mongo

### Adding Mongo

**Installing Mongoose**

```bash
npm install --save mongoose
```

**index.js, include mongoose**
```javascript
var express = require('express');
var app = express();

var bodyParser = require('body-parser');

// HERE!!!!!!!!!!!!
var mongoose = require('mongoose');
mongoose.connect('mongodb://localhost/cats');

// middleware
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));

var cats = require('./cat.js')(app);

var server = app.listen(3000, function() {
    console.log('Server running at http://127.0.0.1:3000/');
});

```

#### Mongoose Model Example

**cat_model.js**

```javascript
var mongoose = require('mongoose');

var catSchema = mongoose.Schema({
    name: String,
    age: Number,
    type: String
});

module.exports = mongoose.model('Cat', catSchema);
```

**cat_routes.js**

```javascript
var _ = require('lodash');
var Cat = require('./cat_model.js');

module.exports = function(app) {

    /* Create */
    app.post('/cat', function(req, res) {
        var newCat = new Cat(req.body);
        newCat.save(function(err) {
            if(err) {
                res.json({info: 'error during cat create', error: err});
            } else {
                res.json({info: 'cat created successfully'});
            }
        });
    });

    /* Read */
    app.get('/cat', function(req, res) {
        Cat.find(function(err, cats) {
            if (err) {
                res.json({info: 'error during finding cats', error: err});
            } else {
                res.json({info: 'cats found successfully', data: cats});
            }
        });
    });

    app.get('/cat/:id', function(req, res) {
        Cat.findById(req.params.id, function(err,cat) {
            if (err) {
                res.json({info: 'error during finding cat', error: err});
            } else {
                if (cat) {
                    res.json({info: 'cat found successfully', data: cat});
                } else {
                    res.json({info: 'cat not found'});
                }
            }
        });
    });

    /* Update */
    app.put('/cat/:id', function(req,res) {
        Cat.findById(req.params.id, function(err,cat) {
            if (err) {
                res.json({info: 'error during finding cat', error: err});
            } else {
                if (cat) {
                    _.merge(cat,req.body);
                    cat.save(function (err) {
                        if(err) {
                            res.json({info: 'error during cat update', error: err});
                        } else {
                            res.json({info: 'cat updated successfully'});
                        }
                    });
                } else {
                    res.json({info: 'cat not found'});
                }
            }
        });
    });

    /* Delete */
    app.delete('/cat/:id', function (req,res) {
        Cat.findByIdAndRemove(req.params.id, function (err) {
            if (err) {
                res.json({info: 'error during remove cat', error: err});
            } else {
                res.json({info: 'cat removed successfully'});
            }
        });
    });
};

```

### Working with Mongo

#### RoboMongo

> Native and cross-platform MongoDB manager

[RoboMongo](https://robomongo.org/)

#### Examples

```
show dbs
use cats
show collections
db.cats.find(); // find all
db.cats.find({"name":"Pere"}); // find cats with name 'Pere'
```

### Nodejs Shines At

NodeJs works very well as a middleware, a "traffic controller".

### Adding Additional Servers

#### Run servers in the background

```bash
npm install -g forever
forever list
```

#### "Request" Module

Let us do requests from one server to another. "Think of it as a node version of **Postman**".

```bash
npm install --save request
```

#### Check for open ports

```bash
sudo lsof -i -n -P | grep LISTEN
```

#### Using npm for scripts

```json
{
  "name": "server",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "forever start ./servers/cat.js | forever start ./servers/dog.js | nodemon ./servers/pet.js"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "body-parser": "^1.15.0",
    "express": "^4.13.4",
    "lodash": "^4.5.1",
    "mongoose": "^4.4.6",
    "request": "^2.69.0"
  }
}
```

## Working Asynchronously

### Processing the requests Asynchronously

Async it is similar to $q in angular but for the backend side.

```bash
npm install --save async
```

## Adding a Cache

### Implementing a Redis Cache

> Redis is an open source (BSD licensed), in-memory data structure store, used as database, cache and message broker. It supports data structures such as strings, hashes, lists, sets, sorted sets with range queries, bitmaps, hyperloglogs and geospatial indexes with radius queries. 

#### Installing Redis on Windows

```bash
# Installing Chocolatey
@powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
```

```bash
choco install redis-64
```

```bash
npm install --save redis
```

#### Usage

```javascript
var r = require('request').defaults({ json: true });

var async = require('async');
var redis = require('redis');
var client = redis.createClient(6379, '127.0.0.1');

module.exports = function(app) {

    app.get('/ping', function (req, res) {
        res.json({pong: Date.now()});
    });

    /* Read */
    app.get('/pets', function(req, res) {
        async.parallel({
            cat: function (callback) {
                r({ uri: 'http://localhost:3000/cat' }, function (error, response, body) {
                    if (error) {
                        callback({ service: 'cat', error: error });
                        return;
                    }
                    if (!error && response.statusCode === 200) {
                        callback(null, body);
                    } else {
                        callback(response.statusCode);
                    }
                });
            },
            dog: function (callback) {
                client.get('http://localhost:3001/dog', function (error,dog) {
                    if (error) {throw error;}
                    if (dog) {
                        callback(null, JSON.parse(dog));
                    } else {
                        r({uri: 'http://localhost:3001/dog'}, function (error,response,body) {
                            if (error) {
                                callback({service: 'dog', error: error});
                                return;
                            }
                            if (!error && response.statusCode === 200) {
                                callback(null,body);
                                //client.set('http://localhost:3001/dog', JSON.stringify(body.data), function (error) {
                                client.setex('http://localhost:3001/dog', 10, JSON.stringify(body.data), function (error) {
                                    if (error) { throw error;}
                                });
                            } else {
                                callback(response.statusCode);
                            }
                        });
                    }
                })
            }
        },
        function (error,results) {
            res.json({
                error: error,
                results: results
            });
        });
    });

};

```


