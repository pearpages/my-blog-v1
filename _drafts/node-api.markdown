---
layout: post
title: "title"
categories: category1 category2
date:  2015-05-26 19:40:22
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

## Nodemon

Node monitor

```bash
sudo npm install -g nodemon
```

## lodash

Utility class, before everybody was using underscore.

```bash
npm install --save lodash
```

```javascript
var _ = require('lodash');
```

## body-parser

This module helps dealing with cookies and bodies.

> The bodyParser object exposes various factories to create middlewares. All middlewares will populate the req.body property with the parsed body, or an empty object ({}) if there was no body to parse (or an error was returned).

```bash
npm install --save body-parser
```

## Creating a npm script

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