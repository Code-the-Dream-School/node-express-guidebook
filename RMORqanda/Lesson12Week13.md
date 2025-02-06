1. Which method is used to handle asynchronous results from a promise? **ANSWER: A**

   **A. .then()**

   B. .resolve()

   C. .await()

   D. .sync()

---

2. What is the primary purpose of using regular expressions (regex)? **ANSWER: C**

   A. To format text by adding spaces and punctuation.

   B. To perform complex mathematical calculations and solve equations.

   **C. To search for, match, and manipulate specific patterns within text data.**

   D. To encrypt and decrypt sensitive information for secure communication.

---

3. What does Express do for Node.js? (Select all that apply) **ANSWERS: A, B, D**

   **A. Provides a framework for building web applications and APIs**

   **B. Manages and handles HTTP requests and responses**

   C. Replaces the built-in http module in Node.js

   **D. Simplifies routing and middleware integration**

   E. Automatically handles database connections

---

4. In your own words describe Node.js (Speak aloud as if interviewing)

   **One possible answer:**
   Node.js is a runtime environment that allows you to run JavaScript on the server side, outside of a web browser. Built on Chrome's V8 JavaScript engine, it enables asynchronous, event-driven architecture, making it highly efficient for handling concurrent requests, especially in I/O-heavy applications.

   One of its main strengths is non-blocking, single-threaded event loops, meaning it can process multiple operations without waiting for previous ones to complete. This is particularly advantageous for applications like real-time chat, streaming, or APIs that require high scalability.

   Node.js uses the npm (Node Package Manager) ecosystem, which offers a huge library of open-source packages, making it easier to integrate third-party tools and functionalities. It’s commonly used in backend development, but its versatility also makes it suitable for building command-line tools, web servers, and microservices.

   Overall, Node.js is great for building fast, scalable, and high-performance applications, especially when real-time communication or handling many simultaneous connections is needed.

---

5. In your own words describe what an API is (Speak aloud as if interviewing)

   **One possible answer:**
   An API, or Application Programming Interface, is a set of rules and protocols that allows one software application to interact with another. It defines the methods and data formats for requesting and exchanging information, making it easier for developers to integrate different systems or services without needing to understand their underlying code.

   APIs act as a bridge between different software components, whether it's between a client and a server, or between different systems in a microservices architecture. For example, when you use a weather app, the app may call an API to get the latest weather data from a remote server.

   APIs can be categorized into different types: 
   - **REST APIs** (Representational State Transfer) are widely used because they follow stateless principles and rely on standard HTTP methods like GET, POST, PUT, and DELETE.
   - **SOAP APIs** (Simple Object Access Protocol) are more rigid and typically used in enterprise settings.
   - **GraphQL** is another type that allows more flexible querying of data.

   In essence, APIs simplify and standardize communication between different software systems, enabling developers to leverage external functionality and build more complex, efficient applications.

---

6. Which method would you use to merge two or more arrays into a single array? **ANSWER: B**

   A. join()

   **B. concat()**

   C. flat()

   D. split()

---

7. What is the role of planning/pseudo code in problem-solving? **ANSWER: D**

   A. Planning is optional and can be skipped if you have a good understanding of the problem.

   B. Planning involves guessing the possible solutions without a structured approach.

   C. Planning should only focus on the implementation details.

   **D. Planning involves outlining the exact steps needed to solve the problem before starting to code.**

---

8. Which method can be used to execute a function on each element of an array and return a new array with the results? **ANSWER: A**

   **A. map()**

   B. filter()

   C. some()

   D. every()

---

9. Describe application deployment in your own words. Be sure to include the process of connecting a MongoDB database to a Node.js Express application on Render.com and steps for both configuring the database connection and handling environment variables securely.

   **One possible answer:**
   Application deployment refers to the process of moving your code from a local development environment to a live server where users can access it. In the case of a Node.js Express app with a MongoDB database, deployment typically involves setting up a cloud server, configuring the database, and ensuring your app can securely connect to it.

   For example, if deploying to Render.com:

   1. **Push your code to a Git repository** (like GitHub) and link it to Render.

   2. **Deploy your Node.js app** by creating a new web service on Render and specifying the branch to deploy from.

   3. **Add MongoDB**: You can create a MongoDB instance directly on Render or use an external service like MongoDB Atlas. Obtain the connection URL (e.g., `mongodb://username:password@host:port/database`).

   4. **Set environment variables**: In Render, you can add environment variables like `MONGO_URI` to store the MongoDB connection URL securely. These variables can be set in the Render dashboard under the "Environment" tab.

   5. **Configure database connection**: In your Node.js app, use a package like `mongoose` to connect to MongoDB. In your `app.js` or `server.js`, use `process.env.MONGO_URI` to securely access the database URI, ensuring no sensitive info is hardcoded.

   By using environment variables, you protect sensitive credentials while ensuring that your app can securely connect to MongoDB in the production environment.

---

10. What is the purpose of the build command in the Render.com deployment setup for a Node.js application? **ANSWER: C**

    A. To install dependencies and set up the runtime environment
   
    B. To compile TypeScript files into JavaScript
   
    **C. To execute scripts and prepare the application for deployment**
   
    D. To test the application before deployment

