# Week 2

## CRUD

* Create
* Read
* Update
* Delete

## Connect Mongo Shell to Atlas Cluster

Use the following command to connect to the m001 Atlas cluster:

```
mongo "mongodb://cluster0-shard-00-00-jxeqq.mongodb.net:27017,cluster0-shard-00-01-jxeqq.mongodb.net:27017,cluster0-shard-00-02-jxeqq.mongodb.net:27017/test?replicaSet=Cluster0-shard-0" --authenticationDatabase admin --ssl --username m001-student --password m001-mongodb-basics
```
Connecting the mongo shell to the Atlas cluster includes a few useful pieces of information:
#. A String of the primary and replica sets

```
"mongodb://cluster0-shard-00-00-jxeqq.mongodb.net:27017,cluster0-shard-00-01-jxeqq.mongodb.net:27017,cluster0-shard-00-02-jxeqq.mongodb.net:27017/test?replicaSet=Cluster0-shard-0"
```
#. An authentication database target

```
--authenticationDatabase admin
```

#. An encrypted connection type and the needed credentials
```
--ssl --username m001-student --password m001-mongodb-basics
```

## Create a Sandbox Cluster

Create a free Sandbox Cluster on Atlas [here](https://cloud.mongodb.com/links/registerForAtlas)
Don't forget to whitelist the necessary IP Adresses

## Connecting to your Sandbox

### Connecting Robo 3T to your Atlas Mongo Cluster is a little more complicated:

#### Connection
Specify a name and the connection to the primary set because you can only connect to a single shard at a time.

#### Authentication

Provide the username 'free' and the password that was setup for your free cluster

#### SSL
For the purposes of the course you can just use the self-signed SSL Credentials. Apparently this is generally a bad practice.

### Connecting directly to mongo shell

You can also just get the string from Cloud Atlas to connect to the cluster via mongo shell

## Load Data into the Sandbox Cluster

Navigate to folder where the file is located and then open connection to Atlas with mongo shell. Then run

```
load('loadMovieDetailsDataset.js') 
```

## Inserting Updating and Replacing

Inserting documents can be accomplished using either Compass or the `insertOne()` function.

For example:
```
use video
db.movieDetails.insertOne({title: "movie title", year: 1990})
```

You can also use `insertMany` to pass in an array of documents/json objects
* `insertMany` can be completed in an ordered (default) or unordered fashion
* in the case of ordered inserts, the insert will stop if an error occurs
* in the case of unorded, mongo will continues inserting documents into the database

## Deleting