# Mongo

Mongo uses BSON format.

## Config file

+ Specific data directory
+ Logging verbosity
+ Log file name and location

```
mongod -f mongod.conf
```

**mongod.conf**
```
# where data files will reside
dbpath=/myfolder/db

# where the log file will be stored
logpath=/myfolder/mongo-server.log

# how verbose the server will be logging
verbose=VVVVV
```

## Basic Commands

```
mongo
```

```javascript
exit //exits cli
show dbs
use foo //use databasename
db //shows currents databse
help
show collections
db.foo.save({_id:1, value:'hello world'}) //save one object to foo collection
db.foo.find() //all documents in foo collection
db.foo.find().pretty() //prettifies the documents got from find collection
ObjectId() // returns a unique identifier any time. It is an object
ObjectId().getTimestamp()
```

## Rules

1. A document must have an **_id** field
2. A document size can be not above 16MB

Mongo accepts anything as an ID but an array

## Save vs Insert

When working with **_id**s, **insert** will prevent us of overwritting a value once is already created. Save, let us update a document once it's already existing. But in fact they are aweful for concurrency, so it's recomended to use **update** command.

## Update

Two concurrent updates will be executed one after the other. 

```javascript
db.foo.update(query,update,options);
//query -> which document
//update -> what change
//options -> one?many?upsert? Upsert means we can create a new document if it doesn't exist.
```

* $inc
* $set
* $rename

```javascript
db.a.save({_id:1, x:10});
db.a.update({_id:1}, {$inc: {x:1}}) //increments x by one
db.a.find()
// in the following two sentences we are able to touch properties of the document, but not overwritting it all
db.a.update({_id:1}, {$set:{y:3}});
db.a.update({_id:1}, {$inc:{x:1}});
//unsetting a property of the document
db.a.update({_id:1}, {$unset: {y: ''}}) // in this case '' it's arbitrary, any value would be correct
db.a.save({_id:1, Naem: 'bob'})
db.a.update({_id:1}, {$rename: {'Naem': 'Name'}})
```

## Array ops

It doesn't need to have an array to be able to run this commands:

* push
* addToSet
* pull
* pop

```javascript
db.a.update({_id:1}, {$push: {things: 'one'}})
db.a.update({_id:1}, {$addToSet: { things: 'four'}}) // only adds the element if does not exist already
db.a.update({_id:1}, {$pull : {things: 'three'}}) //remove all instances of the element 'three'
db.a.update({_id:1}, {$pop: {things: 1}}) //last element in the array
db.a.update({_id:1}, {$pop: {things: -1}}) //first element in the array
```

### Update multiple fields

```javascript
db.a.uptade({}, {$push: {things: 4}}, {multi:true});
db.a.update({things:2}, {$push: {things:42}}, {multi:true}) //update all the documtns that have an array things with the value 2
```

### Update only one record with the criteria

**That's why we also use the sort param**. So if there's more than one will pick the one

```
db.foo.findAndModifiy({
	quere: <document>,
	update: <document>,
	upsert: <boolean>, //create a new record if it doesn't exist
	remove: <boolean>,
	new: <boolean>, //return the new document or the old before the changes
	sort: <document>,
	fields: <document>
});
```

```javascript
var mod = {
        "query" : {
                "things" : 1
        },
        "update" : {
                "$set" : {
                        "touched" : true
                }
        },
        "sort" : {
                "_id" : -1 //sort by id in descending order
        }
};
db.a.findAndModifiy(mod);
mod.update.$set.touched = false;
mod.new = true; // now we are asking to get the modifiet version of the object
```