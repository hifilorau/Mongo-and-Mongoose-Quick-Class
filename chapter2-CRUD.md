# MongooseClass

## Chapter II: Delving into Mongoose CRUD Operations

In the previous chapter, we introduced Mongoose and CRUD operations, created a Mongoose model, defined a schema, and connected to a MongoDB database. In this chapter, we will delve deeper into each of the CRUD operations, exploring their parameters and usage in more detail.

### Create: Model.create()

To create a new document in MongoDB, we can use the Model.create() method. This method takes an object containing the document's data as its parameter and returns a promise that resolves to the created document. Here's an example:

```
const newUser = {
  name: 'John Doe',
  age: 28,
  email: 'john.doe@example.com',
};

User.create(newUser)
  .then((createdUser) => console.log('User created:', createdUser))
  .catch((err) => console.error('Error creating user:', err));
  
  ```
  
  In the above example, we create a new user document with the given data and log the created user to the console.

### Read: Model.find() and Model.findOne()

To read documents from MongoDB, we can use the Model.find() and Model.findOne() methods. The find() method returns an array of documents that match the specified query, while findOne() returns the first document that matches the query or null if no document is found. Both methods accept an optional query object as their first parameter, followed by an optional options object.

Here's an example:

```
// Find all users
User.find()
  .then((users) => console.log('All users:', users))
  .catch((err) => console.error('Error finding users:', err));

// Find user by email
User.findOne({ email: 'john.doe@example.com' })
  .then((user) => console.log('User found:', user))
  .catch((err) => console.error('Error finding user:', err));
  
 ```
 
 In the above example, we first find all users in the database and log them to the console. Then, we find a user with a specific email address and log the found user to the console.

### Update: Model.updateOne() and Model.updateMany()

To update documents in MongoDB, we can use the Model.updateOne() and Model.updateMany() methods. The updateOne() method updates the first document that matches the specified query, while updateMany() updates all documents that match the query. Both methods take a query object as their first parameter, followed by an update object specifying the updates to apply, and an optional options object.

Here's an example:

```
// Update user's age by email
User.updateOne({ email: 'john.doe@example.com' }, { $set: { age: 29 } })
  .then((result) => console.log('User updated:', result))
.catch((err) => console.error('Error updating user:', err));

// Increment the age of all users by 1
User.updateMany({}, { $inc: { age: 1 } })
.then((result) => console.log('All users updated:', result))
.catch((err) => console.error('Error updating users:', err));
```

In the above example, we first update the age of a user with a specific email address and log the result to the console. Then, we increment the age of all users by 1 and log the result to the console.

### Delete: Model.deleteOne() and Model.deleteMany()

To delete documents in MongoDB, we can use the `Model.deleteOne()` and `Model.deleteMany()` methods. The `deleteOne()` method deletes the first document that matches the specified query, while `deleteMany()` deletes all documents that match the query. Both methods take a query object as their first parameter, followed by an optional options object.

Here's an example:

```javascript
// Delete user by email
User.deleteOne({ email: 'john.doe@example.com' })
  .then((result) => console.log('User deleted:', result))
  .catch((err) => console.error('Error deleting user:', err));

// Delete all users with age greater than or equal to 30
User.deleteMany({ age: { $gte: 30 } })
.then((result) => console.log('Users deleted:', result))
.catch((err) => console.error('Error deleting users:', err));

```

In the above example, we first delete a user with a specific email address and log the result to the console. Then, we delete all users with an age greater than or equal to 30 and log the result to the console.

### Conclusion

In this chapter, we explored the CRUD operations in Mongoose in more detail, including their parameters and usage. We covered creating documents using `Model.create()`, reading documents with `Model.find()` and `Model.findOne()`, updating documents using `Model.updateOne()` and `Model.updateMany()`, and deleting documents with `Model.deleteOne()` and `Model.deleteMany()`.

With this knowledge, you can now perform CRUD operations on MongoDB using Mongoose effectively, allowing you to build more complex and data-driven applications with ease. As you continue to work with Mongoose and MongoDB, you may also explore more advanced features such as pagination, transactions, indexing, and aggregation to further optimize your application's performance and capabilities.
