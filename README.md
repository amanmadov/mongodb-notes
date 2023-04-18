# MongoDB Notes



## Section 1: Introduction 



### What is MongoDB

Mongodb is a database system designed to store and manage large amounts of data efficiently. The company behind the database, which also offers a few other products, bears the same name. The name "Mongodb" is derived from the term "humongous," which reflects the database's capacity to store substantial amounts of data while still ensuring efficient data processing.

Unlike SQL-based databases that enforce a fixed schema on stored data, Mongodb offers schemaless flexibility. This flexibility allows for the storage of disparate data types in the same collection, which can grow with the application's evolving requirements. Mongodb also features nested data storage, which facilitates complex relationships between data, which are stored in a single document. This approach is more efficient than the complex joins required by SQL-based databases, where data must be retrieved from different tables.

Mongodb operates by converting JSON data to a binary format, which can be stored and queried more efficiently on the server. The database's strength lies in its flexibility and optimization for usability, which sets it apart from other database systems. This flexibility also contributes to Mongodb's performance efficiency, allowing for efficient data querying in the required format without complex data restructuring on the server.



### The Key MongoDB Characteristics

MongoDB is a so-called NoSQL solution because it follows a concept or philosophy that is opposite to that of SQL-based databases. Instead of normalizing data, which means storing it across multiple tables with clear schemas and using many relations, MongoDB stores data together in a document and does not force a schema on you. Therefore, MongoDB has no schemas. If there are multiple documents in the same collection, they can have different structures. This can lead to messy data, but it is still your responsibility as a developer to work with clean data and implement a solution that works. However, it gives you a lot of flexibility, which is always good.

You can use MongoDB for apps that may still evolve, where the exact data requirements are not yet set. You can get started and always add more information in a collection at a later time.

In MongoDB, you work with fewer relations. There are some relations, but with embedded documents, one core thing about MongoDB is that you have fewer tables, so fewer collections to connect. Instead, you store data together, which is where the efficiency comes from. Since data is stored together, when your application fetches data, it does not need to reach out to collection A, merge it with collection B, and then with collection C. Instead, it goes to collection A, and MongoDB has a very efficient querying mechanism behind the scenes so that it can go through all the data very fast when looking for a specific document. This will be super fast, and then it finds that document, and it's done. It doesn't need to do any merging most of the time. This is where the speed, performance, and flexibility come from, which speaks for itself as to why NoSQL solutions, and among them, most of all MongoDB, are popular for read-write heavy applications that store a lot of data, such as smart devices that send sensor data every second. For such applications, but also for building an online shop or a blog, MongoDB is an amazing solution due to the performance and flexibility it gives you.



### Understanding the MongoDB Ecosystem

MongoDB is a well-known database solution, provided by the company of the same name. In addition to MongoDB, the company offers several other products that make up the MongoDB ecosystem. The core feature of this ecosystem is the MongoDB database, which comes in both self-managed and enterprise solutions. The company also offers tools related to managing the database, which are more geared towards system administration and database administration tasks. Additionally, they provide a cloud solution for the database and a mobile solution that allows users to install MongoDB on mobile devices and work without an internet connection.

To provide a more user-friendly experience, MongoDB offers a graphical user interface called Compass, which allows users to connect to their database and view its contents using an intuitive interface. The company also offers other tools like BI connectors or MongoDB Charts for users who work in the field of data science. These tools help users connect various analytics tools if they need to.

Aside from the database, the company's relatively new offering, Stitch, is their serverless backend solution. Stitch is a decoupled service from the database that offers more than just data storage. It gives users a serverless query API, which allows them to query the database efficiently from within their client-side applications. Additionally, serverless functions allow users to execute code in the cloud on demand, making it possible to execute any JavaScript code in the cloud. MongoDB also offers database triggers, which listen to events in a database, such as document insertion, and execute a function in response. Finally, real-time sync is a feature built to synchronize a database in the cloud with a mobile offline-supporting database on mobile devices.

In summary, the MongoDB ecosystem includes various products and tools that cater to different needs. The core feature of this ecosystem is the MongoDB database, which comes in both self-managed and enterprise solutions. The company also offers tools related to managing the database, a cloud solution, a mobile solution, and a graphical user interface called Compass. Additionally, they provide Stitch, a serverless backend solution, with several features like serverless query API, serverless functions, database triggers, and real-time sync.





