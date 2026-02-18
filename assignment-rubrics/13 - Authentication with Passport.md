## **Lesson 13: Authentication with Passport — Assignment Review Guide**

### **Assignment Rubric**
You can mark the student's assignment as complete if they:
*   [ ] **Branching:** Created and submitted their work on the `lesson13` branch.
*   [ ] **Database Connection:** Successfully connected the application to MongoDB at startup.
*   [ ] **Passport Configuration:** Implemented `passportInit.js` with `LocalStrategy`, `serializeUser`, and `deserializeUser`.
*   [ ] **Views & Partials:** Created `index.ejs`, `logon.ejs`, and `register.ejs` using the correct partials.
*   [ ] **Authentication Flow:** Users can successfully register, log on, and log off.
*   [ ] **Middleware:** Implemented `storeLocals` to handle `res.locals.user` and `flash` messages.
*   [ ] **Route Protection:** Used `authMiddleware` to prevent unauthenticated access to the `/secretWord` route.
*   [ ] **Mindset:** Submitted "N/A" for the mindset response as instructed, focusing on the lesson content.

### **What to Look For**
*   **Passport Integration:** Ensure `app.use(passport.initialize())` and `app.use(passport.session())` are placed *after* the session middleware in `app.js`.
*   **EJS Logic:** Verify that the header partial correctly displays the logged-in user's name and a "Logoff" button only when authenticated.
*   **Error Handling:** Check that `parseValidationErrors.js` is used to return helpful Mongoose validation messages to the user.
*   **Security:** Ensure the logon form uses `method="POST"` and the password input uses `type="password"` to hide characters.

### **Stretch Goals (Optional)**
*   [ ] Did the student implement additional password strength validation?.
*   [ ] Did the student explore the "Hungry for More" TypeScript documentation?.
