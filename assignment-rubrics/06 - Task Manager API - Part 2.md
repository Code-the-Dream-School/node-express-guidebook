# Week 6: Task Manager API Part 2 - Assignment Review Guide

## Assignment Overview
This week students continue building the Task Manager API, adding crucial production-ready features: proper error handling, input validation, and additional CRUD operations. They follow the FreeCodeCamp video from 1:29 to 3:07, implementing async wrapper middleware, custom error classes, validation middleware, and enhanced controller logic. Students also answer two conceptual questions in `QuizAnswers2.txt`.

**Key Learning Objectives:**
- Implement async error handling with middleware
- Create custom error classes
- Add input validation with express-validator or Joi
- Handle edge cases (missing tasks, invalid IDs, validation errors)
- Understand HTTP status codes for different error scenarios



## Review Checklist

### Repository & Git Workflow
- [ ] Work is on a `week6` branch (created from main after merging week5)
- [ ] Work continues in `03-task-manager/starter` directory
- [ ] `.env` file still NOT committed to GitHub
- [ ] Pull request created from `week6` to `main`
- [ ] `QuizAnswers2.txt` file exists with answers to both questions

### Error Handling Implementation
- [ ] `asyncWrapper` middleware created (or `express-async-errors` installed)
- [ ] Custom error classes created (`CustomAPIError`, `BadRequestError`, `NotFoundError`)
- [ ] Error handler middleware implemented
- [ ] All async route handlers wrapped properly
- [ ] Proper status codes returned for different errors

### Validation
- [ ] Validation middleware added (express-validator or Joi)
- [ ] Task name validation (required, max length)
- [ ] Validation errors return 400 status
- [ ] Validation messages are clear and helpful

### CRUD Operations Enhanced
- [ ] GET /api/v1/tasks - Returns all tasks (unchanged)
- [ ] POST /api/v1/tasks - Creates task with validation
- [ ] GET /api/v1/tasks/:id - Returns task or 404 if not found
- [ ] PATCH /api/v1/tasks/:id - Updates task with validation
- [ ] DELETE /api/v1/tasks/:id - Deletes task or 404 if not found
- [ ] All endpoints handle errors gracefully

### Quiz Answers Quality
- [ ] Question 1 answered (purpose of asyncWrapper)
- [ ] Question 2 completed (code for custom error handling)
- [ ] Answers demonstrate understanding of concepts



## What to Look For in the Code

### 1. Async Wrapper Middleware

**Option A: Custom asyncWrapper**

```javascript
// middleware/async.js
const asyncWrapper = (fn) => {
  return async (req, res, next) => {
    try {
      await fn(req, res, next);
    } catch (error) {
      next(error);
    }
  };
};

module.exports = asyncWrapper;
```

**What to verify:**
- Takes a function as parameter
- Returns async function
- Wraps in try-catch
- Calls `next(error)` on error
- Exported properly

**Option B: express-async-errors package**

```javascript
// app.js (at the top, before routes)
require('express-async-errors');
```

**What to verify:**
- Installed: `npm install express-async-errors`
- Required before route definitions
- No asyncWrapper needed in controllers



### 2. Custom Error Classes

```javascript
// errors/custom-error.js
class CustomAPIError extends Error {
  constructor(message, statusCode) {
    super(message);
    this.statusCode = statusCode;
  }
}

module.exports = CustomAPIError;
```

**Enhanced version with specific error types:**

```javascript
// errors/custom-error.js
class CustomAPIError extends Error {
  constructor(message) {
    super(message);
  }
}

class NotFoundError extends CustomAPIError {
  constructor(message) {
    super(message);
    this.statusCode = 404;
  }
}

class BadRequestError extends CustomAPIError {
  constructor(message) {
    super(message);
    this.statusCode = 400;
  }
}

module.exports = { CustomAPIError, NotFoundError, BadRequestError };
```

**What to verify:**
- Extends Error class
- Has statusCode property
- Specific error classes (NotFoundError, BadRequestError) are optional but good
- Properly exported



### 3. Error Handler Middleware

```javascript
// middleware/error-handler.js
const { CustomAPIError } = require('../errors/custom-error');

const errorHandlerMiddleware = (err, req, res, next) => {
  if (err instanceof CustomAPIError) {
    return res.status(err.statusCode).json({ msg: err.message });
  }
  return res.status(500).json({ msg: 'Something went wrong, please try again' });
};

module.exports = errorHandlerMiddleware;
```

