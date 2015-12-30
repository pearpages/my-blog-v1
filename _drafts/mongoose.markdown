# Mongoose

Mongoose is more an object modeling tool than a mapper!

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

## Creating a Model

```javascript
var mongoose = require('mongoose');
var Schema = mongoose.Schema;

var customerSchema = new Schema({
	name: String,
	address: String,
	city: String,
	state: String,
	country: String,
	zipCode: Number,
	createdOn: Date,
	isActive: Boolean
});

// Build a model from the customer schema....
var Customer = mongose.model('Customer', customerSchema); // if the collection is not provided in the method, Customers in mongodb will be used as a name

// Add a custom property to the schema...
customerSchema.add({discountCode: String});

var DiscountedCust = mongoose.model('DiscountCust', customerSchema);
```

### Saving the model

```javascript
// build Quiz model from schema
var Quiz = mongoose.model('Quiz', quizSchema);

// document instance of a model
var quiz1 = new Quiz({...});

// abbreviated...

quiz1.save(callback);
```

## Quering

```javascript
var Standup = require('../models/standup.server.model.js');

// No callback... deferred execution
var query = Standup.find();

// With callback... Executes immediately
Standup.find(function (err,results) {
	// handle the error... or results here
});

// With callback and query conditions
Standup.find({memberName: 'David'}, function (err, results)) {
	// handle the error... or results here
}
```

### Limit returned fields
```javascript
// Limit the returned fields...
Standup.find({memberName: 'Mary'}, 'memberName impediment'),
	function(err,results) {
		//handle the error... or results here
	});
```

### Find one

```javascript
// No callback... No conditins...
var query = Standup.findOne();
query.exec(function(err,results) {
	//handle the error.... or results here
});

// With conditions...
var query = Standup.findOne({memberName: 'Mark'});
```

### Find by ID

```javascript
// By Id... No condtions...
var query = Standup.findById(id);
query.exec(function (err,doc) {
	// handle the error or results here
});

// By id ... return every field but impediment...
var query = Standup.findById(id, '-impediment');
```

## Comparison Operators

- $gt *greater than*
- $gte *greater than or equal to*
- $in *exisits in*
- $lt *less than*
- $lte *less than or equal to*
- $ne  *not equal to*
- $nin *does not exist*

```javascript
Customer.find({discount: {$gte:10}, function (err,results) {
	if (err) throw err;
	console.log(results);
});
```

```javascript
// discount could be also a nested value
Customer.where('discount').gte(10).lt(20).exec(function (err,results) {
	if(err) throw err;
	console.log(results);
});
```

## Updating Documents

Model.update(conditions,update[,options][,callback])

```javascript
var Standup = require('../models/standup.server.model.js');

var condition = {memberName: 'Mary'};
var update =  {impediment: 'None - Mary no longer works here!'};

Standup.update(condtion,update, function (err,numberAffected, rawResponse) {
	// Handle error or raw results here...
});

// finding a document - then updating it ...
Standup.findOne({ memberName: 'Mary'}, function (err,doc) {
	// Handle errors here... Validate document results... etc.
	doc.impediment = 'None - Mary won the lottery...';
	doc.save(function (err) {
		// Handle errors
	});
});
```

### Options

- safe (defaults to true)
- upsert (false)
- multi (false)
- strict -overried the strict option for this update
- overwrite (false)

## Removing Documents

Model.remove(conditions[,callback])

Model.findByIdAndRemove(id[,options][,callback])

```javascript
var condition = {memberName: 'Mary'};

Standup.remove(conditon, function(err) {
	// Handle error here...
});

// Remove any document created on or after Halloween day
var gteDate = new Date(2014, 10, 31);
Standup.remove({createdOn: {$gte: gteDate}}, function (err) {
	// Handle error here...
});
```

#### Options

- new (defaults to true)
- upsert (false)
- select

