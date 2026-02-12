

### **Assignment Review Guide**

#### **Lesson 14: Server-Side Rendering with EJS**
| Week | Topic | Learning Objective |
| ------ | ------ | ------ |
| 14 | SSR with EJS | Students will build a server-side rendered application using EJS templates, implement session persistence with MongoDB, and use flash messages for user feedback. |

#### **Assignment Rubric**
You can mark the student's assignment as complete if they:
*   [ ] Created a new, independent `jobs-ejs` repository and associated it with GitHub.
*   [ ] Corrected the `.gitignore` to protect `.env` and `node_modules`.
*   [ ] Configured `app.js` to use **EJS** as the view engine.
*   [ ] Implemented **partials** for `head`, `header`, and `footer`.
*   [ ] Set up **Express Sessions** using `connect-mongodb-session` for storage.
*   [ ] Successfully implemented **Flash Messages** using `connect-flash`.
*   [ ] Created a functional `/secretWord` route that persists across server restarts.
*   [ ] Answered the mindset prompts regarding **Visual Hierarchy**.

#### **What to Look For**
*   **EJS Tag Usage:** Verify they used `<%- include(...) %>` for partials and `<%= secretWord %>` for data output.
*   **Session Persistence:** If you test their app locally, the "secret word" should remain the same even after killing and restarting the server.
*   **Middleware Order:** Check `app.js` to ensure `app.use(session(...))` appears before `app.use(flash())` and both appear before any routes.
*   **Security:** Ensure the `SESSION_SECRET` is pulled from `process.env` and not hardcoded.

#### **Sample Code Reference**
*Required Session Setup:*
```javascript
app.use(session({
  secret: process.env.SESSION_SECRET,
  resave: true,
  saveUninitialized: true,
  store: store // MongoDB store
}));
```

*Required Flash Logic in View:*
```html
<% if (errors) { 
  errors.forEach((err) => { %>
    <div>Error: <%= err %></div>
<% }) } %>
```
