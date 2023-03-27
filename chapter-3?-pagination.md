# MongooseClass

##Chapter XII: Pagination with Mongoose

As your application grows and the amount of data stored in your MongoDB database increases, it becomes essential to efficiently retrieve and display the data. Pagination is a technique that allows you to fetch and display a subset of data from the database, improving both performance and user experience.

In this chapter, we will explore how to implement pagination using Mongoose. We will cover the basics of pagination, how to use the skip() and limit() methods, and how to create a reusable pagination function.

##Understanding Pagination

Pagination involves dividing your data into smaller chunks or pages and retrieving only a specific page of data at a time. This reduces the amount of data transferred and processed, resulting in faster response times and a better user experience. Pagination is commonly used in web applications, where it's essential to display large datasets in a user-friendly manner.

In Mongoose, we can implement pagination using the skip() and limit() methods available in the query API.

##Using skip() and limit()

The skip() method allows you to skip a specific number of documents before starting to fetch data, while the limit() method allows you to set a limit on the number of documents to retrieve. By combining these two methods, you can achieve pagination in your queries. Here's an example:

```
const pageNumber = 1;
const pageSize = 10;

User.find()
  .skip((pageNumber - 1) * pageSize)
  .limit(pageSize)
  .then((users) => console.log('Users:',users))
.catch((err) => console.error('Error fetching users:', err));

```

In the above example, we fetch a specific page of users by using the `skip()` and `limit()` methods. We calculate the number of documents to skip based on the current `pageNumber` and the desired `pageSize`. In this case, we retrieve the first page of users, with each page containing 10 users.

##Creating a Reusable Pagination Function

To simplify pagination across your application, you can create a reusable function that takes a Mongoose model, query, page number, and page size as parameters and returns the paginated data along with metadata. 

Here's an example:

```javascript
async function paginate(model, query, pageNumber, pageSize) {
  const totalDocuments = await model.countDocuments(query);
  const totalPages = Math.ceil(totalDocuments / pageSize);
  const results = await model
    .find(query)
    .skip((pageNumber - 1) * pageSize)
    .limit(pageSize);

  return {
    pageNumber,
    pageSize,
    totalPages,
    totalDocuments,
    results,
  };
}

// Usage example:
paginate(User, {}, 1, 10)
  .then((data) => console.log('Paginated data:', data))
  .catch((err) => console.error('Error fetching paginated data:', err));
 
 ```
 In the above example, we define a paginate() function that takes a Mongoose model, a query object, a page number, and a page size as parameters. The function first calculates the total number of documents and total pages based on the given query and page size. It then fetches the paginated data using skip() and limit() and returns an object containing the pagination metadata and the results.

The returned object has the following structure:

```
{
  pageNumber: 1, // The current page number
  pageSize: 10, // The number of documents per page
  totalPages: 5, // The total number of pages
  totalDocuments: 50, // The total number of documents matching the query
  results: [...] // The paginated documents
}

```

In the usage example, we call the paginate() function with the User model, an empty query object (to fetch all users), and the desired page number and page size. The function returns a promise that resolves to the paginated data and metadata, which we log to the console.

##Conclusion

In this chapter, we explored how to implement pagination with Mongoose. We discussed the importance of pagination for performance and user experience, and learned how to use the skip() and limit() methods in Mongoose queries to achieve pagination. Additionally, we created a reusable paginate() function to simplify pagination across your application.

With pagination in place, your application can now efficiently handle and display large datasets, resulting in better performance and a more enjoyable user experience. As you continue to work with Mongoose and MongoDB, you may also explore more advanced features such as sorting, filtering, and aggregation to further enhance the capabilities of your application.
 
