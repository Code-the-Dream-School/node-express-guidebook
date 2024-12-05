1. What is the primary purpose of Mongoose in a Node.js application? **ANSWER: A**

   **A) To provide a higher-level abstraction for working with MongoDB**

   B) To serve static files from a server

   C) To handle HTTP requests and responses

   D) To manage user authentication and authorization



2. Which JavaScript array method would you use to create a new array by applying a function to each element of an existing array? **ANSWER: C**

   A) forEach()

   B) filter()

   **C) map()**

   D) reduce()



3. How can you retrieve all documents from a MongoDB collection using Mongoose? **ANSWER: B**

   A) Model.findAll()

   **B) Model.find()**

   C) Model.get()

   D) Model.fetch()



4. Which JavaScript array methods can be used to transform an array into a new array containing only elements that satisfy a specific condition? **ANSWER: B**

   A) map()

   **B) filter()**

   C) reduce()

   D) some()

   E) find()



5. Why is it important to externalize sensitive information, such as API keys and database credentials, into a .env file rather than hardcoding them in the application code?
   
   One possible answer: Externalizing sensitive information like API keys and database credentials into a .env file is important for security and maintainability. Hardcoding these details in application code exposes them to potential breaches, as they may be accidentally committed to version control systems. Storing them in a .env file ensures sensitive data remains separate from the code, easier to manage, and protected from unauthorized access. It also simplifies environment-specific configurations and promotes best practices for deploying across different environments without altering the source code.


7. Describe in detail how Mongoose is used in conjunction with MongoDB.
   
   One possible answer: Mongoose is an Object Data Modeling (ODM) library for MongoDB and Node.js. It provides a schema-based solution to model MongoDB data, enabling developers to define data structures, validation, and business logic. In Mongoose, you define a schema to specify the shape of documents in a MongoDB collection. Then, you create models based on those schemas to interact with the database, such as creating, reading, updating, and deleting documents. Mongoose also supports features like middleware, population (joining related documents), and query building, offering a more structured and flexible way to work with MongoDB in Node.js applications.


9. What is Data Validation and Sanitization and why is it important for the security of an app? Can you list other security elements to consider in terms of storing data?
    
   One possible answer: Data validation ensures that input data is correct, complete, and formatted properly, while sanitization removes harmful elements (like SQL injections or malicious scripts) from input. Both are critical for preventing security vulnerabilities such as cross-site scripting (XSS) and SQL injection. Proper validation and sanitization ensure that only safe, expected data is processed by the app.  Other security elements for storing data include: 1) Encryption (for sensitive data at rest and in transit), 2) Access controls (limiting who can access data), 3) Secure storage (e.g., hashed passwords), and 4) Backup and disaster recovery.
