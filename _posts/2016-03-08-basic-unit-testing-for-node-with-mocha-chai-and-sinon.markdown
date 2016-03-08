---
layout: post
title:  "Basic Unit Testing for Node with Mocha, Chai and Sinon"
date:   2016-03-08 07:32:53
categories: javascript node moche chai sinon
author: Pere Pages
---

## Tools for Unit Testing Node

* Mocha
* Chai
* Sinon
* Gulp or Grunt

### Mocha and Chai

[Mocha](https://mochajs.org/)

>Mocha is a feature-rich JavaScript test framework running on Node.js and the browser, making asynchronous testing simple and fun. Mocha tests run serially, allowing for flexible and accurate reporting, while mapping uncaught exceptions to the correct test cases. Hosted on GitHub.

[Chai](http://chaijs.com/)

> Chai is a BDD / TDD assertion library for node and the browser that can be delightfully paired with any javascript testing framework.

```bash
npm install -g mocha
npm install chai
```

#### First Test

**test.js**

```javascript
'use strict';

// jshint expr: true

var chai = require('chai');
var epect = chai.expect;

chai.should();

function isEven(num) {
	return num % 2 === 0;
}

describe('isEven', function () {
	it('should return true when number is even', function () {
		isEven(4).should.be.true;
	});

	it('should return false when the number is odd', function () {
		isEven(3).should.be.false;
	});

	it('should return false when the number is odd (2)', function () {
		expect(isEven(3)).to.be.false;
	});
});
```

```bash
mocha test.js
```

#### Setup and Teardown

* beforeEach
* afterEach

```javascript
describe('testing add', function () {
	var num;

	beforeEach(function () {
		num = 5;
	});

	afterEach(function () {
		console.log('test run');
	});

	it('should be ten adding 5 to 5', function () {
		add(num,5).should.equal(10);
	});

	it('should be 12 adding 7 to 5', function () {
		add(num,7).should.equal(12);
	});
});
```

### More Mocha Features

* We can nest as many *describe* functions as we need.
* We can use *it.skip* for writing pending tests.
* We can run only one describe or only one it with *only*
* mocha run all test files in the same folder, by default *test* folder
* mocha can also watch for changes in the directory

```javascript
it.skip('should be yellow when it is green', function() {});
xit('should be yellow when it is green', function() {});
```

```javascript
describe.skip('numerical tests', function () {});
xdescribe('numerical tests', function () {});
```

```javascript
describe.only('numerical tests', function () {});
it.only('should result four when 2 + 2', function () {});
```

```bash
mocha -w
```

### Sinon

[Sinon](http://sinonjs.org/)

> Standalone test spies, stubs and mocks for JavaScript. No dependencies, works with any unit testing framework.

* spies
* stubs
* moc

#### Spies

Spies sound like what they do – they watch your functions and report back on how they are called. They generally avoid the violence and mayhem of a Hollywood spy, but depending on your application, this could vary.

An example without spy

```javascript
describe('student.dropClass', function () {
	it('should call the callback', function () {
		var called = false;
		function callback() {
			called = true;
		}

		student.dropClass(1,callback);

		expect(called).to.be.true;
	});
});
```

The same example WITH spy

```javascript
it('should call the callback and log to the console', function () {
	function onClassDropped() {
		console.log('onClassDropped was called');
	}

	var spy = sinon.spy(onClassDropped);

	student.dropClass(1,spy);
	spy.called.should.be.true;
});
```

```javascript
var student, schedule;

beforeEach(function () {
	student = {
		dropClass : function (classId, cb) {
			// do stuff
			if(!!cb.dropClass) {
				cb.dropClass();
			} else {
				cb();
			}
		}
	};

	schedule = {
		dropClass: function() {
			console.log('class dropped');
		}
	};
});

it('should call the callback even if it\'s a method of an object', function () {
	sinon.sply(schedule.dropClass);
	student.dropClass(1,schedule);
	schedule.dropClass.called.should.be.true;
});
```

#### Stubs

With stubs we spy on entire objects. And it lets us change the functionality that we need.

Stubs are more hands-on than spies (though they sound more useless, don’t they). With a stub, you will actually change how functions are called in your test. You don’t want to change the subject under test, thus changing the accuracy of your test. But you may want to test several ways that dependencies of your unit could be expected to act.

```javascript
beforeEach(function () {
	student = {
		dropClass : function (classId, cb) {
			// do stuff
			if(!!cb.dropClass) {
				cb.dropClass();
			} else {
				cb();
			}
		},
		addClass: function (schedule) {
			if (!schedule.classIsFull()) {
				// do stuff
				return true;
			} else {
				return false;
			}
		}
	};

	schedule = {
		dropClass: function() {
			console.log('class dropped');
		},
		classIsFull: function () {
			return true;
		}
	};
});

describe('student with stubs', function () {
	it('should call a stubed method', function () {
		var stub = sinon.stub(schedule);

		stub.dropClass(1, stub.dropClass);
		stub.dropClass.called.should.be.true;
	});

	it('should return true when the class is not full', function () {
		var stub = sinon.stub(schedule);
		stub.classIsFull.returns(false);
		var returnVal = student.addClass(stub);

		returnVal.should.be.true;
	});
});
```

#### Mocks

Mocks take the attributes of spies and stubs, smashes them together and changes the style a bit. A mock will both observe the calling of functions and verify that they were called in some specific way. And all this setup happens previous to calling your subject under test. After the call, mocks are simply asked if all went to plan.

```javascript
describe('student with mocks', function () {
	it('mocks schedule', function() {
		var mockObj = sinon.mock(schedule);
		var expectation = mockObj.expects('classIsFull').once();

		student.addClass(schedule);
		expectation.verify();
	});
});
``` 

### Gulp and Grunt

```bash
npm install --save-dev gulp gulp-mocha gulp-util
```

```javascript
'use strict';

var gulp = require('gulp');
var mocha = require('gulp-mocha');
var gutil = require('gulp-util');

gulp.task('mocha', function () {
	return gulp.src(['test/**/*.js'], {read:false})
	.pipe(mocha({reporter: 'list'}))
	.on('error',gutil.log);
});

gulp.task('watch-mocha', function () {
	gulp.run('mocha');
	gulp.watch(['./**/*.js', 'test/**/*.js'], ['mocha']);
});

gulp.task('default', ['watch-mocha']);
```

```bash
# when running the default value
gulp
```