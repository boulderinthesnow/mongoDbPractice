Part II - Challenges

Write the queries necessary to perform the following tasks

#Write the terminal command to start the mongo server
mongod
#Write the terminal command to enter a mongo shell
mongo
#Show all databases
show dbs
#Use the library database
use library
#Show all the collections inside the library database
db.library.find()
#Using the insert method Add an author with the name of "John", age of 37
db.library.insert({name:"John", age: "37"})
#Using the insert method Add another author with the name of "Jane", age of 42 and give her a property of books which is an empty array.
db.library.insert({name:"Jane", age: "42", books: []})

#Using the .save() method, find an author with an age greater than or equal to 42 and then change the age to 33. Finally, save that author.
var over41 = db.library.findOne({age : {$gt: "41"}})

over41.age = 33

db.library.save(over41)

#Find all of the authors
db.library.find({}, {name:1})

#Find an author with the name of John
db.library.find({name:"John"})

#Find all of the authors but limit the search to one

db.library.findOne({}, {name:1})

#Find an author whose name is not equal to "John" using the $ne operator
db.library.findOne( {name: { $ne: "John"} } )


#Update an author who has a name of "John" and change his name to "James" (without using the set method)
db.library.update({name:"John"},{name:"James"})


#Update an author named "James" and using the set operator, set his name back to John and age to 37.

db.library.update({name:"James"},{$set:{name:"John", age: 37}})

#Delete an author whose name is "John"
db.library.remove({name: "John"},1)

#Delete all of the authors
db.library.remove({})

#Create an author whose name is "John" and has an empty array of books
db.library.insert({name: "John", books: []})

#Update John and Using the $push operator add the string "Of Mice and Men" into the books array.

var johnData = db.library.findOne({name: "John"})

db.library.update(johnData, {$push: {book: "Of Mice and Men"}})
{

#Update John and using the $push and $each operators add the strings "Grapes of Wrath", "The Pearl", "East of Eden", "50 Shades of Gray" into the books array.
db.library.update(johnData, {$push: { book: {$each: ["Grapes of Wrath", "The Pearl", "East of Eden", "50 Shades of Gray"]}}})

#Sorry - John Steinbeck didn't write 50 Shades of Gray, using the $pull operator, remove that book from the array.
db.library.update({book: "50 Shades of Gray"}, {$pull: {book: "50 Shades of Gray"}})

#Finally, using the $in operator, update an author who has a book "Of Mice and Men" and "The Pearl" in the books array and change their name to "John Steinbeck"
var found = db.library.findOne({book: {$all: ["Of Mice and Men","The Pearl"]}})

found.name = "John Steinbeck"

