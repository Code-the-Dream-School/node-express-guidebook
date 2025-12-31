# Week 6: Task Manager API Part 2 — Group Mentor Guide

Welcome to Week 6 of the Node.js course! This week, students are learning:

- How to handle URL parameters with Express  
- How to implement effective error handling in an API  
- How to add input validation for data robustness  
- How to expand CRUD functionality in the Task Manager API  
- How to use middleware for cleaner async code

Students are continuing the Task Manager API from last week, working in `03-task-manager/starter`.



## Warm-Up (5–10 minutes)

Choose one:

**Relationship-Building**  
- What’s the most confusing bug you’ve had to debug?  
- Share a time when good error messages saved you a lot of time.  

**💡 Check for Understanding (from last week)**  
- What’s the difference between route parameters and query parameters?  
- Why is it important to keep `.env` out of version control?  
- How can we use Postman to test error handling?



## Explore vs. Apply — Session Formats

**Explore Sessions** → Demo creating a route with `req.params`, wrapping async handlers to avoid repetitive `try/catch`, and sending meaningful status codes & messages.  

**Apply Sessions** → Students implement their own `GET /tasks/:id`, `PATCH /tasks/:id`, and `DELETE /tasks/:id` routes with validation and error handling.



## Sample Timing for 1-Hour Session

| Time      | Activity                                                        |
|--|--|
| 0:00–0:10 | Warm-up + review key concepts from Part 1                       |
| 0:10–0:25 | Explore: URL params, async wrapper, error handling              |
| 0:25–0:50 | Apply: students add/update routes and test in Postman           |
| 0:50–1:00 | Wrap-up + share lessons learned about debugging & validation    |



## Check for Understanding (Ask 2–3)

- What’s the purpose of an `asyncWrapper` middleware?  
- Why is it useful to create a custom error class like `CustomAPIError`?  
- When should an API return a `404` status code?  



## Explore Prompts

Show a `GET /tasks/:id` route that uses `asyncWrapper` and a custom error when a task isn’t found:

\`\`\`js
const getTask = asyncWrapper(async (req, res, next) => {
  const { id: taskID } = req.params;
  const task = await Task.findOne({ _id: taskID });
  if (!task) {
    return next(new CustomAPIError(`No task with id: ${taskID}`, 404));
  }
  res.status(200).json({ task });
});
\`\`\`

Walk through:
- How `req.params` works
- Why we use `return next()` with an error
- How the global error handler responds

Then show an example update route with validation:

\`\`\`js
const updateTask = asyncWrapper(async (req, res, next) => {
  const { id: taskID } = req.params;
  const task = await Task.findOneAndUpdate(
    { _id: taskID },
    req.body,
    { new: true, runValidators: true }
  );
  if (!task) {
    return next(new CustomAPIError(`No task with id: ${taskID}`, 404));
  }
  res.status(200).json({ task });
});
\`\`\`



## 🛠️ Apply Prompts (Live Coding & Troubleshooting)

### 🔧 Common Sticking Points
* Forgetting to call `runValidators: true` in update operations.  
* Not returning after calling `next()` with an error.  
* Using `findById` incorrectly without error handling.  
* Sending responses twice due to missing `return`.

### Try This Live

**Scenario:** Student’s `GET /tasks/:id` always returns 200, even if the task doesn’t exist.  
Ask: Are they checking `if (!task)` before sending the response? Are they properly using `next()` with an error?



## Engagement Strategies (for quiet groups)

- **Error Designer:** Give them a scenario and have them design the status code & message.  
- **Live Debug:** Show a route with broken error handling and have the group fix it.  
- **Postman Relay:** One student writes a failing request in Postman, another updates the code to make it pass.



## Optional Challenges

- Replace `asyncWrapper` with the `express-async-errors` package and compare.  
- Create validation middleware that rejects requests missing required fields.  
- Add a route to mark all tasks as completed in bulk.



**Mentor To-Do**  
- [ ] Run a session using this guide.  
- [ ] Ensure students test both success and failure cases in Postman.  
- [ ] Submit your [Mentor Session Report](https://airtable.com/appoSRJMlXH9KvE6w/shrp0jjRtoMyTXRzh).
