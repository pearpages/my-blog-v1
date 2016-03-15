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

