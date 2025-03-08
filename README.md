[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/fQWKA2YT)
**Week 1: MongoDB Fundamentals Assignment**

**Objective:**

- Apply MongoDB concepts learned throughout the week.
- Practice working with databases, collections, and documents.
- Develop skills in CRUD operations and data modeling.

**Instructions:**

1. **Setup MongoDB:**

   - Install MongoDB locally or create a free cluster on MongoDB Atlas.
   - Start the MongoDB server locally or connect to the MongoDB Atlas cluster.
   - Verify the installation and connection by running:
     ```sh
     mongo --version
     ```

2. **Database and Collection Creation:**

   - Create a new database called `library`.
   - Inside `library`, create a collection named `books`.

3. **Insert Data:**

   - Insert at least five book records into the `books` collection.
   - Each book should contain fields such as `title`, `author`, `publishedYear`, `genre`, and `ISBN`.

4. **Retrieve Data:**

   - Retrieve all books from the collection.
   - Query books based on a specific author.
   - Find books published after the year 2000.

5. **Update Data:**

   - Update the `publishedYear` of a specific book.
   - Add a new field called `rating` to all books and set a default value.

6. **Delete Data:**

   - Delete a book by its `ISBN`.
   - Remove all books of a particular genre.

7. **Data Modeling Exercise:**

   - Create a data model for an e-commerce platform including collections for `users`, `orders`, and `products`.
   - Decide on appropriate fields and relationships (embedding vs. referencing).
   - Implement the structure using MongoDB.

8. **Aggregation Pipeline:**

   - Use aggregation to find the total number of books per genre.
   - Calculate the average published year of all books.
   - Identify the top-rated book.

9. **Indexing:**

   - Create an index on the `author` field to optimize query performance.
   - Explain the benefits of indexing in MongoDB.

10. **Testing:**

   - Use the MongoDB shell or Compass to verify the inserted and updated records.
   - Ensure all queries return the expected results.

11. **Documentation:**

   - Create a `README.md` file with step-by-step instructions on setting up and running your database.

12. **Submission:**

   - Push your code and scripts to your GitHub repository.

**Evaluation Criteria:**

- Proper setup and connection of MongoDB.
- Accurate implementation of CRUD operations.
- Correct data modeling with appropriate relationships.
- Use of aggregation for insightful queries.
- Clear and concise documentation.
- Proper indexing implementation.




# ANSWERS
# MongoDB Setup and CRUD Operations

## Step 1: Setup MongoDB
### Install MongoDB locally or create a free cluster on MongoDB Atlas.
Start the MongoDB server locally:
```sh
mongod --dbpath /path/to/data/db
```
Verify installation:
```sh
mongo --version
```

## Step 2: Database and Collection Creation
Open the MongoDB shell or use a Node.js script:
```sh
use library
db.createCollection("books")
```

## Step 3: Insert Data
Insert five book records:
```sh
db.books.insertMany([
  { title: "The Pragmatic Programmer", author: "Andrew Hunt", publishedYear: 1999, genre: "Technology", ISBN: "978-0201616224" },
  { title: "Clean Code", author: "Robert C. Martin", publishedYear: 2008, genre: "Technology", ISBN: "978-0132350884" },
  { title: "The Hobbit", author: "J.R.R. Tolkien", publishedYear: 1937, genre: "Fantasy", ISBN: "978-0547928227" },
  { title: "1984", author: "George Orwell", publishedYear: 1949, genre: "Dystopian", ISBN: "978-0451524935" },
  { title: "The Da Vinci Code", author: "Dan Brown", publishedYear: 2003, genre: "Thriller", ISBN: "978-0307474278" }
])
```

## Step 4: Retrieve Data
Retrieve all books:
```sh
db.books.find().pretty()
```
Find books by author:
```sh
db.books.find({ author: "Robert C. Martin" }).pretty()
```
Find books published after 2000:
```sh
db.books.find({ publishedYear: { $gt: 2000 } }).pretty()
```

## Step 5: Update Data
Update the publishedYear of a book:
```sh
db.books.updateOne({ ISBN: "978-0547928227" }, { $set: { publishedYear: 1951 } })
```
Add a rating field to all books:
```sh
db.books.updateMany({}, { $set: { rating: 4.5 } })
```

## Step 6: Delete Data
Delete a book by ISBN:
```sh
db.books.deleteOne({ ISBN: "978-0307474278" })
```
Remove all books in a specific genre:
```sh
db.books.deleteMany({ genre: "Technology" })
```

## Step 7: Data Modeling for E-Commerce
### Collections:
#### Users
```json
{
  "_id": ObjectId,
  "name": "John Doe",
  "email": "john@example.com",
  "address": "123 Main St",
  "orders": [ObjectId]  // References Orders
}
```
#### Products
```json
{
  "_id": ObjectId,
  "name": "Laptop",
  "price": 1000,
  "category": "Electronics",
  "stock": 20
}
```
#### Orders
```json
{
  "_id": ObjectId,
  "userId": ObjectId,  // References Users
  "products": [{ "productId": ObjectId, "quantity": 2 }],
  "totalAmount": 2000
}
```

## Step 8: Aggregation Pipeline
Total books per genre:
```sh
db.books.aggregate([
  { $group: { _id: "$genre", count: { $sum: 1 } } }
])
```
Average published year:
```sh
db.books.aggregate([
  { $group: { _id: null, avgYear: { $avg: "$publishedYear" } } }
])
```
Top-rated book:
```sh
db.books.find().sort({ rating: -1 }).limit(1)
```