### Getting Started

```js
// Command to show existing databases
show dbs

// Command to connect to a database connected currently
use shop

// insertOne: Command to insert one document into a collection
db.products.insertOne({ "name": "Max"})

// We can omit the quotation marks around the key name
db.products.insertOne({ name: "Max"})

// Code expression to insert a new product into the "products" collection
db.products.insertOne({name: "A Book", price: 12.99})

/*

	{
		"acknowledged": true,
		"insertedId" : ObjectId("5ba3427e34cdfa88cd5c2a6a")
	}
 
*/

// find: Command to retrieve all documents from a collection
db.products.find()

// {"_id" : ObjectId("5ba3427e34cdfa88cd5c2a6a"), "name": "A Book", "price": 12.99 }

// pretty: Command to output the results in a prettier way
// Code expression to retrieve all products from the "products" collection in a pretty format
db.products.find().pretty()

/*

{
 "_id" : ObjectId("5ba3427e34cdfa88cd5c2a6a"),
 "name": "A Book",
 "price": 12.99
}

*/

db.products.insertOne({ "name": "T-shirt", "price": 9.99, "description": "This is a high-quality T-shirt" })

db.products.insertOne({ "name": "Computer", "price": 999.99, "details": { "CPU": "Intel i7", "memory": "32GB" } })
```



### Shell vs Drivers

- The course primarily works with the MongoDB shell to teach the different commands and ways of using them.

- The shell is a neutral ground for working with MongoDB, applicable to different programming languages.

- MongoDB drivers are packages installed for different programming languages to connect with the MongoDB server.

- The same commands used in the shell are used in the drivers, adjusted to the syntax of the language being used.

- The core features of the drivers are exactly equal to those of the shell.

- The syntax of the languages differs, but the general way of working with data remains the same.



### MongoDB + Clients: The Big Picture

In general there is the database, the data storage, and the files on a file system which hold your data in the end. There is also a MongoDB server, and on the backend server where you will write your code, you have drivers for different programming languages.

The drivers interact with the MongoDB server, which you started with the mongod command. The MongoDB server doesn't directly write data into files but talks to a storage engine, which you can replace with your favorite storage engine. However, the default one called Wired Tiger is an excellent storage engine that enables you to efficiently work with and store your data.

When you issue a query from your driver or shell, MongoDB forwards that information to the storage engine after doing some other things, and the storage engine stores it in files. Instead of using drivers, you can use the mongo shell to write all your queries. You can also use the mongo shell as a general playground and to administer your server, because that's not something your app would do. If you need to configure something, you can do this as an administrator from your company network through that shell, which is your direct access to the MongoDB server.

If you take a closer look at the data layer with the server, the storage engine, and the file system, you'll see that you need to differentiate between writing and reading from files, which is a bit slower, and writing and reading from memory, which is faster. The storage engine does both: it loads a chunk of data into memory and manages it so that the data you often use is in memory if possible. It also writes data in memory first so that this process is very fast, but then it stores data in the database files. In general, you need to be aware that you always talk to the MongoDB server, and behind that server, the server talks to the storage engine, which manages your data and stores it in files in the end but also in memory in between, so that you can work with the data in a very fast way. This is how the MongoDB server works behind the scenes, you could say.





## Section 2 : Understanding the Basics & CRUD Operations



### Understanding Databases, Collections & Documents

It's really important that you understand how databases collections and documents are related. In a mongodb world, you have one or more databases on your database server and each database can hold one or more collections, a collection would be a table in a SQL database. Now in that collection, you have these documents, multiple documents per collection and the documents are really the data pieces you're storing in your database. Now important, when working with mongodb, you will see that the databases, the collections and the documents are all automatically created for you, they are created implicitly when you start working with them, when you start storing data. That is really convenient, later in the course we'll also learn a way of explicitly creating new collections which allows you to configure them a bit further but this is a cool feature which makes getting started super simple.

Lets bring up that Mongo server again, connect through it through our shell and again see how we can store data in there and which kind of data that is.

