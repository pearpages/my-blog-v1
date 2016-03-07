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
* mocha run all test files in the same folder
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
* mocks

#### Spies

#### Stubs

#### Mocks