**What to verify:**
- Four parameters (err, req, res, next)
- Checks if error is CustomAPIError
- Returns appropriate status code
- Has fallback for unexpected errors (500)
- Placed after routes in app.js



### 4. Enhanced Controllers with Error Handling

```javascript
// controllers/tasks.js
const Task = require('../models/Task');
const asyncWrapper = require('../middleware/async');
const { createCustomError } = require('../errors/custom-error');

const getTask = asyncWrapper(async (req, res, next) => {
  const { id: taskID } = req.params;
  const task = await Task.findOne({ _id: taskID });
  
  if (!task) {
    return next(createCustomError(`No task with id: ${taskID}`, 404));
  }
  
  res.status(200).json({ task });
});

const createTask = asyncWrapper(async (req, res) => {
  const task = await Task.create(req.body);
  res.status(201).json({ task });
});

const updateTask = asyncWrapper(async (req, res, next) => {
  const { id: taskID } = req.params;
  const task = await Task.findOneAndUpdate(
    { _id: taskID },
    req.body,
    {
      new: true,
      runValidators: true,
    }
  );
  
  if (!task) {
    return next(createCustomError(`No task with id: ${taskID}`, 404));
  }
  
  res.status(200).json({ task });
});

const deleteTask = asyncWrapper(async (req, res, next) => {
  const { id: taskID } = req.params;
  const task = await Task.findOneAndDelete({ _id: taskID });
  
  if (!task) {
    return next(createCustomError(`No task with id: ${taskID}`, 404));
  }
  
  res.status(200).json({ task });
});

module.exports = {
  getAllTasks,
  createTask,
  getTask,
  updateTask,
  deleteTask,
};
```

**What to verify:**
- All async functions wrapped with asyncWrapper (or using express-async-errors)
- 404 errors thrown when task not found
- `next()` called with custom errors
- `runValidators: true` in updates
- Proper status codes (200, 201, 404)



### 5. Validation Implementation

**Option A: Using Joi**

```javascript
// Install: npm install joi

// Example in controller or separate validation file
const Joi = require('joi');

const taskSchema = Joi.object({
  name: Joi.string().required().max(20),
  completed: Joi.boolean()
});

// In controller
const { error } = taskSchema.validate(req.body);
if (error) {
  throw new BadRequestError(error.details[0].message);
}
```

**Option B: Using express-validator**

```javascript
// Install: npm install express-validator

// middleware/validation.js
const { body, validationResult } = require('express-validator');

const validateTask = [
  body('name')
    .trim()
    .notEmpty().withMessage('Name is required')
    .isLength({ max: 20 }).withMessage('Name cannot be more than 20 characters'),
  (req, res, next) => {
    const errors = validationResult(req);
    if (!errors.isEmpty()) {
      return res.status(400).json({ errors: errors.array() });
    }
    next();
  }
];

module.exports = { validateTask };

// In routes
router.route('/').post(validateTask, createTask);
```

**Option C: Mongoose validation only**

```javascript
// models/Task.js
const TaskSchema = new mongoose.Schema({
  name: {
    type: String,
    required: [true, 'must provide name'],
    trim: true,
    maxlength: [20, 'name can not be more than 20 characters'],
  },
  completed: {
    type: Boolean,
    default: false,
  },
});
```

**What to verify:**
- Some form of validation present
- Name is required
- Name has max length (usually 20)
- Validation errors return 400 status
- Error messages are helpful



### 6. App.js Configuration

```javascript
// app.js
const express = require('express');
const app = express();
const tasks = require('./routes/tasks');
const connectDB = require('./db/connect');
require('dotenv').config();

// If using express-async-errors
require('express-async-errors');

// Middleware
const notFound = require('./middleware/not-found');
const errorHandlerMiddleware = require('./middleware/error-handler');

app.use(express.static('./public'));
app.use(express.json());

// Routes
app.use('/api/v1/tasks', tasks);

// Error handling middleware (must be AFTER routes)
app.use(notFound);
app.use(errorHandlerMiddleware);

const port = process.env.PORT || 3000;

const start = async () => {
  try {
    await connectDB(process.env.MONGO_URI);
    app.listen(port, () =>
      console.log(`Server is listening on port ${port}...`)
    );
  } catch (error) {
    console.log(error);
  }
};

start();
```

**What to verify:**
- Error middleware placed AFTER routes
- notFound middleware for 404s
- errorHandlerMiddleware for error handling
- If using express-async-errors, required at top



### 7. Not Found Middleware

```javascript
// middleware/not-found.js
const notFound = (req, res) => res.status(404).send('Route does not exist');

module.exports = notFound;
```
