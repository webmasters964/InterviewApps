 
 ## Install MongoDB 

 ```
 Download the MongoDB tarball from https://www.mongodb.com/download-center/community.
 ```

### Create a Data Directory

Create a /data/db directory

### Start the MongoDB Server

Open the terminal, navigate to the MongoDB installation folder, and issue the following command to start the MongoDB server.

```
./mongod --dbpath <data directory path>
```

### Start the MongoDB Client

```
./mongo.exe
```

### Syntax to create a database in MongoDB
```
use <database name>
```

### Create a database

To create a database named mydb, use this command:
> use mydb
Here is the output,
> use mydb
switched to db mydb

### Syntax to drop a database in MongoDB

db.dropDatabase()

use mydb
Here is the output,
> use mydb
switched to db mydb
>
> db.dropDatabase()
{ "ok" : 1 }

###  Display List of Databases
```
show dbs
show databases
```

### Display a List of Commands
```
db.help()
```


### Collections

MongoDB collections are similar to tables in RDBMS. 

```
db.person.insert({_id:100001,name:"Taanushree A S",age:10})

db.createCollection (<name>)

db.createCollection("person")

show collections

```

### Create a Capped Collection

To create a capped collection named student, use the following command.

```
db.createCollection("student",{capped: true,size:1000,max:2})

db.student.isCapped()

db.student.insert([{ "_id" : 10001, "name" : "Taanushree A S", 
"age" : 10 },{ "_id" : 10002, "name" : "Aruna M S", "age" : 14 }])
```


### Query a Capped Collection

```
db.student.find()

db.student.find()
{ "_id" : 10001, "name" : "Taanushree A S", "age" : 10 }
{ "_id" : 10002, "name" : "Aruna M S", "age" : 14 }

> the reverse order, use sort() and set the $natural parameter to -1

db.student.find().sort({$natural:-1})
{ "_id" : 10002, "name" : "Aruna M S", "age" : 14 }
{ "_id" : 10001, "name" : "Taanushree A S", "age" : 10 }

```
## Create Operations

###  Insert a Document and Insert Methods

> db.collection.insertOne Inserts a single document

MongoDB generates an _id field with an ObjectId value. The _id field act as he primary key.

> db.collection.insertMany Inserts multiple documents

Pass an array of documents to the insertMany() method to insert multiple documents

> db.collection.insert Inserts a single document or multiple documents

```
db.student.insert({_id:10003,name:"Anba V M",age:16})

db.student.find()
{ "_id" : 10002, "name" : "Aruna M S", "age" : 14 }
{ "_id" : 10003, "name" : "Anba V M", "age" : 16 }

> db.collection.insertOne()

db.person.insertOne({_id:1001,name:"Taanushree AS",age:10})
db.person.insertOne({name:"Aruna MS",age:14})

db.collection.insertMany()

db.person.insertMany([{_id:1003,name:"Anba V M",age:16},{_id:1004,name:"shobana",age:44}])

db.studentdetails.insertMany( [ {name: "John", result: "pass", marks: { english: 25, maths: 23, science: 25 }, grade: [ { class: "A", total: 73 } ] },{name: "James", result: "pass", marks: { english: 24, maths: 25, science: 25 }, grade: [ { class: "A", total: 74 } ] },{name: "James", result: "fail", marks: { english: 12, maths: 13, science: 15 }, grade: [ { class: "C", total: 40 } ] }])

```

## Read Operations

### Query Documents

You can specify query filters or criteria inside the find() method to query documents based on conditions.
and Specified Fields and the _id Field Only

```
db.collection.find()

db.studentdetails.find( { name: "John" }, { marks: 1, result: 1 } )

{ "_id" : ObjectId("5bae3ed2f10ab299920f0744"), "result" : "pass", "marks" : { "english" : 25, "maths" : 23, "science" : 25 } }
```
> Select All Documents in a collection

```
db.person.find({})
```

> Specify Equality Conditions

```
db.person.find({name:"shobana"})
```
> Specify Conditions Using Query Operator To select all documents from the collection person where age is greater than 10, here is the command

```
db.person.find({age:{$gt:10}})
```

>  Specify AND Conditions

you can specify conditions for more than one field.

```
db.person.find({ name:"shobana",age:{$gt:10}})
```

> Specify OR Conditions

You can use $or in a compound query to join each clause with a logical or 
conjunction.The operator $or selects the documents from the collection that match 
at least one of the selected conditions.

