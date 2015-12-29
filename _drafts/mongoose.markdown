# Mongoose

## Why?

* Validation
* Defaults
* Query builder
* Pseudo-joins
* Life-cycle management

## Mongo Hosting Options

* Microsoft Azure
* mongolab
* Compose

## Robomongo

Shell-centric cross-platform MongoDB management tool

## Mongoose Schema

```javascript
var mongoose = require('mongoose');
var Schema = mongoose.Schema;

var customerSchema = new Schema({
	name: String,
	address: String,
	city: String,
	state: String,
	country: String,
	zipCode: String,
	createdOn: Date,
	isActive: Boolean
});

var simpleSchema = new Schema({fieldName: schemaType});
```

```javascript
var mongoose = require('mongoose');
var Schema = mongoose.Schema;

// child adress schema...
var addressSchema = new Schema({
	type: String,
	street: String,
	city: String,
	state: String,
	country: String,
	postalCode: Number
});

// parent customer schema...
var customerScema = new Schema({
	name: {
		first: String,
		last: String
	},
	address: [addressSchema],
	createdOn: {type: Date, default: Date.now},
	isActive: {type: Boolean, default: true}
});
```

```javascript
var mongoose = require('mongoose');
var Schema = mongoose.Schema;

// pre-define sub-documents...
var subCategory = {
	name: String,
	description: String,
	isActive: Boolean
	};

var subAnswers = {
	answerText: String,
	isCorrect: Boolean,
	displayOrder: Number
};

var subQuestions = {
	questionType: String,
	questionText: String,
	answers: [ subAnswers ]
};

// Define main document schema...
var quizSchema = new Schema({
	name: String,
	description: String,
	categories: [ subCategory],
	questions: [ subQuestions ]
});
}
```

### Allowed Data Types

- String
- Number
- Date (Object)
- Buffer (Object)
- Mixed (Object)
- ObjectId (Object)
- Array (Array -Object-)