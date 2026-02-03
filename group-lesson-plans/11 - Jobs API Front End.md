# **Lesson Plan 13 – A Front End for the Jobs API**

## **About This Week**
This week, students transition from testing their Jobs API with Postman to building a modular, **client-side front end** using HTML and JavaScript. The application follows a **single-page style**, where five different "views" (DIV elements) are toggled visible or hidden based on user interaction. Key concepts include using the **Fetch API** for asynchronous REST calls, managing **JWTs in local storage**, and implementing modular JavaScript using `import` and `export`.

### **Explore Session (60 minutes)**
**Purpose:** Reinforce how front-end JavaScript modules communicate with a Node/Express back end using the Fetch API.

#### **Segment 1 – Warm-Up (5 min)**
*   **Ask:** “Up until now, we’ve used Postman to see our data. What are the benefits of building a browser-based UI for our API?”
*   **Quick poll:** “Where does our front-end JavaScript code run: the browser, the server, or both?” (Clarify that this week's code runs in the **browser context** with access to the DOM).

#### **Segment 2 – I Do (10 min)**
**Mentor demonstrates modular JS and static files:**
*   Explain `app.use(express.static("public"))` to serve the front end.
*   Show how `index.js` acts as the "orchestrator" using **imports** (remind students that they must use `import`, not `require`, in the browser).
*   **CFU Questions:** 
    *   “Why do we separate the views into different files like `jobs.js` and `login.js`?”
    *   “What happens if we forget to use `type="module"` in our script tag?”

#### **Segment 3 – We Do (20 min)**
**Collaborative example: Handling Asynchronous Fetch calls.**
*   Walk through a `try/catch` block for a POST request.
*   Demonstrate the **Authorization header** using `Bearer ${token}`.
*   Discuss the `inputEnabled` flag used to prevent double-clicks during async operations.
*   **CFU Questions:**
    *   “Why is it important to clear input values (like passwords) before switching views?”
    *   “What is the difference between a 200 and a 201 status code when creating or updating data?”

#### **Segment 4 – You Do (20 min)**
**Short Task: Dynamic DOM updates.**
*   “Look at the `showJobs` function. How does it know which job to update when you click 'edit'?”
*   Practice using `dataset.id` to capture the MongoDB `_id` from a button click.

#### **Segment 5 – Wrap-Up (5 min)**
*   Summarize: Fetch → Asynchronous Results → DOM Updates.
*   **Remind:** Students must also submit a **Final Project Proposal** this week.
*   **Reminder:** Assignments are due **Feb 10, 2026**.

### **Apply Session (60 minutes)**
**Purpose:** Support students in connecting their specific data models to the front-end template and debugging the CRUD operations.

#### **Segment 1 – Quick Recap (5 min)**
*   Address the "Data Model" challenge: Ensure students who used a model other than "Job" have updated their forms and tables to match their unique fields.

#### **Segment 2 – Guided Coding (25 min)**
**Mentor demonstrates the 'Delete' logic (The "Fix it yourself" task):**
*   Talk through using a `fetch` call with the `DELETE` method.
*   **Crucial Correction:** Show them why they must change the back-end controller from `send()` to `json()` to avoid front-end exceptions when parsing the response.

#### **Segment 3 – Peer or Solo Debugging (20 min)**
*   Common bugs to check: Missing JWT tokens in headers, `fetch` URL paths, or `localStorage` not persisting after refresh.
