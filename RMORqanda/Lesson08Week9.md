1. What is the primary use of the bcrypt library in a Node.js Express application? **ANSWER: C**

   A) To parse JSON data.

   B) To encrypt and decrypt data.

   **C) To hash and verify passwords securely.**

   D) To handle HTTP requests and responses.



2. Which of the following are potential dangers of storing secrets or tokens in local browser storage (e.g., localStorage or sessionStorage)? (Select all that apply) **ANSWERS: A, C**

   **A) The data is accessible to any JavaScript code running on the same origin.**

   B) The data is transmitted securely over HTTPS.

   **C) The data can be exposed through cross-site scripting (XSS) attacks.**

   D) The data is automatically cleared when the user closes the browser.

   E) The data is protected by the browser’s same-origin policy.



3. What is the primary purpose of using JSON Web Tokens (JWT) in an Express application? **ANSWER: A**

   **A) To securely transmit information between parties as a JSON object.**

   B) To create a unique identifier for each user session.

   C) To store session data on the server.

   D) To encrypt data stored in a database.



4. When hashing a password, what is a key consideration to ensure security? **ANSWER: C**

   A) Use a fast hashing algorithm.

   B) Store the plaintext password in a database for comparison.

   **C) Use a cryptographic hashing algorithm with a salt.**

   D) Use a non-cryptographic hashing algorithm for better performance.



5. Describe what a cookie is and three potential cookie attacks.

   One possible answer: A cookie is a small piece of data stored by a user's browser that helps track and remember information about them, such as session details or preferences. Cookies are often used for authentication, personalization, and tracking user behavior.

   Three potential cookie attacks:

   1. Cross-Site Scripting (XSS) – Malicious scripts steal cookies from a user's session.

   2. Session Hijacking – An attacker intercepts or steals a session cookie to impersonate a user.

   3. Cross-Site Request Forgery (CSRF) – An attacker tricks a user into making unwanted requests with their cookies, compromising their session.



6. Did you change the models for the Jobs API and if so, what did you choose? Will this be your final project?

   Answers will be unique.  Please be sure you're discussing with your students why the Jobs API data models were structured how they were and consult with them about the models they're designing for their final projects. 
