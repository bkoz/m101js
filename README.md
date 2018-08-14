# m101js
MongoDB Node.js Course

## Notes

### Week 2 CRUD
#### Create

db.collection.insertOne({"key1":"value", "key2":"value"});
              insertMany([{doc1},{doc2}]);

ordered:false = Insertions will continue if an error is encountered(i.e. duplicate keys, etc)

db.collection.drop()

db.collection.update - addressed later 

_id field, ObjectId (12-bytes) = date(4), MACaddr(3), pid(2), counter(3)

#### Read

db.collection.find({field:"value", field2:"value"}).pretty()
                                   .count()
Equality
Nested docs must be quoted "doc.subdoc":value
Arrays - (writers":["value1","value2"])
values are AND'd and order matters
(actors:"Jeff Bridges") - will match all docs that contain this value in the "actors" array

Specific element - actors.0:"value" - finds only element 0 with the given value

Cursors - find returns a cursor
docs are returned in batches. Type "it" in the shell to get the next batch
var c = db.collection.find();
var doc = function() {return c.hasNext() ? c.next : null;}
c.objsLeftInBatch();

Projection - 2nd arg to find
How to limit the fields returned in a results doc
find({field1:value,{field2:,_id:0}).pretty - search for field1 but only field 2 is returned, also exclude _id field
To exclude a field, specify field:0

Comparison Operators - See docs
Element 
and - Need to specify multiple criteria on the same field.
regex - find({awards.text:{$regex: /^Won\s.*/}}) - Returns entries that begin with the word "Won" followed by a space and any number of chars after that.
Arrays - 

