### **Node v3: Server-Side Rendering with EJS — Group Mentor Guide**

Welcome to Week 14! This week, students are introduced to **Server-Side Rendering (SSR)** using **EJS (Embedded JavaScript)**. Instead of the front-end + back-end model they’ve used previously, they are now building applications where the server constructs the HTML page with dynamic content before sending it to the client.

#### **Warm-Up (5–10 minutes)**
Choose one:
**Relationship-Building (Mindset: Design 101)**
*   Think of a time you were in a new location (physical or web) and couldn't find your way around. How did that frustrate you, and what eventually helped you find your way?
*   What is your favorite design feature as a user? What makes a website "pleasant" to navigate for you?

**Check for Understanding (SSR Basics)**
*   What is the main difference between **server-side rendering** and building an **API** with a separate front end? (Answer: In SSR, the server inserts data directly into HTML templates before sending them to the browser; in an API model, the front end fetches data separately).
*   Where does the JavaScript inside an EJS file execute? (Answer: On the server side).

#### **Explore vs. Apply — Session Formats**
*   **Explore Sessions** → Demonstrate the three primary **EJS syntax tags** (scriplets/squids) and how to use **partials** to avoid repeating boilerplate HTML.
*   **Apply Sessions** → Help students initialize their new `jobs-ejs` repository, install the necessary packages, and debug the **session** and **flash message** logic.

#### **Sample Timing for 1-Hour Session**
| Time | Activity |
| ------ | ------ |
| 0:00–0:10 | Warm-up + Reviewing **Visual Hierarchy** mindset |
| 0:10–0:30 | Explore: EJS syntax (`<%= %>`, `<% %>`, `<%- %>`) and partials |
| 0:30–0:50 | Apply: Implementing **Sessions** and **Flash Messages** |
| 0:50–1:00 | Wrap-up: Discussion on **res.locals** and deployment readiness |

#### **Check for Understanding (Ask 2–3)**
*   What is a **partial**, and why do we use them? (Answer: They are shared templates like headers/footers that prevent repeating code across pages).
*   Why do we store session data in **MongoDB** instead of just server memory? (Answer: Memory storage is lost if the server restarts; a database makes the session data durable).
*   What does the `connect.sid` cookie do? (Answer: It is the key used by the browser to retrieve the specific session data from the server).
*   What is the purpose of **connect-flash**? (Answer: To store temporary messages—like success or error notifications—that persist across a redirect but are only shown once).

#### **Explore Prompts**
*   **EJS Syntax Hunt:** Let’s look at the three types of tags. Which one do we use for logic (like an `if` statement) and which one for outputting data to the page?
*   **The Power of Partials:** Let's create a `head.ejs`. If we want to change the site title for every page, why is it better to have it in a partial?
*   **Session Secrets:** Why is it critical to keep our `SESSION_SECRET` in the `.env` file and never push it to GitHub?

#### **Apply Prompts (Assignment Hotspots)**
*   **New Repository Setup:** Students must create a **fresh** `jobs-ejs` folder that is not inside any previous project trees.
*   **Middleware Order:** Remind students that the **flash** middleware must come *after* the **session** middleware because flash depends on sessions to work.
*   **The Redirect Loop:** Ensure students understand that `app.post` for the secret word should `redirect` back to the GET route to display the updated value.
*   **res.locals:** If flash messages aren't appearing, check if they've passed the `info` and `errors` arrays into `res.locals` so they are available to the EJS engine.
