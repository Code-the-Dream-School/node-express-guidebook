# Week 5: Task Manager API Part 1 — Group Mentor Guide

Welcome to Week 5 of the Node.js course! This week, students are learning:

- How to set up a MongoDB Atlas cloud database and connect it to a Node/Express app  
- How to create an API for a task manager with basic CRUD operations  
- How to use Postman to test routes during development  
- How to keep secrets safe with `.env` and `.gitignore`  
- *(Optional)* How to review JavaScript Array methods for use in the API

Students will start implementing the back end for the task manager in the `03-task-manager/starter` directory.

---

## 🧊 Warm-Up (5–10 minutes)

Choose one:

**👋 Relationship-Building**  
- What’s a tool you can’t live without when building something?  
- What’s a recent “aha” moment you had while coding?  

**💡 Check for Understanding (from last week)**  
- What is an API?  
- What is the purpose of `npm install` in a project?  
- How does Postman help when testing a back-end API?

---

## 🧭 Explore vs. Apply — Session Formats

**Explore Sessions** → Walk through setting up MongoDB Atlas, connecting with Mongoose, and creating the first Express route. Show testing with Postman.  

**Apply Sessions** → Students set up their own DB connection and implement a simple `GET` and `POST` route for tasks.

---

## ⏱️ Sample Timing for 1-Hour Session

| Time      | Activity                                               |
|-----------|--------------------------------------------------------|
| 0:00–0:10 | Warm-up + review of key concepts                       |
| 0:10–0:25 | Explore: Mongo connection + first route                |
| 0:25–0:50 | Apply: students create and test their own routes       |
| 0:50–1:00 | Wrap-up + reminders about `.env` and pushing to GitHub |

---

## ❓ Check for Understanding (Ask 2–3)

- Why should we store secrets like MongoDB URIs in a `.env` file?  
- What’s the difference between `app.get()` and `app.post()` in Express?  
- How can we confirm that our API is connected to MongoDB?

---

## 🧑‍🏫 Explore Prompts

Show a minimal setup for connecting to MongoDB and defining the first route:

\`\`\`js
// server.js
require('dotenv').config();
const express = require('express');
const mongoose = require('mongoose');

const app = express();
app.use(express.json());

const PORT = process.env.PORT || 3000;

mongoose
  .connect(process.env.MONGO_URI)
  .then(() => console.log('Connected to DB'))
  .catch(err => console.error(err));

app.get('/api/v1/tasks', (req, res) => {
  res.send('List of tasks will go here');
});

app.listen(PORT, () => console.log(`Server running on port ${PORT}`));
\`\`\`

Demo using Postman to send a GET request to `/api/v1/tasks`.

---

## 🛠️ Apply Prompts (Live Coding & Troubleshooting)

### 🔧 Common Sticking Points
* Forgetting to run `npm install` in the starter directory.  
* Not restarting the server after adding `.env` support.  
* Missing `app.use(express.json())` causing empty `req.body` on POST.  
* Pushing `.env` to GitHub (stress checking `.gitignore`).

### ✅ Try This Live

**Scenario:** Student’s API returns “Could not connect to DB.”  
Ask: Is their Mongo URI correct? Did they whitelist their IP address in MongoDB Atlas? Is `.env` being loaded?

---

## 💬 Engagement Strategies (for quiet groups)

- **Request Builder:** Have students suggest new routes to add (`GET /tasks/:id`, `DELETE /tasks/:id`).  
- **Postman Pair Test:** One student runs the server, another sends requests from Postman.  
- **Error Hunt:** Show a snippet with a bug (e.g., missing `await` in DB call) and ask them to debug.

---

## 💡 Optional Challenges

- Complete the optional Array Methods review file in `03-task-manager/optionalArrayMethodsReviewExtraAssignment.js`.  
- Implement `GET /tasks/:id` to retrieve a single task from Mongo.  
- Sign up for LeetCode or HackerRank and solve the FizzBuzz challenge.

---

✅ **Mentor To-Do**  
- [ ] Run a session using this guide.  
- [ ] Ensure students can connect to MongoDB and test a route in Postman.  
- [ ] Submit your [Mentor Session Report](https://airtable.com/appoSRJMlXH9KvE6w/shrp0jjRtoMyTXRzh).