In the terminal (on Mac), type **sudo mongo** to start a server. This will start up the mongodb server using the wired tiger storage engine. Now this is the server up and running and you need to keep this process running, so don't close this window, don't quit this process yet, as you can see it's now waiting for new connections on port 27017. By the way if you wanted to use a different port or you're facing issues with this one, you can use a different port and now I did quit the server by hitting control and c, you can use a different port by specifying** \--port **when starting up the server and then you can listen for that port.

So with that up and running, let's keep that up and running and open a new additional window in the terminal and in there, you can now run **mongo **without the d at the end to use the mongo shell and automatically connect to the up and running server. And now we can start running commands again and work with our database.

Now, before we run any commands, you might be wondering why I'm using the shell. When you build a real application using MongoDB, you won't use the shell for that. Instead, you'll use one of the MongoDB drivers depending on the programming language you're using.

On the documentation page, you can find an extensive list of all the drivers MongoDB offers for various programming languages. Depending on what you're building for, you need to choose your driver, follow the installation docs, and then embed it into your application code.

The shell allows us to write queries that are very similar to the queries in the different drivers. The shell is actually based on JavaScript, so it's extremely similar to Node.js. If you check out any article there, you can switch between the different languages. The interesting thing is the default always is the shell. These are the commands we'll write, but if you then switch to Python, for example, you'll see that it's pretty similar. We had "**insertOne**" in the shell written like this, and now in Python, it follows the Python naming standards, but it's still "**insertOne**" and is configured and used in the same way. This is true for all programming languages. It, of course, uses the syntax of that language and the best practices you should use for writing code in that language, but the way you use it, the way you pass data, and then you can configure it always are the same. This is why we use the shell here without deleting anything.

In the shell you can run "**show dbs**" to see which databases you have on this mongodb server. The default databases here simply exist to store configuration for this database server or for example the admin database will allow you to create users and roles and how people can use and interact with the database. We can switch to a database with the "**use**" command and you can even switch to databases which don't exist yet. When we switch to a newly created db and type "**show dbs**", we still don't see db we created. The reason for this is that this database does not get created before we start entering data in there, but if we do start entering data, it will be created automatically and implicitly, so we don't have to create the database in advance.

Now we get our flights database and in there, let's say we want to store some flight data. You can reference the database you're currently in, so in our case the flights database, with "**db**" and then you chain commands by typing a dot and then the command. Now important, make sure you've got the casing and the name in correct.



### JSON & BSON

1. MongoDB uses BSON (binary JSON) for storing data in the database.

2. JSON is what we write and see in MongoDB, but behind the scenes, it is converted to BSON by MongoDB driver.

3. BSON is more efficient than JSON in terms of storage space and speed.

4. BSON supports additional data types such as ObjectId, decimals, and large numbers.

5. MongoDB provides an automatically created unique ID for every document inserted, which is of type ObjectId and can be used for sorting.

6. We always work with data in JSON format but can omit quotation marks for field names if there is no whitespace.

7. Documents in the same collection do not need to have the same schema.

8. We can assign our own IDs instead of using the auto-generated ObjectId. But it has to be unique. Because duplicate IDs are not allowed in MongoDB.



```js
// assigning custom Id
db.flightData.insertOne({depAirport: "TXL", arrAirport: "LHR", _id: "txl-lhr-1"})
```



### CRUD & MongoDB

- CRUD operations are the core operations that one performs on their data in MongoDB, regardless of whether they are building an application, doing analytics, or administering a database.

- MongoDB offers different methods for CRUD operations such as insertOne, insertMany, find, findOne, updateOne, updateMany, replaceOne, deleteOne, and deleteMany.

- Filters are used in find and update methods to narrow down the data.



```js
db.flightData.deleteOne({departureAirport: "TXL"})
// { "acknowledged": true, "deleted Count": 1 }

db.flight Data.find().pretty()

// updating a document
// if there is a marker it will update its value if not it creates it
db.flightData.updateOne ({distance: 12000}, {$set: {marker: "delete"}})
// { "acknowledged": true, "matchedCount": 1, "modifiedCount" : 1 }

db.flightData.find().pretty()

// will update everything, no filter
db.flightData.updateOne({}, {$set: {marker: "delete"}})

// will delete everything that has marker:delete
db.flightData.deleteMany({marker: "delete"})
```





### Understanding insertMany()

- Use insertMany to insert the entire array of documents.

- InsertMany allows inserting multiple elements using an array.

