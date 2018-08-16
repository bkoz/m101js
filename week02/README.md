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

```
{ "title" : "P.S. I Love You" }
{ "title" : "Love Actually" }
{ "title" : "Shakespeare in Love" }
```
```
> db.movieDetails.find( {}, {title: 1, _id:0});
{ "title" : "Once Upon a Time in the West" }
{ "title" : "A Million Ways to Die in the West" }
{ "title" : "Wild Wild West" }
{ "title" : "West Side Story" }
{ "title" : "Slow West" }
{ "title" : "An American Tail: Fievel Goes West" }
{ "title" : "Red Rock West" }
{ "title" : "How the West Was Won" }
{ "title" : "Journey to the West" }
{ "title" : "West of Memphis" }
{ "title" : "Star Wars: Episode IV - A New Hope" }
{ "title" : "Star Wars: Episode V - The Empire Strikes Back" }
{ "title" : "Star Wars: Episode VI - Return of the Jedi" }
{ "title" : "Star Wars: Episode I - The Phantom Menace" }
{ "title" : "Star Wars: Episode III - Revenge of the Sith" }
{ "title" : "Star Trek" }
{ "title" : "Star Wars: Episode II - Attack of the Clones" }
{ "title" : "Star Trek Into Darkness" }
{ "title" : "Star Trek: First Contact" }
{ "title" : "Star Trek II: The Wrath of Khan" }
Type "it" for more
> db.movieDetails.find( {}, {title: 1});
{ "_id" : ObjectId("569190ca24de1e0ce2dfcd4f"), "title" : "Once Upon a Time in the West" }
{ "_id" : ObjectId("569190cb24de1e0ce2dfcd50"), "title" : "A Million Ways to Die in the West" }
{ "_id" : ObjectId("569190cb24de1e0ce2dfcd51"), "title" : "Wild Wild West" }
{ "_id" : ObjectId("569190cb24de1e0ce2dfcd52"), "title" : "West Side Story" }
{ "_id" : ObjectId("569190cb24de1e0ce2dfcd53"), "title" : "Slow West" }
{ "_id" : ObjectId("569190cb24de1e0ce2dfcd54"), "title" : "An American Tail: Fievel Goes West" }
{ "_id" : ObjectId("569190cc24de1e0ce2dfcd55"), "title" : "Red Rock West" }
{ "_id" : ObjectId("569190cc24de1e0ce2dfcd56"), "title" : "How the West Was Won" }
{ "_id" : ObjectId("569190cc24de1e0ce2dfcd57"), "title" : "Journey to the West" }
{ "_id" : ObjectId("569190cc24de1e0ce2dfcd58"), "title" : "West of Memphis" }
{ "_id" : ObjectId("569190cc24de1e0ce2dfcd59"), "title" : "Star Wars: Episode IV - A New Hope" }
{ "_id" : ObjectId("569190cc24de1e0ce2dfcd5a"), "title" : "Star Wars: Episode V - The Empire Strikes Back" }
{ "_id" : ObjectId("569190cc24de1e0ce2dfcd5b"), "title" : "Star Wars: Episode VI - Return of the Jedi" }
{ "_id" : ObjectId("569190cc24de1e0ce2dfcd5c"), "title" : "Star Wars: Episode I - The Phantom Menace" }
{ "_id" : ObjectId("569190cd24de1e0ce2dfcd5d"), "title" : "Star Wars: Episode III - Revenge of the Sith" }
{ "_id" : ObjectId("569190cd24de1e0ce2dfcd5e"), "title" : "Star Trek" }
{ "_id" : ObjectId("569190cd24de1e0ce2dfcd5f"), "title" : "Star Wars: Episode II - Attack of the Clones" }
{ "_id" : ObjectId("569190cd24de1e0ce2dfcd60"), "title" : "Star Trek Into Darkness" }
{ "_id" : ObjectId("569190cd24de1e0ce2dfcd61"), "title" : "Star Trek: First Contact" }
{ "_id" : ObjectId("569190cd24de1e0ce2dfcd62"), "title" : "Star Trek II: The Wrath of Khan" }
Type "it" for more

> db.movieDetails.find( {}, {title: 1, _id:0});
{ "title" : "Once Upon a Time in the West" }
{ "title" : "A Million Ways to Die in the West" }
{ "title" : "Wild Wild West" }
{ "title" : "West Side Story" }
{ "title" : "Slow West" }
{ "title" : "An American Tail: Fievel Goes West" }
{ "title" : "Red Rock West" }
{ "title" : "How the West Was Won" }
{ "title" : "Journey to the West" }
{ "title" : "West of Memphis" }
{ "title" : "Star Wars: Episode IV - A New Hope" }
{ "title" : "Star Wars: Episode V - The Empire Strikes Back" }
{ "title" : "Star Wars: Episode VI - Return of the Jedi" }
{ "title" : "Star Wars: Episode I - The Phantom Menace" }
{ "title" : "Star Wars: Episode III - Revenge of the Sith" }
{ "title" : "Star Trek" }
{ "title" : "Star Wars: Episode II - Attack of the Clones" }
{ "title" : "Star Trek Into Darkness" }
{ "title" : "Star Trek: First Contact" }
{ "title" : "Star Trek II: The Wrath of Khan" }
Type "it" for more
> db.movieDetails.find( {year: 1964}, {title: 1, _id:0});
{ "title" : "Dr. Strangelove or: How I Learned to Stop Worrying and Love the Bomb" }
{ "title" : "Before Hollywood, There Was Fort Lee, N.J." }
{ "title" : "FX 18" }
{ "title" : "Aa bakudan" }
{ "title" : "Mit csinált Felséged 3-tól 5-ig?" }
{ "title" : "Xie jian mu dan hong" }
{ "title" : "Mars na Drinu" }
{ "title" : "Heshtje që flet" }
{ "title" : "El rapto de T.T." }
{ "title" : "Abflug LH 646" }
{ "title" : "I Am Cuba" }
{ "title" : "Tintin et les oranges bleues" }
{ "title" : "KK 17" }
> db.movieDetails.find( {title: "Muppets from Space"}, {title: 1, _id:0});
{ "title" : "Muppets from Space" }
> 
```

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

???
```
updateOne({filter:value},{$set: plot});
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

#### 2

Write an update command that will remove the "tomato.consensus" field for all documents matching the following criteria:

The number of imdb votes is less than 10,000
The year for the movie is between 2010 and 2013 inclusive
The tomato.consensus field is null
How many documents required an update to eliminate a "tomato.consensus" field?

NOTE: There is a dump of the video database included in the handouts for the "Creating Documents" lesson. Use that data set to answer this question.