1. In Mongoose, which method is used to handle asynchronous operations with thenables (i.e., Promises) for querying a MongoDB database? **ANSWER:C**

   A) find()

   B) save()

   **C) exec()**

   D) populate()



2. Which regex pattern matches an email address? **ANSWER: A**

   **A) ^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$**

   B) ^https?://[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$

   C) ^\d{4}-\d{2}-\d{2}$

   D) ^[a-zA-Z0-9]{5,}$



3. What will happen if you do not handle the Promise returned by a Mongoose query? **ANSWER: B**

   A) The query will automatically be canceled.

   **B) The query will execute, but you will not be able to access the results or handle errors.**

   C) Mongoose will throw a synchronous error.

   D) The query will be executed, and Mongoose will throw an error if the query fails.




4. Which of the following query parameters can be used to filter results in an API request? (Select all that apply) **ANSWERS: A, C, D, E**

   **A) where**

   B) filter

   **C) q**

   **D) search**

   **E) fields**



5. Which query parameters are commonly used to paginate results in an API request? (Select all that apply) **ANSWERS: A, B, C, D**

   **A) page**

   **B) limit**

   **C) offset**

   **D) start**

   E) range



6. Describe in your own words what a router is.

   One possible answer: A router is a system that manages the navigation and mapping of URLs to specific resources or actions within an application. It determines how incoming HTTP requests are handled and directs them to the appropriate function, controller, or page. Routers are commonly used in both frontend (like React Router) and backend (like Express.js) frameworks to define routes, ensuring that when users visit different URLs, they are served the correct content or functionality. This enables dynamic and responsive user experiences in single-page applications (SPAs) and multi-page web apps.



7. List hypothetical ways a developer and user would want data sorted when returned from an API.

   Possible answers may include any of the following, or other considerations:
   
   a. Alphabetically – Sorting by name, title, or category (ascending or descending).

   b. Numerically – Sorting by price, rating, or count (ascending or descending).

   c. Chronologically – Sorting by date, like creation or update timestamps.

   d. Custom Order – Based on user-defined criteria or preferences.

   e. Randomly – Shuffling the results for variety.

   f. By Relevance – Sorting based on search terms or algorithmic scoring.

   g. Grouped – Sorting by categories or tags, to show related items together.