- MongoDB automatically assigns IDs and maintains order.



```js
// will insert array of objects
db.flightData.insertMany([{obj1},{obj2},{obj3}])
```



### Finding Data with find() and findMany()

```js
// selects all the records with distance = 12000
db.flightData.find({distance: 12000}).pretty()

// selects all the records with distance > 10000
db.flightData.find({distance: {$gt: 10000}}).pretty()

// selects first matching record with  distance > 900
db.flightData.findOne({distance: {$gt: 900}}).pretty()
```



### update vs updateMany()

- The update operation can be done using updateOne or updateMany methods.

- To update a document, we can filter using a unique identifier like an objectId.

- To update a field in a document, we can use the $set operator.

- Using update without specifying whether it's updateOne or updateMany will update all matching documents.

- If we want to replace an entire document, we can use the replaceOne method.

- Using update to replace an entire document will override all existing key-value pairs in the document except for the unique identifier.



```js
// updates only delayed property
db.flightData.updateOne({_id: ObjectId("5b978ae64206ab")}, {$set: {delayed: true}})

// updates only delayed property
db.flightData.update({_id: ObjectId("5b978ae64206ab")}, {$set: {delayed: false}})

// be carefull: will replace entire document
db.flightData.updateOne ({_id: ObjectId("5b97882ce62da95ae64206ab")}, {delayed: false })
// WriteResult({ "nMatched" : 1, "nUpserted": 0, "nModified": 1 })

db.flightData.find().pretty()

/*

{"_id" : ObjectId("5b97882ce62da95ae64206ab"), "delayed" : false }

{
"_id" : ObjectId("5b97882ce62da95ae64206ac"),
"departureAirport" : "LHR",
"arrivalAirport" : "TXL",
"aircraft" : "Airbus A320",
"distance" : 950,
"intercontinental": false
}

*/


// replaces entire content, safer way to replace data
db.flightData.replaceOne(
{_id: ObjectId("5b97882ce62da95ae64206ab")}, 
{
	"departureAirport": "MUC",
	"arrivalAirport": "SFO",
	"aircraft": "Airbus A380",
	"distance": 12000,
	"intercontinental": true.
})

*/
```



### find() & Cursor Object

Using the <strong><code>find</code></strong> method returns a cursor with multiple documents, so the data is not immediately retrieved. The shell provides the first 20 documents by default, but we can control the output with <strong><code>forEach</code></strong> or <strong><code>toArray</code></strong>. The <strong><code>pretty</code></strong> method is available on the cursor to format the output nicely. It's important to note that cursors are not used with methods like <strong><code>insert</code></strong>, <strong><code>update</code></strong>, and <strong><code>delete</code></strong> because these methods manipulate data rather than fetch it.

- The find command does not return all documents in a collection but rather a cursor object with metadata, which can be used to cycle through the results.

- The shell happens to take the cursor and give us the first 20 documents by default

- Using toArray exhausts the cursor and returns an array of all the documents.

- Using forEach allows you to write code to execute on every element in the database, which is more efficient for large sets of data.

- The forEach method fetches the next document for every loop cycle, making it more efficient and less memory-intensive.

- Essentially, when using forEach, it only retrieves the next document during each loop cycle, making it efficient because it doesn't fetch all data at once and load it into memory. Instead, it retrieves data only when required, saving bandwidth and preventing excessive memory usage.



```js
// returns a cursor object with 20 documents
db.passengers.find().pretty()
// Type "it" for more

// returns all documents as an array
db.passengers.find().toArray()

// execute built in printjson method on cursor returned
db.passengers.find().forEach((p) => printjson(p))

// pretty function works only with cursor thats why it only works with find() function
// it will not work with findOne() because findOne() does not return cursor
```



### Understanding Projection

- Projection is a way to filter out unnecessary data from the MongoDB server before it's transferred to the application, which can save bandwidth and improve performance.

- Projection can be used with the find method by passing a second argument containing a document that specifies which key-value pairs to retrieve.

- The default behavior is to retrieve all fields, including the ID, but fields can be excluded by specifying them with a value of 0 in the projection document.

- Projection happens on the MongoDB server and is therefore more efficient than filtering data in the application.

- Important thing to understand here is that this filtering or this data transformation is happening

    on the mongodb server, so this happens before the data is shipped to you