---

11. Describe in detail how Mongoose is used in conjunction with MongoDB (Written response and speak this question aloud as if interviewing)

    **One possible answer:**
    Mongoose is an Object Data Modeling (ODM) library for MongoDB and Node.js, providing a higher-level abstraction to interact with MongoDB databases. It simplifies the process of working with data by offering schema-based modeling, validation, and query-building features.

    To use Mongoose with MongoDB:

       1. **Install Mongoose**: You first install it using `npm install mongoose`.

       2. **Connect to MongoDB**: Mongoose connects to the MongoDB database using `mongoose.connect()`, where you provide the MongoDB URI. This URI can be a local instance or a cloud-based service like MongoDB Atlas.

       3. **Define a Schema**: A schema defines the structure of your documents, including field types, validation, and default values. It acts as a blueprint for your MongoDB collections.  The schema is created using `new mongoose.Schema()` and utilizes objects to define the schema.

       4. **Create a Model**: Mongoose uses the schema to create a model, which provides methods for interacting with the database, such as creating, reading, updating, and deleting documents.

       5. **CRUD Operations**: You can now perform CRUD operations like `User.create()`, `User.find()`, and `User.update()`, leveraging Mongoose’s built-in query methods.

    Mongoose provides a cleaner, more structured way to interact with MongoDB compared to using the native MongoDB driver directly.

---

12. Which of the following techniques can help reduce latency and improve the efficiency of an API? **ANSWER: B**

    A. Using synchronous processing for all requests

    **B. Optimizing database queries and ensuring proper indexing**

    C. Increasing the size of API responses with unnecessary data

    D. Reducing the frequency of API updates and deployments

---

13. Which of the following features can be specified in a Mongoose schema? (Select all that apply) **ANSWER: All of them**

    A. Data types for each field (e.g., String, Number, Date)

    B. Validation rules for data (e.g., required fields, min/max length)

    C. Indexes for optimizing query performance

    D. Methods for data manipulation and querying

---

14. What is a key benefit of using cross-disciplinary collaboration when solving complex problems with technology? **ANSWER: C**

    A. It limits the scope of possible solutions to a single field
   
    B. It ensures that the problem is solved solely with technological approaches
   
    **C. It brings together diverse perspectives and expertise to develop more innovative solutions**
   
    D. It focuses only on technological solutions without considering other fields

---

15. What role does user-centered design play in creating effective technological solutions? **ANSWER: B**

    A. It ensures that the technology is designed for developers rather than end-users
   
    **B. It focuses on meeting the needs and preferences of the end-users to enhance usability and effectiveness**
   
    C. It prioritizes technical specifications over user needs
   
    D. It eliminates the need for user feedback during the design process

---

16. Which of the following methods or options can be used to sort query results in MongoDB? (Select all that apply) **ANSWERS: A, C, D**

    **A. Using the sort() method with a sorting document**
   
    B. Using the find() method with a limit option
   
    **C. Using the find() method with a sort option**
   
    **D. Using the aggregate() method with a $sort stage**

---

17. Describe what strategies are most effective for improving the performance of an API (Written response and speak this question aloud as if interviewing)

    **One possible answer:**
    To improve the performance of an API, several strategies can be implemented:

    1. **Caching**: Store frequently accessed data in a cache (e.g., Redis or Memcached) to reduce database load and decrease response times. Cache API responses or common query results for a set period.

    2. **Database Optimization**: Ensure efficient database queries by indexing frequently queried fields, using query optimization techniques, and minimizing unnecessary joins. Consider using read replicas for handling read-heavy operations.

    3. **Asynchronous Processing**: For long-running tasks, use background processing (e.g., message queues like RabbitMQ or AWS SQS) to avoid blocking API responses. This improves user experience by returning results quickly.

    4. **Rate Limiting**: Implement rate limiting to control the number of requests from users and prevent overload. This ensures fair resource distribution and protects the server from excessive traffic.

    5. **Compression**: Use data compression (e.g., gzip) for API responses to reduce payload size, which speeds up data transfer and reduces bandwidth usage.

    6. **Load Balancing**: Distribute traffic across multiple servers using load balancers, ensuring no single server is overwhelmed, which improves uptime and availability.

    7. **Pagination**: Instead of returning large datasets, implement pagination for list endpoints to limit the number of items returned at once, enhancing both server and client performance.

    These strategies, when applied appropriately, help create a more scalable and responsive API.

---

18. What does the unique: true property do in a Mongoose schema? **ANSWER: B**

    A. Ensures that a field cannot be null

    **B. Enforces that the field's value is unique in the collection**

    C. Automatically indexes the field

    D. Encrypts the field's value

---

19. What is the purpose of indexing in MongoDB? **ANSWER: A**

    **A. To improve query performance by reducing search time**

    B. To duplicate data across multiple collections

    C. To enforce unique constraints on fields

    D. To back up the database automatically

---

20. Describe your project's functionality, purpose, features, and technology used as if it was already complete. (Written response and speak this question aloud as if interviewing)

    **Answers will vary**
