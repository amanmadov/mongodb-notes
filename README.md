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



<br><br>

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
db.flightData.updateOne({_id: ObjectId("5b97882ce62da95ae64206ab")}, {$set: {delayed: true}})

// updates only delayed property
db.flightData.update({_id: ObjectId("5b97882ce62da95ae64206ab")}, {$set: {delayed: false}})

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
db.flightData.replaceOne
(
    {_id: ObjectId("5b97882ce62da95ae64206ab")}, 
    {
        "departureAirport": "MUC",
        "arrivalAirport": "SFO",
        "aircraft": "Airbus A380",
        "distance": 12000,
        "intercontinental": true.
    }
)

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
    "status" :  {
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
    "status" :  {
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
db.passengers.updateOne ({name: "John Doe"}, {$set: {hobbies: ["sports","cooking"]}})
// { "acknowledged": true, "matchedCount": 1, "modifiedCount": 1 }

db.passengers.find().pretty()

/*
    {
        "_id" : ObjectId("5b978c66e62da95ae64206c0"),
        "name" : "John Doe",
        "age" : 68,
        "hobbies" : ["sports", "cooking"]
    }
*/
```



- Embedded or nested documents and arrays provide flexibility in structuring data in MongoDB.

- Dot notation can be used to access nested fields in embedded documents.

- MongoDB is able to search for specific data in nested documents using dot notation and double quotation marks.

- Dot notation allows drilling into embedded documents in filters.



```js
// filtering on the array
db.passengers.findOne({name: "John Doe"}).hobbies
// [ "sports", "cooking"]

db.passengers.find({hobbies: "sports"}).pretty()

/*
    {
        "_id" : ObjectId("5b978c66e62da95ae64206c0"),
        "name": "John Doe",
        "age" : 68,
        "hobbies" : ["sports", "cooking"]
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





### Section Summary

- A database can hold multiple collections and each collection can hold multiple documents

- Databases and collections are created lazily, meaning only when a document is inserted or when you need a specific database or collection

- A document cannot be directly inserted into a database, it must be part of a collection

- Documents have a certain structure, including a unique ID called \_id, and can have embedded documents, arrays, texts, and numbers

- CRUD operations (create, read, update, delete) are important in working with a database

- MongoDB offers multiple CRUD operations for a single document and bulk actions

- Find method returns a cursor, not a list of documents, which allows for manually going through the documents and saving bandwidth

- Filters and operators can be used to narrow down the set of data found, with special operators identified by the dollar sign

- Projection can be used to restrict the amount of fields per document

<br><br>

## Section 3: Schemas & Relations



### Resetting the database

To get rid of your data, you can simply load the database you want to get rid of (`use databaseName`) and then execute `db.dropDatabase()`. Similarly, you could get rid of a single collection in a database via `db.myCollection.drop()`.



### Why do we use Schemas?

- The decisions you make about how to structure your data will impact how you use MongoDB

- Document schemas are important to define in order to structure and organize your data in MongoDB

- MongoDB offers a variety of data types like text, numbers, and dates that are important to understand in order to store the right data for your application

- Understanding relations between documents is also important for reflecting different entities in your application

- Schema validation is important for ensuring that incoming data meets your requirements and can be performed in MongoDB.

- MongoDB is schemaless, meaning it doesn't enforce any schemas, and documents can look different within the same collection.

- A schema refers to the structure of one document, including its fields and value types.

- While it's possible to mix different schemas, having some kind of schema is usually beneficial for developers to efficiently work with their data.

- In the example of an online shop, it's in the developer's interest to have a schema for products, such as fields for name and price, so that the data can be properly accessed and used in application code.



```js
use shop
// switched to db shop

db.products.insertOne({name: "A book", price: 12.99})

/*
    {
        "acknowledged": true,
        "insertedId" : ObjectId("5b98c5204d01c52e1637a98e")
    }
*/

db.products.insertOne({title: "T-Shirt", seller: {name: "Max", age: 29}})

/*
    {
        "acknowledged": true,
        "insertedId" : ObjectId("5b98c54b4d01c52e1637a98f")
    }
*/

db.products.find().pretty()

/*
    {
        "_id" : ObjectId("5b98c5204d01c52e1637a98t"),
        "name": "A book",
        "price": 12.99
    }
    {
        "_id" : ObjectId("5b98c54b4d01c52e1637a98f"),
        "title": "T-Shirt",
        "seller" :  {
                        "name": "Max",
                        "age" : 29
                    }
    }
*/
```



### Structuring Documents

- Two approaches to storing data in MongoDB: chaotic approach (different documents with different structures in the same collection) or structured approach (all entries have exactly the same schema)

- The realistic approach is a mixture of the two, where there is a core structure that every document fulfills (e.g., name and price), but extra information is added to some documents

- This approach allows for flexibility in storing data, while still having some structure that is necessary for the application's use case

- The middle ground is seen as the most realistic option, where there is a general schema that includes some core fields that exist on every document, but where there is also room for flexibility to store extra information.

- In SQL-like approach all documents have exactly the same fields.



```js
// Delete everything on the products collections
db.products.deleteMany({})

// insert product with same schema (mongodbish approach)
db.products.InsertOne({name: "A book", price: 12.99})
db.products.insertOne({name: "A T-Shirt", price: 20.99})

// insert product with same schema (sqlish approach)
db.products.InsertOne({name: "A book", price: 12.99, details: null})
db.products.insertOne({name: "A T-Shirt", price: 20.99, details: null})

db.products.find().pretty()

// insert product with different schema
db.products.insertOne({name: "A Computer", price: 1299, details: {cpu: "Intel i7 8770"}})
```



### Data Types in MongoDB

- MongoDB allows to define schema and structure documents as per use case or application

- Different data types that can be used in MongoDB are text, boolean, integer, floating-point, decimal, ObjectId, Date, timestamp, arrays and embedded documents

- There is no hard limitation on the number of characters in text but the maximum document size is 16MB

- MongoDB supports different integer types, int32 and int64 depending on the range of values to be stored

- The default value type in the MongoDB shell is a 64-bit float value, but smaller or larger integer values can be stored too

- NumberDecimal type is used to store high-precision floating-point values with up to 34 decimal places

- ObjectId is a unique identifier for each document, with a temporal component, ensuring that the documents are sorted based on their timestamp

- ISO date type is used to save dates, and a timestamp type can be created automatically by MongoDB to ensure that the documents are uniquely ordered based on their timestamp

- MongoDB allows embedding documents and arrays of values, with nested documents or lists of arrays also possible.



### Data Types In Action



```js
use companyData
// switched to db company Data

db.companies.insertOne
(
    {
        name: "Fresh Apples Inc", 
        isStartup: true, 
        employees: 33, 
        funding: 123456789101234567890, 
        details: { ceo: "Mark Super" }, 
        tags: [{ title: "super" }, { title: "perfect" }], 
        foundingDate: new Date(), 
        inserted At: new Timestamp()
    }
)

/*
    {
        "acknowledged": true,
        "insertedId" : ObjectId("5b99252f159c35ea114dd665")
    }
*/
    
// funding field is too big thats why it will overflow
// wil be stored as 123456789101234567000
```



- The MongoDB server can drop databases by switching to the database and executing the "drop database" or "db.dropdatabase" command.

- MongoDB can store different data types like text (enclosed in quotation marks), booleans, numbers (integers and floating-point numbers), arrays (using square brackets), embedded documents, dates, and timestamps.

- The shell used in MongoDB is based on JavaScript, and therefore it uses "new date" and "new timestamp" functions to create dates and timestamps.

- The MongoDB shell we use is based on JavaScript.

- JavaScript doesn't differentiate between integers and floating point numbers.

- The number will be stored as a double or float in MongoDB, not as a high-precision decimal number.

- The stored number will have some imprecision on the decimal places.

- In case of super big numbers, it may be necessary to store them separately, perhaps as a string.

- "db.stats" is a utility method provided by the shell. It outputs statistics about the database. It shows the number of collections and objects in the database. It also displays the average object size.



```js
db.numbers.insertOne({a: 1})
db.numbers.findOne()
db.stats()

/*
    {
        "db" "companyData",
        "collections": 2,
        "views": 0,
        "objects": 2,
        "avgObjSize": 134.5,
        "dataSize" : 269,
        "storageSize" : 32768,
        "numExtents": 0,
        "indexes": 2,
        "indexSize" : 32768,
        "fsUsedSize": 543127957504,
        "fsTotalSize": 1000240963584,
        "ok": 1
    }
*/

db.companies.drop()
db.stats()

/*
    {
        "db" : "companyData",
        "collections" : 1,
        "views": 0,
        "objects" : 1,
        "avgObjSize" : 33,
        "dataSize" : 33,
        "storageSize" : 16384,
        "numExtents": 0,
        "indexes" : 1,
        "indexSize" : 16384,
        "fsUsedSize" : 543134736384,
        "fsTotalSize" : 1000240963584,
        "ok": 1
    }
*/

db.numbers.deleteMany({})
db.stats()

/*
    {
        "db" : "companyData",
        "collections" : 1,
        "views" : 0,
        "objects": 0,
        "avgObjSize" : 0,
        "dataSize" : 0,
        "storageSize" : 16384,
        "numExtents" : 0,
        "indexes" : 1,
        "indexSize" : 16384,
        "fsUsedSize" : 543139909632,
        "fsTotalSize": 1000240963584,
        "ok": 1
    }
*/

// to shrink the size of data stored use functions like
db.numbers.insertOne({a: NumberInt(1)})
db.stats()

/*
    {
        "db" : "companyData",
        "collections" : 1,
        "views": 0,
        "objects" : 1,
        "avgObjSize" : 29,
        "dataSize" : 29,
        "storageSize" : 20480,
        "numExtents" : 0,
        "indexes" : 1,
        "indexSize" : 20480,
        "fsUsedSize" : 543148703744,
        "fsTotalSize" : 1000240963584,
        "ok": 1
    }
*/

typeof db.numbers.findOne().a
// number
```





### Data Types & Limits

MongoDB has a couple of hard limits - most importantly, a single document in a collection (including all embedded documents it might have) must be <= 16mb. Additionally, you may only have 100 levels of embedded documents.

- You can find all limits (in great detail) here: [https://docs.mongodb.com/manual/reference/limits/](<https://docs.mongodb.com/manual/reference/limits/>)

- For the data types, go to page: [https://docs.mongodb.com/manual/reference/bson-types/](<https://docs.mongodb.com/manual/reference/bson-types/>)



**Important data type limits are:**

- Normal integers (int32) can hold a maximum value of +-2,147,483,647

- Long integers (int64) can hold a maximum value of +-9,223,372,036,854,775,807

- Text can be as long as you want - the limit is the 16mb restriction for the overall document

It's also important to understand the difference between int32 (NumberInt), int64 (NumberLong) and a normal number as you can enter it in the shell. The same goes for a normal double and NumberDecimal.

**NumberInt** creates a **int32**	value => `NumberInt(55)`

**NumberLong** creates a **int64**	value => `NumberLong(7489729384792)`

If you just use a number (e.g. `insertOne({a:&nbsp;1}`), this will get added as a **normal double** into the database. The reason for this is that the shell is based on JS which only knows float/ double values and doesn't differ between integers and floats.

**NumberDecimal** creates a high-precision double value => `NumberDecimal("12.99")` => This can be helpful for cases where you need (many) exact decimal places for calculations.

When not working with the shell but a MongoDB driver for your app programming language (e.g. PHP, .NET, Node.js, ...), you can use the driver to create these specific numbers.

Example for Node.js: [<u>http://mongodb.github.io/node-mongodb-native/3.1/api/Long.html</u>

](<http://mongodb.github.io/node-mongodb-native/3.1/api/Long.html>)



```javascript
// This will allow you to build a NumberLong value like this:
const Long = require('mongodb').Long;&nbsp;
db.collection('wealth').insert({value: Long.fromString("121949898291")});
```

By browsing the API docs for the driver you're using, you'll be able to identify the methods for building int32s, int64s etc.





### How to Derive your Data Structure

- When modeling schemas, it's important to consider what data the application needs or generates, and where it needs it.

- The data structure is defined by the fields required and how they relate to each other, and this may involve grouping fields together.

- The type of data or information to be displayed on different pages defines the queries needed, which also impacts the collections and document structure.

- Consider how often data is fetched and written, as this affects the optimization of data fetching and duplication.

- Relations between different entities in the data are important to model correctly.





### Understanding Relations

- When dealing with multiple collections that are related, it's important to consider how to store related data.

- One way to reflect a relation is by using embedded documents. For example, a user document could have a nested address document.

- Another approach is to use references. For example, a customers collection could have an array of favorite books, where each book is represented by an ID that corresponds to a book document in a separate books collection.

- Using embedded documents can result in duplicate data and can make updates more difficult, while using references requires additional queries but can avoid duplicate data and simplify updates.

- The choice between embedded documents and references depends on the specific use case and the trade-offs between data duplication and ease of querying and updating.





### One To One Relation - Embedded

Lets create a database and application for a hospital where patients have a one-to-one relationship with a disease summary. Disease summary is a summary of the patient's illnesses and previous diseases. Two ways to model the relationship between patient and disease summary: reference approach and embedded document approach:

- Reference approach: patient has a diseaseSummary ID, and a separate collection stores disease summaries

- Embedded document approach: patient document includes the disease summary as an embedded document

- The embedded document approach is more efficient and simpler for a strong one-to-one relationship



```js
use hospital
db.patients.insertOne({name: "Max", age: 29, diseaseSummary: "summary-max-1"})
db.patients.findOne()

/*
    {
        "_id" : ObjectId("5b98d2394d01c52e1637a998"),
        "name": "Max",
        "age" : 29,
        "diseaseSummary" : "summary-max-1"
    }
*/

db.diseaseSummaries.insertOne({_id: "summary-max-1", diseases: ["cold", "broken leg"]})
db.diseaseSummaries.findOne()
// { "_id" : "summary-max-1", "diseases" : [ "cold", "broken leg" ] }

db.patients.findOne().diseaseSummary
// summary-max-1

var dsid = db.patients.findOne().diseaseSummary
dsid
// summary-max-1

db.diseaseSummaries.findOne({_id: dsid})
// {"_id" : "summary-max-1", "diseases" : [ "cold", "broken leg" ] }

db.patients.deleteMany({})
db.patients.insertOne({name: "Max", age: 29, diseaseSummary: {diseases: ["cold", "broken leg"]}})
db.patients.findOne()
```





### One To One Relation - Using References

One-to-one relationships can be modeled with embedded documents or separate collections. A possible example is a person owning a car. Application needs can drive the decision to split up the data into separate collections. If we're only interested in one type of data (e.g. persons or cars), it might not be optimal to fetch all the data with an embedded document. In this case we should use references approach.



```js
use carData

// using embedded approach for one to one relation between user and car
db.persons.insertOne({name: "Max", car: {model: "BMW", price: 40000}})

/*
    {
        "acknowledged": true,
        "insertedId" : ObjectId("5b98d3e94d01c52e1637a99a")
    }
*/

db.persons.findOne()

/*
    {
        "_id" : ObjectId("5b98d3e94d01c52e1637a99a")
        "name" : "Max",
        "car" : {
                    "model": "BMW",
                    "price" 40000
                }
    }
*/

db.persons.deleteMany({})

// // using references approach for one to one relation between user and car
db.persons.insertOne({name: "Max", age: 29, salary: 3000})

/*
    {
        "acknowledged": true,
        "insertedId" : ObjectId("5b98d4654d01c52e1637a99b")
    }
*/

db.cars.insertOne({model:"BMW", price:40000, owner: ObjectId("5b98d4654d01c52e1637a99b")})
```





### One To Many Relation - Embedded

One-to-many relationships are common, such as in the Q&A section of Udemy where a question thread can have multiple answers. In MongoDB, one way to model this is to have a separate collection for answers and store IDs to the answers in the question thread collection.



```js
use support

db.question Threads.insertOne
(
    {
        creator: "Max", question: "How does that all work?", 
        answers: ["q1a1","q1a2"]
    }
)

/*
    {
        "acknowledged": true,
        "insertedId" : ObjectId("5b98d5104d01c52e1637a99d")
    }
*/

db.questionThreads.findOne()

/*
    {
        "_id" : ObjectId("5b98d5104d01c52e1637a9d"),
        "creator": "Max",
        "question" : "How does that all work?",
        "answers" : ["q1a1", "q1a2"]
    }
*/

db.answers.insertMany
(
    [
        {_id: "qlal", text: "It works like that."}, 
        {_id: "q1a2", text: "Thanks!"}
    ]
)
// { "acknowledged": true, "insertedIds" : [ "qla1", "q1a2" ] }

db.answers.find()

// {"_id" : "qlal", "text": "It works like that." }
// {"_id" : "qla2", "text": "Thanks" }
```



Another approach is to embed the answers as a list of documents within the question thread document, which is useful for scenarios where the merged data is needed and the number of answers is not too large to cause document bloat.

For larger scenarios, querying by reference might be more efficient than embedding.



```js
db.questionThreads.deleteMany({})
db.questionThreads.insertOne
(
    {
        creator: "Max", 
        question: "How does that work?", 
        answers: [{text: "Like that."}, {text: "Thanks!"}]
    }
)

db.questionThreads.findOne()

/*
    {
        "_id" : ObjectId("5b98d5c14d01c52e1637a99e"),
        "creator": "Max",
        "question" : "How does that work?",
        "answers": [{"text": "Like that."}, {"text": "Thanks!"}]
    }
*/
```





### One To Many Relation - Using References

- One-to-many relationships can be split into collections to avoid overhead data and hitting document limitations.

- For a database holding major cities and citizens, embedding all citizens within a city document would result in unnecessary data and take a long time to fetch.

- Splitting the data into separate collections for cities and citizens would allow for more efficient retrieval of metadata and avoiding the 16mb limit for nested documents.

- The cities collection would store only city metadata, while the citizens would be stored in a separate collection with their associated city ID.

- Each citizen would have a unique ID, such as an object ID.

- Using insertMany requires square brackets around all objects being inserted.

- Retrieving just the cities or citizens can be done efficiently without unnecessary data transfer.



```js
use cityData
db.cities.insertOne({name: "New York City", coordinates: {lat: 21, 1ng: 55}})

/*
    {
        "acknowledged": true,
        "insertedId" : ObjectId("5b98d6b44d01c52e1637a99f")
    }
*/

db.cities. findOne()

/*
    {
        "_id" : ObjectId("5b98d6b44d01c52e1637a⁹
        "name": "New York City",
        "coordinates" : {
                            "lat": 21,
                            "lng" : 55
                        }
    }
*/

db.citizens.insertMany 
(
    [
        {name: "Max Schwarzmueller", cityId: ObjectId("5b98d6b44d01c52e1637a99f"}, 
        {name: "Manuel Lorenz", cityId: ObjectId("5b98d6b44d01c52e1637a99f"}
    ]
)

db.citizens.find().pretty()
/*
    {
        "_id" : ObjectId("5b98d7284d01c52e1637a9a0"),
        "name": "Max Schwarzmueller",
        "cityId" : ObjectId("5b98d6b44d01c52e1637a99f")
    }

    {
        "_id" : ObjectId("5b98d7284d01c52e1637a9a1"),
        "name" : "Manuel Lorenz",
        "cityId" : ObjectId("5b98d6b44d01c52e1637a99f")
    }
*/
```





### Many To Many Relation - Embedded

- In the context of customers buying products, this creates a many-to-many relationship, where a customer can buy multiple products, and a product can be bought by different customers

- This relationship can be modeled using references, typically in SQL, where a join table is created

- In MongoDB, it can be modeled with two tables only, without a third table or join table, by updating the customers' collection and adding an array of orders, where each order is an object with a product ID and quantity

- This is still a reference-driven approach, as only the product ID is referenced, not the entire product data



```js
use shop

// SQL approach
db.products.insertOne({title: "A Book", price: 12.99})
/* 
    {
        "acknowledged": true,
        "insertedId" : ObjectId("5b98d7a04d01c52e1637a9a2")
    }
*/

db.customers.insertOne({name: "Max", age: 29})
/*
    {
        "acknowledged": true,
        "insertedId" : ObjectId("5b98d7ac4d01c52 1637 19a3")
    }
*/

db.orders.insertOne
(
    {
        productId: ObjectId("5b98d7a04d01c52e1637a9a2"), 
        customerId: ObjectId("5b98d7ac4d01c52e1637a9a3") 
    }
)

db.orders.drop()
//true

db.products.find()
// {"_id" : ObjectId("5b98d7a04d01c52e1637a9a2"), "title" : "A Book", "price": 12.99 }

db.customers.find()
// { "_id" : ObjectId("5b98d7ac4d01c52e1637a9a3"), "name" : "Max", "age" : 29 }

db.customers.updateOne({}, {$set: {orders: [{productId: ObjectId("5b98d7a04d01c52e1637a9a2"), quantity: 2}]}})
//{ "acknowledged": true, "matchedCount": 1, "modified Count": 1 }

db.customers.findOne()

/*
    {
        "_id" : ObjectId("5b98d7ac4d01c52e1637a9a3"),
        "name": "Max",
        "age" : 29,
        "orders": [
                    {
                        "productId" : ObjectId("b98d 'a04d01c52e1637a9a2"),
                        "quantity" : 2
                    }
                  ]
        }
*/
```



- Alternatively, an embedded approach can be used, where the orders array is replaced with an array of documents containing both metadata for the order (e.g. quantity) and the product data (e.g. title, price)

- One disadvantage of this approach is data duplication, as product data would be duplicated in each order document

- However, this approach may be fine, as changes in the product data would not affect existing orders, and the unique product ID can still be used to identify the product.



```js
// Alternative approach
db.customers.updateOne({}, {$set: {orders: [{title: "A Book", price: 12.99, quantity: 2}]}})
db.customers.findOne()

/*
    {
        "_id" : ObjectId("5b98d7ac4d01c52e1637a9a3"),
        "name": "Max",
        "age" : 29,
        "orders": [
                    {
                    "title": "A Book",
                    "price": 12.99,
                    "quantity" : 2
                    }
                  ]       
    }
*/
```





### Many To Many Relation - Using References

- Many-to-many relationship example with books and authors. A book can multiple authors and an author can write multiple books.

- Embedded approach: authors' data is embedded in books collection. And authors collection also exists separately.

- Changes in authors' data require updates in both books and authors collections, which is error-prone and bad for performance.



```js
use bookRegistry
db.books.insertOne
(
    {
        name: "My favorite Book", 
        authors: [{name: "Max Schwarz", age: 29}, {name: "Manuel Lor", age: 30}]
    }
)

db.books.find().pretty()
/*
    {
        "_id" : ObjectId("5b98d9984d01c52e1637a9a5"),
        "name": "My favorite Book",
        "authors" : [
                        {
                            "name" : "Max Schwarz",
                            "age" : 29
                        },
                        {
                            "name": "Manuel Lor",
                            "age" : 30
                        }
                    ]
    }
*/

db.authors.insertMany
(
    [
        {name: "Max Schwarz", age: 29, address: {street: "Main"}}, 
        {name: "Manuel Lor", age: 30, address: {street: "Tree"}}
    ]
)

db.authors.find().pretty()

/*
    {
        "_id" : ObjectId("5b98d9e44d01c52e1637a9a6"),
        "name": "Max Schwarz",
        "age" : 29, I
        "address" : {"street" "Main"}
    }
    {
        "_id" : ObjectId("5b98d9e44d01c52e1637a9a7"),
        "name": "Manuel Lor",
        "age" : 30,
        "address" : {"stree" : "Tree"}
    }
*/
```



- Reference approach: books collection only contains references to authors' ObjectId

- Author data is guaranteed to be up-to-date

- Manual merging of data is required when fetching all books with their corresponding authors' data.



```js
db.books.updateOne
(
    {}, 
    {
        $set: {
            authors: [
                Objectid 5b98d9e44d01c52e1637a9a6"), 
                ObjectId("5b98d9e44d01c52e1637a9a7")
            ]
        }
    }
)

db.books.findOne()

/*
    {
        "_id" : ObjectId("5b98d9984d01c52e1637a9a5"),
        "name": "My favorite Book",
        "authors": [
                        ObjectId("5b98d9e44d01c52e1637a9a6"),
                        ObjectId("5b98d9e44d01c52e1637a9a7");
                   ]
    }
*/
```





### Summarizing Relations

- Embedded documents are good for grouping logically related data for one-to-many or one-to-one relations that do not overlap with other data

- Super deep nesting should be avoided as there is a limit of 100 levels and a 16mb limit per document (including embedded documents)

- Reference approach is great for many-to-many relationships, shared data, or when there is a lot of duplicates to update

- Splitting data across collections is also a good solution if you need to overcome nesting or size limits

- There is no general formula for creating relations, it depends on your application needs, how often data is changed, and the type of relationship (one-to-one, one-to-many, many-to-many)





### Using "lookUp()" for Merging Reference Relations 

- MongoDB offers the lookup operator for merging related documents that are split up using the reference approach.

- The lookup operator is used with the aggregate method, which allows for multiple steps in aggregating data.

- To use the lookup operator, four things need to be defined: the collection to relate documents from, the local field in the collection, the foreign field key in the target collection, and an alias for the merged data.

- The lookup operator allows for merging data in one step and mitigates some of the disadvantages of splitting documents across collections.

- Using references still costs more performance than using embedded documents, but the lookup operator can help with getting the data needed.



```js
db.books.aggregate
(
    [
        {$lookup: {from: "authors", localField: "authors", foreignField: "_id", as: "creators"}}
    ]
).pretty()

/*
    {
    "_id" : ObjectId("5b98d9984d01c52e1637a9a5"),
    "name": "My favorite Book",
    "authors": [ObjectId("5b98d9e44d01c52e1637a9a6"), ObjectId("5b98d9e44d01c52e1637a9a7")],
    "creators" : 
                [
                    {
                    "_id" : ObjectId("5b98d9e44d01c52e1637a9a6"),
                    "name": "Max Schwarz",
                    "age" : 29,
                    "address" : {"street" : "Main},
                    "_id" : ObjectId("5b98d9e44d01c52e1637a9a7"),
                    "name": "Manuel Lor",
                    "age" : 30,
                    "address" : {"street" : "Tree"}
                    }
                ]
    }
*/
```





### Example Project: A Blog App

- In this exercise, the goal is to define a schema for a blog app, identify core entities and their relationships, and model those relations.

- The application has a user, post, and comment data entities.

- The user may have a name, age, and email.

- The post may have a title, text, comments and tags.

- The comment may have some text.

- A user can create, edit, and delete a post and comment on a post.

- A post can have multiple comments, and each comment belongs to a user.

- The approach to model these entities is to go with one collection only, the post collection.

- Users and comments can be embedded in the post collection.

- Nesting comments in the post collection is a good idea because comments are a one-to-many relationship, and a post typically does not have millions of comments.

- Nesting the user in the post collection is not a good idea because one user can create many posts, which can result in a lot of duplicate data.

- A better approach is to create two collections, users, and posts, and use embedded documents for comments and tags in the post collection.



```js
use blog
db.users.insertMany
(
    [
        { name: "Max Schwarzmueller", age: 29, email: "max@test.com" }, 
        { name: "Manuel Lolrenz", age: 30, email: "manu@test.com" }
    ]
)

db.users.find().pretty()

/*
    {
        "_id" : ObjectId("5b98e0db4d01c52e1637a9a8"),
        "name": "Max Schwarzmueller",
        "age" : 29,
        "email" : "max@test.com"
    }
    {
        "_id" : ObjectId("5b98e0db4d01c52e1637a9a9"),
        "name" : "Manuel Lorenz",
        "age" : 30,
        "email" : "manu@test.com"
    }
*/
```



Relations are established between the posts and users collections, with the post creator identified by their unique ID. Comments are also added to the post, with each comment including the text and the ID of the user who created it.



```js
db.posts.insertOne
(
    {
        title: "My first Post!", 
        text: "This is my first post, I hope you like it!", 
        tags: ["new", "tech"], 
        creator: ObjectId("5b98e0db4d01c52e1637a9a9"), 
        comments: [{text: "I like this post.!", author: ObjectId("5b98e0db4d01c52e1637a9a8")}]
    }
)

db.posts.findOne()

/*
    {
        "_id" ObjectId("5b98e17d4d01c52e1637a9aa"),
        "title": "My first Post!",
        "text" : "This is my first post, I hope you like it!",
        "tags": ["new", "tech"],
        "creator": ObjectId("5b98e0db4d01c52e1637a9a9"),
        "comments" : [
                        {
                        "text": "I like this post!",
                        "author": ObjectId("5b98e0db4d01c52e1637a9a8")
                        }
        ]
    }
*/
```



It is very important to structure data and relations in a way that makes sense for the specific application, taking into account factors such as data size, frequency of updates, and overall structure.





### Schema Validation

- Schema validation can help lock down flexibility in MongoDB when a strict schema is needed.

- Schema validation validates incoming data based on the defined schema and either accepts or rejects it.

- Schema validation can be defined for insert, update, or insertMany operations.

- Schema validation can be set to strict or moderate validation level.

- Schema validation can be set to throw an error or log a warning if validation fails.

- Choosing the validation level and action depends on the application's needs.

- Schema validation can be added in the code.



### Adding Collection Document Validation

- Adding validation to MongoDB collections can be done easily by explicitly creating the collection with a validator schema when adding it for the first time.

- The create collection command is used to explicitly create a collection and define a validator schema as the second argument to configure the collection.

- The validator key takes a sub-document where a JSON schema can be defined against which incoming data with insert or updates has to validate.

- A schema can be defined for every document added to the collection by setting the bson type to object and the required key as an array containing the names of fields that are required in the document.

- Properties of documents in the collection can be defined in more detail by adding a properties key, a nested document, and defining their bson types, whether they are required, and descriptions.



```js
db.posts.drop()

db.createCollection('posts', {
  validator: {
    $jsonSchema: {
      bsonType: 'object',
      required: ['title', 'text', 'creator', 'comments'],
      properties: {
        title: {
          bsonType: 'string',
          description: 'must be a string and is required'
        },
        text: {
          bsonType: 'string',
          description: 'must be a string and is required'
        },
        creator: {
          bsonType: 'objectId',
          description: 'must be an objectid and is required'
        },
        comments: {
          bsonType: 'array',
          description: 'must be an array and is required',
          items: {
            bsonType: 'object',
            required: ['text', 'author'],
            properties: {
              text: {
                bsonType: 'string',
                description: 'must be a string and is required'
              },
              author: {
                bsonType: 'objectId',
                description: 'must be an objectid and is required'
              }
            }
          }
        }
      }
    }
  }
})

db.posts.insertOne
(
    {
        title: "My first Post!", 
        text: "This is my first post, I hope you like it!", 
        tags: ["new", "tech"], 
        creator: ObjectId("5b98e0db4d01c52e1637a9a9"), 
        comments: [{text: "I like this post.!", author: ObjectId("5b98e0db4d01c52e1637a9a8")}]
    }
)
```





### Changing the Validation Action

- Additional settings can be set for validation in MongoDB. To activate the settings, the collection needs to be created again and validation needs to be set up again.

- The db.runCommand function can be used by a database administrator to add validation settings.

- The command to set collection modifier is 'collMod', which defines the collection to be modified.

- Validator and the entire schema needs to be passed to create validation, just like in create collection.

- To change validation settings, a new file needs to be added, where the create collection code is copied into, and run command is used.

- Validation level controls whether all inserts and updates are checked or only updates to elements that were valid before.

- Validation action can be set to 'error' which blocks the action and throws an error or 'warn' which writes a warning in the log file and allows the action to be executed.

- A warning is written in the log file if a validation action is set to 'warn' and the action is executed.

- The log file is stored on the system and can be viewed later.

- Validation settings can be configured depending on the application and requirements.



```js
db.runCommand({
	collMod: 'posts',
	validator: {
		$jsonSchema: {
			bsonType: 'object',
			required: ['title', 'text', 'creator', 'comments'],
			properties: {
				title: {
					bsonType: 'string',
					description: 'must be a string and is required'
				},
				text: {
					bsonType: 'string',
					description: 'must be a string and is required'
				},
				creator: {
					bsonType: 'objectId',
					description: 'must be an objectid and is required'
				},
				comments: {
					bsonType: 'array',
					description: 'must be an array and is required',
					items: {
						bsonType: 'object',
						required: ['text', 'author'],
						properties: {
							text: {
								bsonType: 'string',
								description: 'must be a string and is required'
							},
							author: {
								bsonType: 'objectId',
								description: 'must be an objectid and is required'
							}
						}
					}
				}
			}
		}
	},
	validationAction: 'warn'
});
```





### Module Summary

- Its is recommended that when developing a database, it is crucial to consider the structure and modeling of the data. This involves taking into account the format in which the data will be fetched and how frequently it will be fetched or changed.

- Additionally, it is important to optimize for either reads or writes, depending on the specific use case. Duplicate data should be avoided for frequently updated information, while duplicates can be allowed for infrequently changing data that is frequently read.

- Furthermore, the amount and size of data to be saved should also be considered, along with the relationships between the data, such as one-to-one, one-to-many, or many-to-many relationships.

- Choosing between embedding or referencing data will depend on these relationships and the need to fetch data separately or deal with large amounts of nested data.

- Finally, It is recommended to implement schema validation to enforce rules on incoming data using JSON schema, as this will help to ensure data consistency and accuracy. It is important to configure how these rules are applied to ensure data integrity



- The MongoDB Limits: [<u>https://docs.mongodb.com/manual/reference/limits/</u>](<https://docs.mongodb.com/manual/reference/limits/>)

- The MongoDB Data Types: [<u>https://docs.mongodb.com/manual/reference/bson-types/</u>](<https://docs.mongodb.com/manual/reference/bson-types/>)

- More on Schema Validation: [<u>https://docs.mongodb.com/manual/core/schema-validation/</u>](<https://docs.mongodb.com/manual/core/schema-validation/>)





















