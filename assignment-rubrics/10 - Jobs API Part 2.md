### **Assignment Review Guide**

#### **Lesson 10: Jobs API Part 2**
| Week | Topic | Learning Objective |
| ------ | ------ | ------ |
| 10 | Jobs API Part 2 | Students will complete CRUD operations, implement security middleware, handle validation errors, and deploy the API to Render.com. |

#### **Assignment Rubric**
You can mark the student's assignment as complete if they:
*   [ ] Successfully implemented and tested all CRUD operations for their model.
*   [ ] Created and pushed the `week10` git branch.
*   [ ] **Security:** Included `helmet`, `cors`, `xss-clean`, and `express-rate-limit` in the application.
*   [ ] **Access Control:** Verified that each operation uses the User ID to restrict access to the correct user.
*   [ ] **Postman:** Created a Postman collection with tests using environment variables for the URL and `accessToken`.
*   [ ] **Deployment:** Deployed the application to **Render.com** (not Heroku).

#### **What to Look For**
*   **Security Integration:** Check `app.js` (or the main server file) to ensure the security packages are required and used as middleware.
*   **Deployment Configuration:** Verify the presence of a `.node-version` file in the repository.
*   **Render.com URL:** The student should provide a live URL (e.g., `https://jobs-api-<name>.onrender.com`) that has been tested in Postman.
*   **Error Handling:** Look for logic that returns meaningful error messages specifically for Mongoose validation errors.
*   **Environment Variables:** Ensure no sensitive information (like `MONGO_URI` or `JWT_SECRET`) is hardcoded in the source code; they should be in environment variables.

#### **Bonus Task**
*   [ ] Did the student attempt to implement **Swagger/OpenAPI** documentation for their endpoints?
