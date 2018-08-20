# Week 2 homework 
## Assignments

### hw2-1

Which of the choices below is the title of a movie from the year 2013 that is rated PG-13 and won no awards? Please query the video.movieDetails collection to find the answer.

NOTE: There is a dump of the video database included in the handouts for the "Creating Documents" lesson. Use that data set to answer this question.

Restore 

```
$ cd creating_documents
$ mongorestore dump
$ use video
```

```
> db.movieDetails.find( { year:2013, rated:"PG-13", "awards.wins":{ $eq:0 } } ).pretty();
```

### hw2-2

Using the video.movieDetails collection, which of the queries below would produce output documents that resemble the following. Check all that apply.

NOTE: We are not asking you to consider specifically which documents would be output from the queries below, but rather what fields the output documents would contain.

Only queries where filter contained {_id:0}


### hw2-3

Using the video.movieDetails collection, how many movies list "Sweden" second in the the list of countries.

NOTE: There is a dump of the video database included in the handouts for the "Creating Documents" lesson. Use that data set to answer this question.

```
> db.movieDetails.find({"countries.1":"Sweden"}).count();
6
>
```

### hw2-4

How many documents in our video.movieDetails collection list just the following two genres: "Comedy" and "Crime" with "Comedy" listed first.

NOTE: There is a dump of the video database included in the handouts for the "Creating Documents" lesson. Use that data set to answer this question.

```
> db.movieDetails.find( { genres: ["Comedy", "Crime"] } ).count()
20
>
```

### hw2-5

As a follow up to the previous question, how many documents in the video.movieDetails collection list both "Comedy" and "Crime" as genres regardless of how many other genres are listed?

NOTE: There is a dump of the video database included in the handouts for the "Creating Documents" lesson. Use that data set to answer this question.

Could it be just adding the $all operator?
```
> db.movieDetails.find( { genres: { $all: ["Comedy", "Crime"] } } ).count()
56
> 
```

### hw2-6

Suppose you wish to update the value of the "plot" field for one document in our "movieDetails" collection to correct a typo. Which of the following update operators and modifiers would you need to use to do this?

Looks like ```$set``` should do it.

```
> db.names.insert({first:"Bob",last:"Kozdemba",nick:"Koz"})
WriteResult({ "nInserted" : 1 })
> db.names.find()
{ "_id" : ObjectId("5b756e5399f193a64b7b88bc"), "first" : "Bob", "last" : "Kozdemba", "nick" : "Koz" }
> db.names.updateMany({first:"Bob"},{$set:{nick:"BK"}})
{ "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }
> db.names.find()
{ "_id" : ObjectId("5b756e5399f193a64b7b88bc"), "first" : "Bob", "last" : "Kozdemba", "nick" : "BK" }
> 
```

### Challenge problems

#### 1

Suppose our movie details documents are structured so that rather than contain an awards field that looks like this:
```
"awards" : {
    "wins" : 56,
    "nominations" : 86,
    "text" : "Won 2 Oscars. Another 56 wins and 86 nominations."
}
```
they are structured with an awards field as follows:
```
"awards" : {
    "oscars" : [
        {"award": "bestAnimatedFeature", "result": "won"},
        {"award": "bestMusic", "result": "won"},
        {"award": "bestPicture", "result": "nominated"},
        {"award": "bestSoundEditing", "result": "nominated"},
        {"award": "bestScreenplay", "result": "nominated"}
    ],
    "wins" : 56,
    "nominations" : 86,
    "text" : "Won 2 Oscars. Another 56 wins and 86 nominations."
}
```
What query would we use in the Mongo shell to return all movies in the video.movieDetails collection that either won or were nominated for a best picture Oscar? You may assume that an award will appear in the oscars array only if the movie won or was nominated. You will probably want to create a little sample data for yourself in order to work this problem.

HINT: For this question we are looking for the simplest query that will work. This problem has a very straightforward solution, but you will need to extrapolate a little from some of the information presented in the "Reading Documents" lesson.

Inserted the following:
```
use video;
db.oscars.insertOne({name: "movie01", "awards" : {
    "oscars" : [
        {"award": "bestAnimatedFeature", "result": "won"},
        {"award": "bestMusic", "result": "won"},
        {"award": "bestSoundEditing", "result": "nominated"},
        {"award": "bestScreenplay", "result": "nominated"}
    ],
    "wins" : 56,
    "nominations" : 86,
    "text" : "Won 2 Oscars. Another 56 wins and 86 nominations."
} } );
db.oscars.insertOne({name: "movie02", "awards" : {
    "oscars" : [
        {"award": "bestAnimatedFeature", "result": "won"},
        {"award": "bestMusic", "result": "won"},
        {"award": "bestSoundEditing", "result": "nominated"},
        {"award": "bestScreenplay", "result": "nominated"}
    ],
    "wins" : 56,
    "nominations" : 86,
    "text" : "Won 2 Oscars. Another 56 wins and 86 nominations."
} } );
db.oscars.insertOne({name: "movie03", "awards" : {
    "oscars" : [
        {"award": "bestAnimatedFeature", "result": "nominated"},
        {"award": "bestMusic", "result": "nominated"},
        {"award": "bestPicture", "result": "won"},
        {"award": "bestSoundEditing", "result": "nominated"},
        {"award": "bestScreenplay", "result": "nominated"}
    ],
    "wins" : 56,
    "nominations" : 86,
    "text" : "Won 1 Oscars. Another 56 wins and 86 nominations."
} } );
db.oscars.insertOne({name: "movie04", "awards" : {
    "oscars" : [
        {"award": "bestAnimatedFeature", "result": "nominated"},
        {"award": "bestMusic", "result": "nominated"},
        {"award": "bestPicture", "result": "won"},
        {"award": "bestSoundEditing", "result": "won"},
        {"award": "bestScreenplay", "result": "nominated"}
    ],
    "wins" : 56,
    "nominations" : 86,
    "text" : "Won 2 Oscars. Another 56 wins and 86 nominations."
} } );
db.oscars.insertOne({name: "movie05", "awards" : {
    "oscars" : [
        {"award": "bestAnimatedFeature", "result": "nominated"},
        {"award": "bestMusic", "result": "nominated"},
        {"award": "bestPicture", "result": "nominated"},
        {"award": "bestSoundEditing", "result": "nominated"},
        {"award": "bestScreenplay", "result": "won"}
    ],
    "wins" : 56,
    "nominations" : 86,
    "text" : "Won 1 Oscars. Another 56 wins and 86 nominations."
} } );
```
A start
```
db.oscars.find({"awards.oscars":[{ $all: {"award": "bestPicture","result": "won"}}]}).count()
db.oscars.find({"awards":{"oscars":{$all:[{"award":"bestPicture","result":"won"}]}}}).count()
```

#### 2

Write an update command that will remove the "tomato.consensus" field for all documents matching the following criteria:

The number of imdb votes is less than 10,000
The year for the movie is between 2010 and 2013 inclusive
The tomato.consensus field is null
How many documents required an update to eliminate a "tomato.consensus" field?

NOTE: There is a dump of the video database included in the handouts for the "Creating Documents" lesson. Use that data set to answer this question.

A start
```
> db.movieDetails.find({"imdb.votes": {$lt: 10000}, year: {$gte: 2010, $lte: 2013} , "tomato.consensus":null }).count()
```
