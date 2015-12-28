# Mongo

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

```
mongo
```

```
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


```
db.foo.update(query,update,options);
//query -> which document
//update -> what change
//options -> one?many?upsert? Upsert means we can create a new document if it doesn't exist.
```

```

```