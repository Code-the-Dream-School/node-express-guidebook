### **Group Mentor Guide**

#### **Week 10: Jobs API Part 2 — Group Mentor Guide**
Welcome to Week 10! This week, students complete the **Jobs API** project by finishing all CRUD operations and adding essential security layers before deploying their work to **Render.com**.

#### **Warm-Up (5–10 minutes)**
Choose one:
**Relationship-Building (Mindset: Focused Execution)**
*   This week has no specific mindset assignment so you can focus entirely on the lesson. How do you handle weeks where the technical load is heavier? 
*   What is one feature you've added to your Jobs API (or custom model) that you are most proud of?

**Check for Understanding (from Part 1)**
*   What is the purpose of the `accessToken` in our Postman configuration?
*   How do we ensure that a user can only see the jobs they created? (Answer: By using the User ID in our Mongoose queries).

#### **Explore vs. Apply — Session Formats**
*   **Explore Sessions** → Walk through the purpose of security middleware (`helmet`, `cors`, `xss-clean`, `express-rate-limit`) and the concept of **Swagger/OpenAPI** for documentation.
*   **Apply Sessions** → Debugging Render.com deployment errors or helping students implement Mongoose validation error handling.

#### **Sample Timing for 1-Hour Session**
| Time | Activity |
| ------ | ------ |
| 0:00–0:10 | Warm-up + Reviewing `week10` branch creation |
| 0:10–0:30 | Explore: Security packages and why they are required for deployment |
| 0:30–0:50 | Apply: Live testing CRUD operations in Postman with env variables |
| 0:50–1:00 | Wrap-up: Deployment steps for Render.com |

#### **Check for Understanding (Ask 2–3)**
*   What does the **helmet** package do for our application? (Answer: Sets HTTP headers to protect against well-known vulnerabilities).
*   Why is **express-rate-limit** important for a public API? (Answer: To prevent denial of service attacks by limiting requests from a single IP).
*   When is **CORS** actually necessary? (Answer: When the front end and back end are on different base URLs, such as in a React project).
*   What is **Swagger**, and why is it useful for developers? (Answer: It documents endpoints so other developers know how to call the API).

#### **Explore Prompts**
*   **The Security Stack:** Let's look at `xss-clean`. Even though it is deprecated, why is it still included in this lesson? (Answer: To prevent cross-site scripting attacks by removing harmful scripts).
*   **Better Error Messages:** How can we improve Mongoose validation errors so the user gets a meaningful message instead of a generic server error?
*   **Environment Variables:** Why must we never push our `.env` file to GitHub, and how do we add those values to Render?

#### **Apply Prompts (Assignment Hotspots)**
*   **Branching:** Remind students to create the `week10` branch while the `week9` branch is active.
*   **Render Versioning:** Ensure students have created a `.node-version` file in their root directory to avoid deployment failures.
*   **Postman Config:** Check that students have set up environment variables for both their URL and the `accessToken`.
*   **Access Control:** Double-check that every CRUD operation—especially Update and Delete—uses the User ID to verify ownership.