```
db.person.find( { $or: [ { name: "shobana" }, { age: { $eq: 20 } } ] } )
```


## Update Operations

> db.collection.updateOne To modify a single document

> db.collection.updateMany To modify multiple documents

> db.collection.replaceOne To replace the first matching document in the collection that matches the filter

```
db.collection.updateOne()
db.collection.updateMany()
db.collection.replaceOne()
```

> Update a Single Document
MongoDB provides modify operators to modify field values such as $set.

```
db.student.updateOne({name: "Joshi"},{$set:{"marks.english": 20}})
```

> Update Multiple Documents

Use the following code to update all documents in the student collection where result equals fail.

```
db.student.updateMany( { "result":"fail" }, { $set: { "marks.english": 20, marks.maths: 20 } })
```

> Replace a Document
You can replace the entire content of a document except the _id field by passing an entirely new document as the second argument to db.

```
collection.replaceOne()
db.student.replaceOne( { name: "John" }, {_id:1001,name:"John",marks:{english:36,maths:39},result:"pass"})
```


## Delete Operations

Delete operations allow us to delete documents from a collection.

> db.collection.deleteOne To delete a single document

> db.collection.deleteMany To delete multiple documents


```
db.collection.deleteOne()
db.collection.deleteMany()
```

>  Delete Only One Document That Matches a Condition

```
db.student.deleteOne({name: "John"})
```

> Delete All Documents That Match a Condition

```
db.student.deleteMany({name: "Jack"})
```

>  Delete All Documents from a Collection

```
db.student.deleteMany({})
```

### MongoDB Import and Export

> import data from the student.csv and  To work with the Mongo export command, start the mongod
process and open another command prompt to issue the Mongo export command.

```
C:\Program Files\MongoDB\Server\4.0\bin>
mongoimport --db student --collection students --type csv --headerline --file c:\Sample\student.csv

db.students.find()

C:\Program Files\MongoDB\Server\4.0\bin>
mongoexport --db student --collection students --out C:\Sample\student.json
```

## Embedded Documents in MongoDB

> Using embedded documents allows us to embed a document within another document.

```
{_id:1001,name:"John",marks:{english:35,maths:38},result:"pass"}

db.employee.insertMany([{_id:1001,name:"John",address:{previous:"123,1st Main",current:"234,2nd Main"},
unit:"Hadoop"}, {_id:1002,name:"Jack", address:{previous:"Cresent Street",current:"234,Bald Hill Street"},unit:"MongoDB"}, 
{_id:1003,name:"James", address:{previous:"Cresent Street",current:"234,Hill Street"},unit:"Spark"}])
```

### Embedded or Nested Document

```
{previous:"Cresent Street",current:"234,Bald Hill Street"}

db.employee.find( { address: { previous:"Cresent Street",current:"234,Bald Hill Street" }} )

db.employee.find( { address: { previous:"Cresent Street",current:"234,Bald Hill Street" }} )
{ "_id" : 1002, "name" : "Jack", "address" : { "previous" : "Cresent Street", "current" : "234,Bald Hill Street" }, "unit" : "MongoDB" }
```

### Query on a Nested Field

> use dot notation to query a field of the embedded document.

```
db.employee.find( { "address.previous": "Cresent Street" } )

db.employee.find( { "address.previous": "Cresent Street" } )
{ "_id" : 1002, "name" : "Jack", "address" : { "previous" : "Cresent Street", "current" : "234,Bald Hill Street" }, "unit" : "MongoDB" }
{ "_id" : 1003, "name" : "James", "address" : { "previous" : "Cresent Street", "current" : "234,Hill Street" }, "unit" : "Spark" }
```


### Match an Array

> To specify an equality condition on an array, you need to specify the exact array to match in the <value> of the query document 
{<field>:<value>}.

```
db.employeedetails.find( { projects: ["Hadoop", "MongoDB"] } )

{ "_id" : ObjectId("5badcbd5f10ab299920f072a"), "name" : "Smith", "projects" : [ "Hadoop", "MongoDB" ], "scores" : [ 22, 28, 26 ] }

```

> To query all documents where projects is an array that contains the string "MongoDB" as one of its elements,

```
db.employeedetails.find( { projects: "MongoDB" } )

{ "_id" : ObjectId("5badcbd5f10ab299920f0728"), "name" : "John", "projects" : [ "MongoDB", "Hadoop", "Spark" ], "scores" : [ 25, 28, 29 ] }
{ "_id" : ObjectId("5badcbd5f10ab299920f072a"), "name" : "Smith", "projects" : [ "Hadoop", "MongoDB" ], "scores" : [ 22, 28, 26 ] }

```

