## Assignment Review Guide
**Lesson 13: A Front End for the Jobs API**

#### **Assignment Rubric**
You can mark the student's assignment as **complete** if they meet the following criteria:

*   **Git Workflow:** Created a `week11` (or `lesson-13`) branch and submitted a Pull Request.
*   **Project Structure:** Created a `public` directory containing `index.html` and modular JS files (`index.js`, `jobs.js`, etc.).
*   **Core Functionality:**
    *   **Authentication:** User can register and logon (persisting the JWT in `localStorage`).
    *   **Logoff:** Correctly clears the JWT and removes job data from the DOM using `replaceChildren`.
    *   **CRUD:** User can view, add, and edit jobs.
    *   **Delete Task:** Successfully implemented the "delete" logic on the front end and updated the back-end controller.
*   **Mindset/Proposal:** Completed the 3 problem-solving prompts and submitted a **Final Project Proposal** (covering Concept, Data Models, and Features).
*   **Deployment:** The application is deployed and functional on **Render.com**.

#### **What to Look For**
*   **Data Model Consistency:** If the student chose a different topic (e.g., "Recipes"), ensure all forms, table headers, and JS variables were renamed appropriately.
*   **Asynchronous Logic:** Did they correctly use `async/await` and `try/catch` for all fetch operations?
*   **Security:** Verify they are using the `Bearer ${token}` in Authorization headers and clearing inputs after use.
*   **Delete Operation:** Did they handle the "empty body" bug by changing the controller to return valid JSON?
