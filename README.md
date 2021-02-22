# mongo-basic
## mongo shell
1. Connect

```mongo "mongodb+srv://<username>:<password>@<cluster>.mongodb.net/admin"```
2. find( )
```
show dbs
use database_name
show collections

db.movies.find()
db.movies.count()

db.movies.find({title: "Night at the Museum"}).pretty()
db.movies.find({year: 2006}).pretty()
db.movies.find({year: 2006}).count()
db.movies.find({genre: "Action, Adventure, Comedy"}).pretty()

db.zips.find()
db.zips.find({"state": "NY"})
db.zips.find({"state": "NY"}).count()
db.zips.find({"state": "NY", "city": "ALBANY"})
db.zips.find({"state": "NY", "city": "ALBANY"}).pretty()
```
3. Insert
```
db.todos.insertOne({ todo: "Learn MongoDB", isComplete: false, dueDate: Date(), importance: 1 })
db.todos.insertMany([{ todo: "Become MongoDB Ninja", isComplete: false, dueDate: Date(), importance: 3 }, {todo: "Learn the lyrics to I AM A BANANA", isComplete: false, dueDate: Date() , importance: 10}]);
```
4. Update
```
db.todos.updateOne({ todo: "Use MongoDB Compass" }, { $set: { isComplete: true } })
```
5. Delete
```
db.todos.deleteOne({ todo: "Learn the lyrics to I AM A BANANA" })
db.todos.deleteMany({ isComplete: true })
db.todos.deleteMany({ importance : {$gte : 2} })
db.todos.deleteMany({})
```
6. Query Operator

= 
```
db.mycol.find({"by":"tutorials point"}).pretty()
```
< 
```
db.mycol.find({"likes":{$lt:50}}).pretty()
```
<= 
```
db.mycol.find({"likes":{$lte:50}}).pretty()
```
> 
```
db.mycol.find({"likes":{$gt:50}}).pretty()
```
>=
```
db.mycol.find({"likes":{$gte:50}}).pretty()
```
!=
```
db.mycol.find({"likes":{$ne:50}}).pretty()
```

7. AND 
```
// được viết bởi 'tutorials point'và có title là 'MongoDB Overview'
db.mycol.find({$and:[{"by":"tutorials point"},{"title": "MongoDB Overview"}]}).pretty()

db.movies.find({$and: [{genre: "Action, Adventure, Comedy"}, {year: 2006}]}).pretty()

db.movies.find({$and: [{genre: "Action, Adventure, Comedy"}, {year: 2006}, {viewerRating: 5.4}]}).pretty()

db.movies.find({$and: [{genre: "Action, Adventure, Comedy"}, {year: 2006}, {viewerRating: {$gte: 6} }]}).pretty()
```
8. OR
```
// được viết bởi 'tutorials point' hoặc có title là 'MongoDB Overview'
db.mycol.find({$or:[{"by":"tutorials point"},{"title": "MongoDB Overview"}]}).pretty()

// Document mà có các like > 10 và có title là hoặc 'MongoDB Overview' hoặc bởi là 'tutorials point'.
db.mycol.find({"likes": {$gt:10}, $or: [{"by": "tutorials point"},
   {"title": "MongoDB Overview"}]}).pretty()
```
9. NOR
```
// Documents có tên không phải là "Radhika" và họ không phải là "Christopher"
db.empDetails.find(
	{
		$nor:[
			{"First_Name": "Radhika"},
			{"Last_Name": "Christopher"}
		]
	}
).pretty()
```
10. NOT
```
db.empDetails.find( { "Age": { $not: { $gt: "25" } } } )
```
11. Sort
```
//1 tức là sắp xếp tăng dần theo field1
db.player.find().sort({'name':1})

db.movies.find({$and: [{genre: "Action, Adventure, Comedy"}, {year: 2006}, {viewerRating: {$gte: 6} }]}, {title:1, plot:1, viewerRating:1}).sort({viewerRating: 1}).pretty()

db.movies.find({$and: [{genre: "Action, Adventure, Comedy"}, {year: 2006}, {viewerRating: {$gte: 6} }]}, {title:1, plot:1, viewerRating:1}).sort({viewerRating: -1}).pretty()

// -1 sắp xếp giảm dần
db.player.find().sort({'country':1, 'age':-1})
```
12. Display
```
db.todos.find({ $or: [{ importance: { $lte: 3 } }, { isComplete: false }] }, { todo: 1, _id: 0 })

db.movies.find({$and: [{genre: "Action, Adventure, Comedy"}, {year: 2006}, {viewerRating: {$gte: 6} }]}, {title:1}).pretty()

db.movies.find({$and: [{genre: "Action, Adventure, Comedy"}, {year: 2006}, {viewerRating: {$gte: 6} }]}, {title:1, plot:1}).pretty()
```

13. Search in array
```
db.movies.find({cast:{$in:["Ben Stiller"]}}).pretty()

db.movies.find({cast:{$in:["Ben Stiller"]}}, {title:1}).sort({viewerRating:1})

db.movies.find({cast:{$in:["Ben Stiller"]}}, {title:1, viewerRating:1}).sort({viewerRating:1})

db.movies.find({cast:{$in:["Ben Stiller"]}}, {title:1, viewerRating:1}).sort({viewerRating:-1})

db.movies.find({$and : [{cast:{$in:["Ben Stiller"]}},{viewerVotes: {$gte:1000}}]}, {title:1, viewerRating:1}).sort({viewerRating:-1})


```
