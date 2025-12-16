# Week 5: Task Manager API Part 1 - Assignment Review Guide

## Assignment Overview
This week students follow a video tutorial (CodingAddict's Node/Express Projects, 0:00:00 to 1:28:45) to build the first part of a Task Manager API. They set up a MongoDB database, connect it to their Express app, and implement basic CRUD operations. This is their first exposure to databases and NoSQL, making it a challenging but foundational week.

**Key Learning Objectives:**
- Set up MongoDB Atlas (cloud database)
- Connect Express app to MongoDB using Mongoose
- Create a Task model with Mongoose schema
- Implement CRUD API endpoints (Create, Read, Update, Delete)
- Test API endpoints using Postman



## Review Checklist

### Repository & Git Workflow
- [ ] Student merged week 4 to main before starting
- [ ] Work is on a `week5` branch
- [ ] Work is in `03-task-manager/starter` directory
- [ ] `.env` file is NOT committed to GitHub
- [ ] `.gitignore` includes `.env` and `/node_modules`
- [ ] No MongoDB credentials visible in committed code
- [ ] Pull request created from `week5` to `main`

### MongoDB Setup
- [ ] Student has MongoDB Atlas account set up
- [ ] Database cluster created
- [ ] Database user created with password
- [ ] Connection string properly stored in `.env` file
- [ ] App successfully connects to MongoDB (no connection errors)

### File Structure
- [ ] `models/Task.js` exists with Task schema
- [ ] `controllers/tasks.js` exists with controller functions
- [ ] `routes/tasks.js` exists with route definitions
- [ ] `db/connect.js` exists with database connection logic
- [ ] `.env` file exists locally (but not in repo)
- [ ] `app.js` properly configured with routes and middleware

### API Endpoints (Should all work in Postman)
- [ ] **GET /api/v1/tasks** - Returns all tasks
- [ ] **POST /api/v1/tasks** - Creates a new task
- [ ] **GET /api/v1/tasks/:id** - Returns single task by ID
- [ ] **PATCH /api/v1/tasks/:id** - Updates a task
- [ ] **DELETE /api/v1/tasks/:id** - Deletes a task

### Code Quality
- [ ] Task model has required fields (name, completed)
- [ ] Routes properly connected to controllers
- [ ] Error handling present (even if basic)
- [ ] Async/await used correctly with try-catch blocks
- [ ] Code follows tutorial structure reasonably well



## What to Look For in the Code

### 1. Environment Variables (.env file)
**This file should NOT be in the repo, but students should have it locally:**

```
MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/task-manager?retryWrites=true&w=majority
```

**Check that:**
- The `.env` file is in `.gitignore`
- No MongoDB credentials are hardcoded in any JavaScript files
- The connection string is properly formatted



### 2. Database Connection (db/connect.js)

```javascript
const mongoose = require('mongoose');

const connectDB = (url) => {
  return mongoose.connect(url, {
    useNewUrlParser: true,
    useCreateIndex: true,
    useFindAndModify: false,
    useUnifiedTopology: true,
  });
};

module.exports = connectDB;
```

**Common issues:**
- Missing `return` statement
- Not exporting the function
- Connection options might vary (some deprecated in newer Mongoose versions)



### 3. Task Model (models/Task.js)

```javascript
const mongoose = require('mongoose');

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

module.exports = mongoose.model('Task', TaskSchema);
```

**What to verify:**
- Schema exported as a model
- `name` field is required and has validation
- `completed` field defaults to false
- Basic validation messages present



### 4. Controllers (controllers/tasks.js)

Should contain 5 controller functions:

```javascript
const Task = require('../models/Task');

const getAllTasks = async (req, res) => {
  try {
    const tasks = await Task.find({});
    res.status(200).json({ tasks });
  } catch (error) {
    res.status(500).json({ msg: error });
  }
};

const createTask = async (req, res) => {
  try {
    const task = await Task.create(req.body);
    res.status(201).json({ task });
  } catch (error) {
    res.status(500).json({ msg: error });
  }
};

const getTask = async (req, res) => {
  try {
    const { id: taskID } = req.params;
    const task = await Task.findOne({ _id: taskID });
    
    if (!task) {
      return res.status(404).json({ msg: `No task with id: ${taskID}` });
    }
    
    res.status(200).json({ task });
  } catch (error) {
    res.status(500).json({ msg: error });
  }
};

const updateTask = async (req, res) => {
  try {
    const { id: taskID } = req.params;
    const task = await Task.findOneAndUpdate({ _id: taskID }, req.body, {
      new: true,
      runValidators: true,
    });
    
    if (!task) {
      return res.status(404).json({ msg: `No task with id: ${taskID}` });
    }
    
    res.status(200).json({ task });
  } catch (error) {
    res.status(500).json({ msg: error });
  }
};

const deleteTask = async (req, res) => {
  try {
    const { id: taskID } = req.params;
    const task = await Task.findOneAndDelete({ _id: taskID });
    
    if (!task) {
      return res.status(404).json({ msg: `No task with id: ${taskID}` });
    }
    
    res.status(200).json({ task });
  } catch (error) {
    res.status(500).json({ msg: error });
  }
};

module.exports = {
  getAllTasks,
  createTask,
  getTask,
  updateTask,
  deleteTask,
};
```

**What to verify:**
- All 5 functions present and exported
- Try-catch blocks for error handling
- Proper use of async/await
- Correct Mongoose methods (`.find()`, `.create()`, `.findOne()`, etc.)
- 404 responses for missing tasks



### 5. Routes (routes/tasks.js)

```javascript
const express = require('express');
const router = express.Router();

const {
  getAllTasks,
  createTask,
  getTask,
  updateTask,
  deleteTask,
} = require('../controllers/tasks');

router.route('/').get(getAllTasks).post(createTask);
router.route('/:id').get(getTask).patch(updateTask).delete(deleteTask);

module.exports = router;
```

**What to verify:**
- Routes properly import controllers
- Correct HTTP methods (GET, POST, PATCH, DELETE)
- `:id` parameter for single-task routes
- Router exported



### 6. Main App File (app.js)

```javascript
const express = require('express');
const app = express();
const tasks = require('./routes/tasks');
const connectDB = require('./db/connect');
require('dotenv').config();

// middleware
app.use(express.static('./public'));
app.use(express.json());

// routes
app.use('/api/v1/tasks', tasks);

const port = 3000;

const start = async () => {
  try {
    await connectDB(process.env.MONGO_URI);
    app.listen(port, console.log(`Server is listening on port ${port}...`));
  } catch (error) {
    console.log(error);
  }
};

start();
```

**What to verify:**
- `dotenv` configured before using `process.env`
- Database connection before starting server
- Routes mounted at correct path
- Middleware for JSON parsing
- Static files middleware for serving frontend (if included)



## Testing with Postman

Students should be able to demonstrate these working:

### 1. Create a Task (POST)
**Request:**
```
POST http://localhost:3000/api/v1/tasks
Body (JSON):
{
  "name": "Test task"
}
```

**Expected Response (201):**
```json
{
  "task": {
    "_id": "507f1f77bcf86cd799439011",
    "name": "Test task",
    "completed": false,
    "__v": 0
  }
}
```



### 2. Get All Tasks (GET)
**Request:**
```
GET http://localhost:3000/api/v1/tasks
```

**Expected Response (200):**
```json
{
  "tasks": [
    {
      "_id": "507f1f77bcf86cd799439011",
      "name": "Test task",
      "completed": false,
      "__v": 0
    }
  ]
}
```



### 3. Get Single Task (GET)
**Request:**
```
GET http://localhost:3000/api/v1/tasks/507f1f77bcf86cd799439011
```

**Expected Response (200):**
```json
{
  "task": {
    "_id": "507f1f77bcf86cd799439011",
    "name": "Test task",
    "completed": false,
    "__v": 0
  }
}
```



### 4. Update Task (PATCH)
**Request:**
```
PATCH http://localhost:3000/api/v1/tasks/507f1f77bcf86cd799439011
Body (JSON):
{
  "completed": true
}
```

**Expected Response (200):**
```json
{
  "task": {
    "_id": "507f1f77bcf86cd799439011",
    "name": "Test task",
    "completed": true,
    "__v": 0
  }
}
```



### 5. Delete Task (DELETE)
**Request:**
```
DELETE http://localhost:3000/api/v1/tasks/507f1f77bcf86cd799439011
```

**Expected Response (200):**
```json
{
  "task": {
    "_id": "507f1f77bcf86cd799439011",
    "name": "Test task",
    "completed": true,
    "__v": 0
  }
}
```