> Specify Query Operators => To query all documents where the scores field is an array that contains at 
least one element whose value is greater than 26 we can use the $gt operator.

```
db.employeedetails.find( { scores:{$gt:26} } )

{ "_id" : ObjectId("5badcbd5f10ab299920f0728"), "name" : "John", "projects" : [ "MongoDB", "Hadoop", "Spark" ], "scores" : [ 25, 28, 29 ] }
{ "_id" : ObjectId("5badcbd5f10ab299920f072a"), "name" : "Smith", "projects" : [ "Hadoop", "MongoDB" ], "scores" : [ 22, 28, 26 ] }
```

> Query an Array with Compound Filter Conditions on the Array Elements

```
db.employeedetails.find( { scores: { $gt: 20, $lt: 24 } } )

{ "_id" : ObjectId("5badcbd5f10ab299920f0729"), "name" : "James", "projects" : [ "Cassandra", "Spark" ], "scores" : [ 26, 24, 23 ] }
{ "_id" : ObjectId("5badcbd5f10ab299920f072a"), "name" : "Smith", "projects" : [ "Hadoop", "MongoDB" ], "scores" : [ 22, 28, 26 ] }

```
> $elemMatch operator => The $elemMatch operator allows us to specify multiple conditions on the array elements

```
db.employeedetails.find( { scores: { $elemMatch: { $gt: 23, $lt: 27 } } } )

{ "_id" : ObjectId("5badcbd5f10ab299920f0728"), "name" : "John", "projects" : [ "MongoDB", "Hadoop", "Spark" ], "scores" : [ 25, 28, 29 ] }
{ "_id" : ObjectId("5badcbd5f10ab299920f0729"), "name" : "James", "projects" : [ "Cassandra", "Spark" ], "scores" : [ 26, 24, 23 ] }
{ "_id" : ObjectId("5badcbd5f10ab299920f072a"), "name" : "Smith", "projects" : [ "Hadoop", "MongoDB" ], "scores" : [ 22, 28, 26 ] }
```

> Query an Array Element by Index Position > Use dot notation to query an array element by its index position.

```
db.employeedetails.find( { "scores.2": { $gt: 26 } } )

{ "_id" : ObjectId("5badcbd5f10ab299920f0728"), "name" : "John", "projects" : [ "MongoDB", "Hadoop", "Spark" ], "scores" : [ 25, 28, 29 ] }
```

> $size Operator => use the $size operator to query an array by number of elements. To select all documents where the projects array has two elements

```

db.employeedetails.find( { "projects": { $size: 2 } } )

{ "_id" : ObjectId("5badcbd5f10ab299920f0729"), "name" : "James", "projects" : [ "Cassandra", "Spark" ], "scores" : [ 26, 24, 23 ] }
{ "_id" : ObjectId("5badcbd5f10ab299920f072a"), "name" : "Smith", "projects" : [ "Hadoop", "MongoDB" ], "scores" : [ 22, 28, 26 ] }

```
>  $push Operator => use the $push operator to add a value to an array.

```
db.employeedetails.update({name:"James"},{$push:{Location: "US"}})

db.employeedetails.find({name:"James"})

{ "_id" : ObjectId("5c04bef3540e90478dd92f4e"), "name" : "James", "projects" : [ "Cassandra", "Spark" ], "scores" : [ 26, 24, 23 ], "Location" : [ "US" ] }
```

> To append multiple values to an array, use the $each operator.

```
db.employeedetails.update({name: "Smith"},{$push:{Location:{$each:["US","UK"]}}})

db.employeedetails.find({name:"Smith"})

{ "_id" : ObjectId("5c04bef3540e90478dd92f4f"), "name" : "Smith", "projects" : [ "Hadoop", "MongoDB" ], "scores" : [ 22, 28, 26 ], "Location" : [ "US", "UK" ] }
```

> The $addToSet operator to add a value to an array. $addToSet adds a value to an array only if a value is not present.

```
db.employeedetails.update( {name: "James"}, { $addToSet: {hobbies: [ "drawing", "dancing"]} })

{ "_id" : ObjectId("5c04bef3540e90478dd92f4e"), "name" : "James", "projects" : [ "Cassandra", "Spark" ], "scores" : [ 26, 24, 23 ], "Location" : [ "US" ],
 "hobbies" : [ [ "drawing", "dancing" ] ] }
```