```js
// selecting only name field
db.passengers.find({}, {name: 1}).pretty()

/*

{
    "_id" : ObjectId("5b978c66e62da95ae64206ad"),
    "name": "Max Schwarzmueller"
}

*/

// excluding the _id field
db.passengers.find({}, {name: 1, _id: 0}).pretty()

/*

{
    "name": "Max Schwarzmueller"
}

*/
```



### Embedded Documents & Arrays

- Embedded documents is a core feature of MongoDB.

- With embedded documents, you can have a field in your document that contains another document as its value, and you can have multiple levels of nesting, up to 100 levels in MongoDB.

- The overall document size has to be below 16 megabytes.

- Arrays are another kind of data you can store in MongoDB, and they can hold any data, including embedded documents.

- Arrays can hold lists of data in a document.



```js
// Embedded documents
// The status document is an embedded document within the flight data document
// Embedded documents are also called nested documents
db.flightData.updateMany({}, {$set: {status: {description: "on-time", lastUpdated: "1 hour ago"}}})
// { "acknowledged": true, "matchedCount": 2, "modified Count": 2 }

db.flight Data.find().pretty()
// Each flight data document has a child document (the status document).
// The status document can have its own nested documents.

/*

{
  "_id" : ObjectId("5b97882ce62da95ae64206ab"),
  "departureAirport" : "MUC",
  "arrivalAirport" : "SFO",
  "aircraft" : "Airbus A380",
  "distance" : 12000,
  "intercontinental": true,
  "status" : {
                "description": "on-time",
                 "lastUpdated" : "1 hour ago"
             }
}
{
  "_id" : ObjectId("5b97882ce62da95ae64206ac"),
  "departureAirport" : "LHR",
  "arrival Airport" : "TXL",
  "aircraft": "Airbus A320",
  "distance" : 950,
  "intercontinental": false,
  "status" : {
                "description": "on-time",
                "lastUpdated" : "1 hour ago"
              }
}             

*/

// Creating an embedded document within an embedded document in a collection document.
db.flightData.updateMany({}, {$set: {status: {description: "on-time", lastUpdated: "1 hour ago", details: {responsible: "John Wick"}}}})
```



- MongoDB can store arrays of data.

- Arrays are marked with square brackets and can contain any kind of data, including numbers, strings, and even documents.

- Arrays can be used in a document, as well as nested or embedded documents.

- Updating an array in MongoDB is done using the $set operator.



```js
// 
db.passengers.updateOne ({name: "Albert Twostone"}, {$set: {hobbies: ["sports", "cooking"]}})
// { "acknowledged": true, "matchedCount": 1, "modifiedCount": 1 }

db.passengers.find().pretty()

/*

{
    "_id" : ObjectId("5b978c66e62da95ae64206c0"),
    "name" : "Albert Twostone",
    "age" : 68,
    "hobbies" : [
                  "sports",
                  "cooking"
                ]
}

*/
```



- Embedded or nested documents and arrays provide flexibility in structuring data in MongoDB.

- Dot notation can be used to access nested fields in embedded documents.

- MongoDB is able to search for specific data in nested documents using dot notation and double quotation marks.

- Dot notation allows drilling into embedded documents in filters.



```js
// filtering on the array
db.passengers.findOne({name: "Albert Twostone"}).hobbies
// [ "sports", "cooking"]

db.passengers.find({hobbies: "sports"}).pretty()

/*

{
  "_id" : ObjectId("5b978c66e62da95ae64206c0"),
  "name": "Albert Twostone",
  "age" : 68,
  "hobbies" : [
              "sports",
              "cooking"
              ]
}

*/
```





```js
// filtering on the objects
db.flightData.find({"status.description": "on-time"}).pretty()

/*

{
"_id" : ObjectId("5b97882ce62da95ae64206ab"),
"departureAirport" : "MUC",
"arrivalAirport" : "SFO",
"aircraft" : "Airbus A380",
"distance" : 12000,
"intercontinental": true,
"status" : {
              "description" : "on-time",
              "lastUpdated" : "1 hour ago",
              "details" : {
                            "responsible" : "Max Schwarzmueller"
                           }
            }
}

*/

db.flightData.find({"status.details.responsible": "Max Schwarzmueller"}).pretty()
```

