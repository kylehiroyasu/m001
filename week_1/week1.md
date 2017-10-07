# Week 1

## Grading

 * Quizzes: are ungraded
 * Labs/Homework: ~50% of grade
 * Final Exam: ~50% of grade
 * Lowest Lab/Homework grade is dropped from final grade

## Connecting to Atlas with Compass

Here are the sign in credentials to the class cluster:
> Hostname: cluster0-shard-00-00-jxeqq.mongodb.net
> Username: m001-student
> Password: m001-mongodb-basics
> Replica Set Name: Cluster0-shard-0
> Read Preference: Primary Preferred


## Databases, Documents, Collections

The basic structure of a mongoDB database is the following:

* database
 * collection
  * documents

In the mongo shell you can choose the database you want to use (for example `thisDatabase`) with the following command:
`use thisDatabase`
And then proceed to access collections inside the database using the `db` keyword like so:
`db.thisCollection.find({})`

* Note that the following are true:
 * A database can store multiple collections
 * Each database and collection name combination defines a namespace (ex: dbName.collectionName)
 * Documents are stored in collections

## Datatypes

MongoDB is able to support many of the most common data types such as:

* integers
* floats
* doubles
* strings
* null
* dates/timestamps
* and many others!

In addition MongoDB also supports data type which generally aren't supported in relational databases such as:
* arrays
* objects
* geospatial mappings

What also sets MongoDB apart from relational databases is that collections and document schemas/key value pairs are not strictly defined by type.
This means that the schema of documents inside a single collection can be changed/evolve and that for a given key:value you/your application can write the value as any datatype.

## JSON

Much of MongoDBs interaction/design is modelled around [JSON Objects/Structures](http://www.json.org/) so it is important to have at least a basic understanding of notation.