> Use the $pop operator to remove the first or last element of an array. To remove the first element in the scores array.

```
db.employeedetails.update( {name: "James"},{ $pop: {scores:-1}})

 db.employeedetails.find({name:"James"}) { "_id" : ObjectId("5c04bef3540e90478dd92f4e"), "name" : "James", "projects" : [ "Cassandra", "Spark" ],
  "scores" : [ 24, 23 ], "Location" : [ "US" ], "hobbies" : [ [ "drawing", "dancing" ] ] }
```

> To remove the last element in the scores array

```
db.employeedetails.update( {name: "James"},{ $pop: {scores:1}})

db.employeedetails.find({name:"James"})

{ "_id" : ObjectId("5c04bef3540e90478dd92f4e"), "name" : "James", "projects" : [ "Cassandra", "Spark" ], "scores" : [ 24 ], 
"Location" : [ "US" ], "hobbies" : [ [ "drawing", "dancing" ] ] }
```

###  Document Nested in an Array 

> selects all documents in the array field marks that match the specified document

```
 db.studentmarks.insertMany([{name:"John",marks:[{class: "II", total: 489},{ class: "III", total: 490 }]},{name: "James",marks:[{class: "III", total: 469 },
 {class: "IV", total: 450}]},{name:"Jack",marks:[{class:"II", total: 489 },{ class: "III", total: 390}]},{name:"Smith", marks:[{class: "III", total: 489}, 
 {class: "IV", total: 490}]}, {name:"Joshi",marks:[{class: "II", total: 465}, { class: "III", total: 470}]}])

 db.studentmarks.find( { "marks": {class: "II", total: 489}})

{ "_id" : ObjectId("5bae10e6f10ab299920f073f"), "name" : "John", "marks" : [ { "class" : "II", "total" : 489 }, { "class" : "III", "total" : 490 } ] }
{ "_id" : ObjectId("5bae10e6f10ab299920f0741"), "name" : "Jack", "marks" : [ { "class" : "II", "total" : 489 }, { "class" : "III", "total" : 390 } ] }

```

### Field Embedded in an Array of Documents

>  use dot notation to query a field embedded in an array of documents.

```
db.studentmarks.find( { 'marks.total': { $lt: 400 } } )

{ "_id" : ObjectId("5bae10e6f10ab299920f0741"), "name" : "Jack", "marks" : [ { "class" : "II", "total" : 489 }, { "class" : "III", "total" : 390 } ] }


db.studentmarks.find( { 'marks.0.class': "II" } )

{ "_id" : ObjectId("5bae10e6f10ab299920f073f"), "name" : "John", "marks" : [ { "class" : "II", "total" : 489 }, { "class" : "III", "total" : 490 } ] }
{ "_id" : ObjectId("5bae10e6f10ab299920f0741"), "name" : "Jack", "marks" : [ { "class" : "II", "total" : 489 }, { "class" : "III", "total" : 390 } ] }
{ "_id" : ObjectId("5bae10e6f10ab299920f0743"), "name" : "Joshi", "marks" : [ { "class" : "II", "total" : 465 }, { "class" : "III", "total" : 470 } ] }
```


### 

```
```


### 

```
```

### 

```
```

### 

```
```
### 

```
```


### 

```
```

### 

```
```

### 

```
```

### 

```
```


### 

```
```

### 

```
```

### 

```
```
### 

```
```


### 

```
```

### 

```
```

### 

```
```

### 

```
```


### 

```
```

### 

```
```

### 

```
```
### 

```
```


### 

```
```

### 

```
```

### 

```
```

### 

```
```


### 

```
```

### 

```
```

### 

```
```
### 

```
```


### 

```
```

### 

```
```

### 

```
```

### 

```
```


### 

```
```

### 

```
```

### 

```
```
### 

```
```


### 

```
```

### 

```
```

### 

```
```

### 

```
```


### 

```
```

### 

```
```

### 

```
```
### 

```
```


### 

```
```

### 

```
```

### 

```
```

### 

```
```


### 

```
```

### 

```
```

### 

```
```
### 

```
```


### 

```
```

### 

```
```

### 

```
```

### 

```
```


### 

```
```

### 

```
```

### 

```
```
### 

```
```


### 

```
```

### 

```
```

### 

```
```