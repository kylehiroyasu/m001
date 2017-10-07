# Week 3

## Query Operators

> For which CRUD operations can one use the query operators we will discuss in this chapter?
> * They can be used for any of the CRUD operations

### Comparison Operators

* `gt`: greater than
* `lt`: less than
* `gte`/`lte`: greater than or equal/ less than or equal

Example using them together on the same field:

db.movieDetails.find({runtime: {$gte: 90, $lte: 120}}, {_id:0, title:1, runtime:1})

Using equality filters across mutliple fields:

db.movieDetails.find({runtime: {$gte: 180}, "tomato.meter": {$gte: 95}}, {_id:0, title:1, runtime:1})

Using the not equal filter

db.movieDetails.find({rated: {$ne: "UNRATED"}}

 * NOTE: this include not only "UNRATED" films but also films without a rating field

Using in an array

db.movieDetails.find({rated: {$ne: {$in: ["UNRATED", "PG-13"]}}}

> Using the $in operator, filter the video.movieDetails collection to determine how many movies list either
> "Ethan Coen" or "Joel Coen" among their writers. Your filter should match all movies that list either of
> the Coen brothers as writers regardless of how many other writers are also listed. Select the number of
> movies matching this filter from the choices below.

```
use video
db.movieDetails.find({writers: { $in: ["Ethan Coen", "Joel Coen"]}}).count()

```

### Element Operators

* `$exists`: search if key does or does not exist, can also use `null` which will find all docs with value set to null or where the key does not exist
* `$type`: can specify the type of the values the documents should have

examples:
```
db.movieDetails.find({mpaaRating: {$exists:false}})
db.movieDetails.find({"tomato.consensus":null})
db.movieDetails.find({viewerRating: {$type: "double"})

```

> Connect to our class Atlas cluster from the mongo shell or Compass and answer the following question.
> How many documents in the `100YWeatherSmall.data` collection do NOT contain the key `atmosphericPressureChange`.

```
use 100YWeatherSmall
db.data.find({atmosphericPressureChange:{$exists:false}})

```

###  Logical Operators

* `$or`: can be use to or on an array of multiple field/keys

`db.movieDetails.find({$or: [{"tomato.meter": {$gt: 95}}, {"metacritic": {$gt:88}}]})`

* `$and`: similar behavior to or, but same as doing a normal find query

```
// same results
db.movieDetails.find({$and: [{"tomato.meter": {$gt: 95}}, {"metacritic": {$gt: 88}}]})
db.movieDetails.find({"tomato.meter": {$gt: 95}, "metacritic": {$gt: 88})

//more useful example
db.movieDetails.find({$and: [{"metacritc": {$ne:null}},{"metacritic": {$exists:true}}]})

```

> Connect to our class Atlas cluster from the mongo shell or Compass and view the `ships.shipwrecks`
> collection. In this collection, `watlev` describes the water level at the shipwreck site and `depth`
> describes how far below sea level the ship rests. How many documents in the `ships.shipwrecks`
> collection match either of the following criteria: `watlev` equal to "always dry" or `depth` equal to 0.


```
use ships

db.shipwrecks.find({$or : [{watlev:"always dry"}, {depth: 0}]}).count()

```

## $all

* `$all` : all the values must be included in the keys array
* specified as the value of a given key instead including key value pairs


```
db.movieDetails.find({genres: {$all: ["Comedy", "Crime", "Drama"]}})

```

> Connect to our class Atlas cluster from the mongo shell or Compass and view the `100YWeatherSmall.data`
> collection. The `sections` field in this collection identifies supplementary readings available in a
> given document by a three-character code. How many documents list: "AG1", "MD1", and "OA1" among the
> codes in their `sections` array. Your count should include all documents that include these three codes
> regardless of what other codes are also listed.

```
use 100YWeatherSmall
db.data.find({sections: {$all: ["AG1", "MD1", "OA1"]}}).count()
```

## $size

* `$size`: This can help you query for arrays of a certain size

```
db.movieDetails.find({countries: {$size:1}})
```

## $elemMatch

* allows you to query fields where value is an array of objects on the per object level, instead of all values in the array.

```
use video

// matching on a single element in the array which has this information
db.movieDetails.find({boxOffice: {$elemMatch: {"country":"Germany", "revenue": {$gt:17}}}})

//VS searching all elements in the array for the same criteria
db.movieDetails.find({"boxOffice.country":"Germany", "boxOffice.revenue": {$gt:17}})
```

> In the M001 class Atlas cluster you will find a database added just for this week of the course.
> It is called `results`. Within this database you will find two collections: `surveys` and `scores`.
> Documents in the `results.surveys` collection have the following schema.

```
{_id: ObjectId("5964e8e5f0df64e7bc2d7373"),
 results: [{product: "abc", score: 10}, {product: "xyz", score: 9}]}
```
> The field called `results` that has an array as its value. This array contains survey results for
> products and lists the product name and the survey score for each product.
> 
> How many documents in the `results.surveys` collection contain a score of 7 for the product, "abc"?

```
use results

db.surveys.find({results: {$elemMatch : {"product":"abc", "score": 7}}}).count()
```

## $regex

* can be used to search for text patterns using a regex

```
db.movieDetails.find({})
db.movieDetails.find({"awards.text": {$regex: /^Won .* /}})
```