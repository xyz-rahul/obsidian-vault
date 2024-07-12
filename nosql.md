
Not Only SQL 
non relational database

use key-value pair 


### Types of NoSQL Database:

- Document-based databases
- Key-value stores
- Column-oriented databases
- Graph-based databases


## Mongo db
non relational database
document-based db

default port 27017
# BSON 

BSON superset of JSON
JSON like structure with support for data types like  object, int, date, etc. 
[BSON Types - MongoDB Manual v7.0](https://www.mongodb.com/docs/manual/reference/bson-types/)

# CRUD
[MongoDB CRUD Operations | MongoDB](https://www.mongodb.com/resources/products/fundamentals/crud)

Certainly! Here are the basic CRUD (Create, Read, Update, Delete) operations in MongoDB, presented as commands:

### Create

- **Insert a document:**
  ```bash
  db.collection.insertOne(<document>)
  db.collection.insertMany([<document1>, <document2>, ...])
  ```

### Read

- **Find documents:**
  ```bash
  db.collection.find(<query>, <projection>)
  db.collection.findOne(<query>, <projection>)
  ```

- **Count documents:**
  ```bash
  db.collection.countDocuments(<query>)
  ```

- **Aggregate documents:**
  ```bash
  db.collection.aggregate([<pipeline>])
  ```

### Update

- **Update documents:**
  ```bash
  db.collection.updateOne(<filter>, <update>, <options>)
  db.collection.updateMany(<filter>, <update>, <options>)
  ```

- **Replace document:**
  ```bash
  db.collection.replaceOne(<filter>, <replacement>, <options>)
  ```

### Delete

- **Delete documents:**
  ```bash
  db.collection.deleteOne(<filter>)
  db.collection.deleteMany(<filter>)
  ```

- **Drop collection:**
  ```bash
  db.collection.drop()
  ```


[Query and Projection Operators - MongoDB Manual v7.0](https://www.mongodb.com/docs/manual/reference/operator/query/)
# Indexes

## What are indexes?

An index is a pointer to data in a collection
uses B-Tree data structure. 
uses binary search, instead of linear search, . 
faster read, slower write

### Creating Indexes
```bash
db.<collection>.createIndex({ 
  <field>: <type>, 
  <field2>: <type>, 
  …
})
```

Example:

```bash
db.trees.createIndex({ genus: -1 })
```

- `-1` indicates descending order.
- `+1` indicates ascending order.

### Dropping Indexes

To drop an index:
```bash
db.<collection>.dropIndex(<index>)
```

### Viewing Indexes
```bash
db.collection.getIndexes()
```

### Indexing Performance Insights via `.explain()`

When querying, you can use `.explain()` to get insights into how MongoDB executes a query and uses indexes.

# Operator

[Query and Projection Operators - MongoDB Manual v7.0](https://www.mongodb.com/docs/manual/reference/operator/query/)



# Schema validation
[Specify Validation With Query Operators - MongoDB Manual v7.0](https://www.mongodb.com/docs/manual/core/schema-validation/specify-query-expression-rules/)
```js
db.createCollection(<name>,
	{
	  '$jsonSchema': {
	    bsonType: 'object',
	    required: [ 'name', 'year', 'major', 'address' ],
	    properties: {
	      name: {
	        bsonType: 'string',
	        description: 'must be a string and is required'
	      },
	      year: {
	        bsonType: 'int',
	        minimum: 2017,
	        maximum: 3017,
	        description: 'must be an integer in [ 2017, 3017 ] and is required'
	      },
	      gpa: {
	        bsonType: [ 'double' ],
	        description: 'must be a double if the field exists'
	      }
	    }
	  }
	}
)

```


Questions

### Why embedded document/ why not join
[Embedding MongoDB Documents For Ease And Performance | MongoDB](https://www.mongodb.com/resources/products/fundamentals/embedded-mongodb)

## Projection Operators[](https://www.mongodb.com/docs/manual/reference/operator/query/#projection-operators "Permalink to this heading")

| Name                                                                                                                            | Description                                                                                                                                                                                                                                                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [`$`](https://www.mongodb.com/docs/manual/reference/operator/projection/positional/#mongodb-projection-proj.-)                  | Projects the first element in an array that matches the query condition.                                                                                                                                                                                                                                                               |
| [`$elemMatch`](https://www.mongodb.com/docs/manual/reference/operator/projection/elemMatch/#mongodb-projection-proj.-elemMatch) | Projects the first element in an array that matches the specified [`$elemMatch`](https://www.mongodb.com/docs/manual/reference/operator/projection/elemMatch/#mongodb-projection-proj.-elemMatch) condition.                                                                                                                           |
| [`$meta`](https://www.mongodb.com/docs/manual/reference/operator/aggregation/meta/#mongodb-expression-exp.-meta)                | Projects the document's score assigned during the `$text` operation.<br><br>## NOTE<br><br>`$text` provides text query capabilities for self-managed (non-Atlas) deployments. For data hosted on MongoDB Atlas, MongoDB offers an improved full-text query solution, [Atlas Search.](https://www.mongodb.com/docs/atlas/atlas-search/) |
| [`$slice`](https://www.mongodb.com/docs/manual/reference/operator/projection/slice/#mongodb-projection-proj.-slice)             | Limits the number of elements projected from an array. Supports skip and limit slices.                                                                                                                                                                                                                                                 |


### Why does Profiler use in MongoDB

why mongo over sql

###  What does MongoDB not being ACID compliant really mean?

https://stackoverflow.com/a/17499088
It's actually not correct that MongoDB is not ACID-compliant. On the contrary, MongoDB is ACID-compilant **_at the document level_**.

Any update to a single document is

- Atomic: it either fully completes or it does not
- Consistent: no reader will see a "partially applied" update
- Isolated: again, no reader will see a "dirty" read
- Durable: (with the appropriate write concern)

What MongoDB doesn't have is **_transactions_** -- that is, multiple-document updates that can be rolled back and are ACID-compliant.

###  How can you achieve primary key - foreign key relationships in MongoDB?
do it using embedded document or at application level 

###  Does MongoDB pushes the writes to disk immediately or lazily?
lazily

###  What is a covered query in MongoDB?
[Query Optimization - MongoDB Manual v7.0](https://www.mongodb.com/docs/manual/core/query-optimization/#:~:text=A%20covered%20query%20is%20a,are%20in%20the%20same%20index.)

A covered query is a query that can be satisfied entirely using an index and does not have to examine any documents. An index [covers](https://www.mongodb.com/docs/manual/core/query-optimization/#std-label-indexes-covered-queries) a query when all of the following apply:

- all the fields in the [query](https://www.mongodb.com/docs/manual/tutorial/query-documents/#std-label-read-operations-query-document) are part of an index, **and**
    
- all the fields returned in the results are in the same index.


### How can you achieve transaction and locking in MongoDB?

###  What is oplog?

###  Is MongoDB schema-less?
by default yes but shema can be enforced at document level

### When to Redis or MongoDB?
### What are three primary concerns when choosing a data management system?
cap theorem
### Q15: How to find MongoDB records where array field is not empty? ☆☆☆☆

[](https://gist.github.com/paulfranco/7436965eb26b9bb1310736f2bd6b6905#q15-how-to-find-mongodb-records-where-array-field-is-not-empty-)

**Answer:** Consider some variants:

```js
collection.find({ pictures: { $exists: true, $not: { $size: 0 } } }) 
collection.find({ pictures: { $exists: true, $ne: [] } })
collection.find({ pictures: { $gt: [] } }) // since MongoDB 2.6 
collection.find({'pictures.0': {$exists: true}}); // beware if performance is important - it'll do a full collection scan
```

**Source:** _stackoverflow.com_


# remaingin
aggregation
data modeling

Data modeling
	organising data
	links/relation between entitites