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

## Creating a npm script
```json
{
  "scripts": {
"start":"nodemon index.js"
  }
}
```