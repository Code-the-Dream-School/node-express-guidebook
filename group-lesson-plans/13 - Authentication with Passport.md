## **Lesson 13: Authentication with Passport — Group Mentor Guide**

Welcome to Week 13! This week, students move from basic API creation to implementing secure user authentication using **Passport.js**. They will explore how to manage user identities in a server-side rendered application using **sessions and cookies**.

### **Warm-Up (5–10 minutes)**
**Mindset: Accessibility (A11y)**
*   The internet is a powerful tool, but it can be a "huge stumbling block" if built without accessibility in mind. 
*   **Discussion:** Share a time when you wanted or needed something but didn't have access to it. How did that lack of access impact your life?
*   How can we, as developers, ensure that the "awesome things" we build are usable by everyone?

### **Check for Understanding (Theory)**
*   When is the **cookie-based** approach more secure than using JWTs? (Answer: When using a browser, because sensitive information like a JWT is not stored in local storage).
*   Why can't we use cookies when one server calls another server? (Answer: Because cookies only have meaning for browsers).
*   What is the difference between `passport.initialize()` and `passport.session()`? (Answer: `initialize()` sets up Passport to work with Express; `session()` checks the session cookie for a user ID and deserializes it into `req.user`).

### **Explore vs. Apply — Session Formats**
*   **Explore Sessions** → Walk through the "Passport Lifecycle." Explain how `serializeUser` saves an ID to a cookie and `deserializeUser` uses that ID to retrieve the full user object from the database.
*   **Apply Sessions** → Live-code the `authMiddleware` to demonstrate how to protect a route (like the "Secret Word" page) and redirect unauthenticated users.

###### **Sample Timing for 1-Hour Session**
| Time | Activity |
| :--- | :--- |
| 0:00–0:10 | Warm-up: Discussing the impact of accessibility in web development |
| 0:10–0:25 | Explore: The flow of cookie-based authentication and the LocalStrategy |
| 0:25–0:50 | Apply: Troubleshooting `passportInit.js` and configuring the `logon` route |
| 0:50–1:00 | Wrap-up: Checking the implementation of `storeLocals` for flash messages |

### **Check for Understanding (Ask 2–3)**
*   In the `LocalStrategy`, what are the `usernameField` and `passwordField` used for? (Answer: They tell Passport which fields in the `req.body` to look for—in this case, "email" and "password").
*   What are the three arguments accepted by the `done` callback in Passport? (Answer: 1. An error or null; 2. The user object or false; 3. An object with a message for flash notifications).
*   How do we check if a user is logged in within our EJS templates? (Answer: By checking if the `user` object exists, which is made available via `res.locals` in the `storeLocals` middleware).

### **Apply Prompts**
*   **JWT Removal:** Remind students to remove JWT references from `models/User.js`, as this lesson specifically uses sessions/cookies instead of tokens.
*   **Password Matching:** Ensure students implement the logic in `registerDo` to check if `password` and `password1` match before creating the user.
*   **Flash Messages:** If errors aren't appearing on the page, check if the student is correctly passing the `errors` variable in the `res.render` call within `registerDo`.
*   **Route Protection:** Remind students that `authMiddleware` must be added to the `app.use` statement for any route they wish to protect, such as `/secretWord`.
