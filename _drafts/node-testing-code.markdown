---
layout: post
title: "Testing Node Code"
categories: javascript nodejs testing
date:  2016-03-23 19:12:12
---

#### Contents
{:.no_toc}
* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

* Business Logic
* Exceptions
* Finding Edge Cases
* IO & Async Operations
* Mocks
* Promises
* Test Coverage

## Testing Business Logic

* To arrange
* To Act
* To Assert

Tests don't have to be 'DRY'. They can have duplication of code if it helps to understand better the test.

## Testing Errors

```javascript
var Student = require("../Student"),
    Course = require('../Course'),
    chai = require('chai'),
    should = chai.should(),
    expect = chai.expect;

describe('unregisterStudent', function() {
    var courseName = 'Introduction to Awesomenewss',
    courseCode = "AWE 101",
    courseDescription = "This course will make you awesome!";

    it("should throw an error if we try to remove a student that is not in the class", function() {
        var course = Course.create(courseName, courseCode, courseDescription);

        expect(function() {
            course.unregisterStudent("asdf");
        }).to.throw();
    });
});
```

## Finding Edge Cases

## IO and Asynchronous Operations

## Testing with Mocks

## Testing Promises

Install the library ```bluebird```

```bash
npm install --save-dev bluebird
```

## Test Coverage


