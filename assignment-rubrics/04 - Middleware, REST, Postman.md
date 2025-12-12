# Week 04: Middleware, REST Methods & Postman — Assignment Review Guide

**Learning objective**: Students will learn about middleware, HTTP methods (GET, POST, PUT, DELETE), testing with Postman, refactoring code into routes and controllers, and front-end interaction with APIs.

You can mark the student's assignment as complete if they: 

- [ ] Have created the `week4` branch and submitted a pull request
- [ ] Implemented a `logger` middleware function that logs method, URL, and time
- [ ] Created GET and POST endpoints for `/api/v1/people`
- [ ] Properly parsed request bodies using `express.urlencoded()` and `express.json()`
- [ ] Refactored code into separate `routes/people.js` and `controllers/people.js` files
- [ ] Implemented GET by ID, PUT, and DELETE endpoints for people
- [ ] All endpoints return appropriate HTTP status codes
- [ ] Code follows Express.js best practices

## Sample Solution Code

### app.js (Main Application File)

```javascript
const express = require('express');
const app = express();
const { products, people } = require('./data');

// Logger middleware
const logger = (req, res, next) => {
  const method = req.method;
  const url = req.url;
  const time = new Date().toLocaleString();
  console.log(`[${time}] ${method} ${url}`);
  next();
};

// Middleware - must come before routes that need it
app.use(logger); // Apply logger to all routes
app.use(express.urlencoded({ extended: false })); // Parse URL-encoded bodies
app.use(express.json()); // Parse JSON bodies
app.use(express.static('./methods-public')); // Serve static files

// Import routers
const peopleRouter = require('./routes/people');

// Use routers
app.use('/api/v1/people', peopleRouter);

// Products route (not refactored - optional)
app.get('/api/v1/products', (req, res) => {
  res.json(products);
});

// Start server
const PORT = 3000;
app.listen(PORT, () => {
  console.log(`Server is listening on port ${PORT}...`);
});
```

### routes/people.js (Router File)

```javascript
const express = require('express');
const router = express.Router();

const {
  getPeople,
  addPerson,
  getPersonById,
  updatePerson,
  deletePerson
} = require('../controllers/people');

// GET all people - /api/v1/people
router.get('/', getPeople);

// POST new person - /api/v1/people
router.post('/', addPerson);

// GET person by ID - /api/v1/people/:id
router.get('/:id', getPersonById);

// PUT (update) person - /api/v1/people/:id
router.put('/:id', updatePerson);

// DELETE person - /api/v1/people/:id
router.delete('/:id', deletePerson);

module.exports = router;
```

### controllers/people.js (Controller File)

```javascript
let { people } = require('../data');

// GET all people
const getPeople = (req, res) => {
  res.status(200).json({ success: true, data: people });
};

// POST - Add new person
const addPerson = (req, res) => {
  const { name } = req.body;
  
  if (!name) {
    return res.status(400).json({ 
      success: false, 
      message: 'Please provide a name' 
    });
  }
  
  const newPerson = {
    id: people.length + 1,
    name: name
  };
  
  people.push(newPerson);
  
  res.status(201).json({ 
    success: true, 
    name: name 
  });
};

// GET person by ID
const getPersonById = (req, res) => {
  const { id } = req.params;
  const personId = parseInt(id);
  
  const person = people.find((p) => p.id === personId);
  
  if (!person) {
    return res.status(404).json({ 
      success: false, 
      message: `No person with id ${id}` 
    });
  }
  
  res.status(200).json({ success: true, data: person });
};

// PUT - Update person
const updatePerson = (req, res) => {
  const { id } = req.params;
  const { name } = req.body;
  const personId = parseInt(id);
  
  const person = people.find((p) => p.id === personId);
  
  if (!person) {
    return res.status(404).json({ 
      success: false, 
      message: `No person with id ${id}` 
    });
  }
  
  if (!name) {
    return res.status(400).json({ 
      success: false, 
      message: 'Please provide a name' 
    });
  }
  
  // Update the person's name
  person.name = name;
  
  res.status(200).json({ 
    success: true, 
    data: person 
  });
};

// DELETE person
const deletePerson = (req, res) => {
  const { id } = req.params;
  const personId = parseInt(id);
  
  const person = people.find((p) => p.id === personId);
  
  if (!person) {
    return res.status(404).json({ 
      success: false, 
      message: `No person with id ${id}` 
    });
  }
  
  // Filter out the person to delete
  people = people.filter((p) => p.id !== personId);
  
  res.status(200).json({ 
    success: true, 
    data: people 
  });
};

module.exports = {
  getPeople,
  addPerson,
  getPersonById,
  updatePerson,
  deletePerson
};
```

## Optional Assignment: Cookie Authentication

### app.js (Additional Code)

```javascript
const cookieParser = require('cookie-parser');

// Add after body parsing middleware
app.use(cookieParser());

// Auth middleware
const auth = (req, res, next) => {
  if (req.cookies.name) {
    req.user = req.cookies.name;
    next();
  } else {
    res.status(401).json({ 
      success: false, 
      message: 'Unauthorized' 
    });
  }
};

// Logon endpoint
app.post('/logon', (req, res) => {
  const { name } = req.body;
  
  if (!name) {
    return res.status(400).json({ 
      success: false, 
      message: 'Please provide a name' 
    });
  }
  
  res.cookie('name', name);
  res.status(201).json({ 
    success: true, 
    message: `Hello, ${name}!` 
  });
});

// Logoff endpoint
app.delete('/logoff', (req, res) => {
  res.clearCookie('name');
  res.status(200).json({ 
    success: true, 
    message: 'You are now logged off' 
  });
});

// Test endpoint with auth
app.get('/test', auth, (req, res) => {
  res.status(200).json({ 
    success: true, 
    message: `Welcome, ${req.user}!` 
  });
});
```

## Expected Postman Test Results

### GET /api/v1/people
**Request:**
```
GET http://localhost:3000/api/v1/people
```

**Response:** `200 OK`
```json
{
  "success": true,
  "data": [
    { "id": 1, "name": "john" },
    { "id": 2, "name": "peter" },
    { "id": 3, "name": "susan" },
    { "id": 4, "name": "anna" },
    { "id": 5, "name": "emma" }
  ]
}
```

### POST /api/v1/people
**Request:**
```
POST http://localhost:3000/api/v1/people
Content-Type: application/json

{
  "name": "alice"
}
```

**Response:** `201 Created`
```json
{
  "success": true,
  "name": "alice"
}
```

### POST /api/v1/people (Error - Missing Name)
**Request:**
```
POST http://localhost:3000/api/v1/people
Content-Type: application/json

{}
```

**Response:** `400 Bad Request`
```json
{
  "success": false,
  "message": "Please provide a name"
}
```

### GET /api/v1/people/:id
**Request:**
```
GET http://localhost:3000/api/v1/people/1
```

**Response:** `200 OK`
```json
{
  "success": true,
  "data": { "id": 1, "name": "john" }
}
```

### GET /api/v1/people/:id (Not Found)
**Request:**
```
GET http://localhost:3000/api/v1/people/999
```

**Response:** `404 Not Found`
```json
{
  "success": false,
  "message": "No person with id 999"
}
```

### PUT /api/v1/people/:id
**Request:**
```
PUT http://localhost:3000/api/v1/people/1
Content-Type: application/json

{
  "name": "Johnny"
}
```

**Response:** `200 OK`
```json
{
  "success": true,
  "data": { "id": 1, "name": "Johnny" }
}
```

### DELETE /api/v1/people/:id
**Request:**
```
DELETE http://localhost:3000/api/v1/people/1
```

**Response:** `200 OK`
```json
{
  "success": true,
  "data": [
    { "id": 2, "name": "peter" },
    { "id": 3, "name": "susan" },
    { "id": 4, "name": "anna" },
    { "id": 5, "name": "emma" }
  ]
}
```

## Common Student Errors & Solutions

### Middleware Issues

**Error**: Logger middleware not working
```javascript
// ❌ WRONG - Not calling next()
const logger = (req, res, next) => {
  console.log(req.method, req.url);
  // Missing next()!
};

// ✅ CORRECT - Must call next()
const logger = (req, res, next) => {
  console.log(req.method, req.url, new Date().toLocaleString());
  next(); // Required!
};
```

**Error**: Middleware order issues
```javascript
// ❌ WRONG - Body parser after routes
app.use('/api/v1/people', peopleRouter);
app.use(express.json()); // Too late!

// ✅ CORRECT - Body parser before routes
app.use(express.json());
app.use('/api/v1/people', peopleRouter);
```

### Request Body Parsing Issues

**Error**: req.body is undefined
```javascript
// ❌ WRONG - Missing body parsing middleware
app.post('/api/v1/people', (req, res) => {
  console.log(req.body); // undefined!
});

// ✅ CORRECT - Add body parsing first
app.use(express.urlencoded({ extended: false }));
app.use(express.json());

app.post('/api/v1/people', (req, res) => {
  console.log(req.body); // Works!
});
```

### Status Code Errors

**Error**: Using wrong status codes
```javascript
// ❌ WRONG status codes
res.status(200).json({ message: 'Created' }); // Should be 201
res.status(200).json({ message: 'Not found' }); // Should be 404
res.status(500).json({ message: 'Bad request' }); // Should be 400

// ✅ CORRECT status codes
res.status(201).json({ success: true }); // Created
res.status(404).json({ success: false }); // Not Found
res.status(400).json({ success: false }); // Bad Request
res.status(200).json({ success: true }); // OK
```

### Router Refactoring Issues

**Error**: Wrong path in router
```javascript
// ❌ WRONG - Using full path in router
// routes/people.js
router.get('/api/v1/people', getPeople); // Wrong!

// app.js
app.use('/api/v1/people', peopleRouter);
// Results in /api/v1/people/api/v1/people

// ✅ CORRECT - Use relative path in router
// routes/people.js
router.get('/', getPeople); // Correct!

// app.js
app.use('/api/v1/people', peopleRouter);
// Results in /api/v1/people
```

**Error**: Not exporting router
```javascript
// ❌ WRONG - Missing export
// routes/people.js
const router = express.Router();
router.get('/', getPeople);
// No module.exports!

// ✅ CORRECT - Export router
const router = express.Router();
router.get('/', getPeople);
module.exports = router;
```

### Parameter Handling Issues

**Error**: Not converting ID to number
```javascript
// ❌ WRONG - Comparing string to number
const getPersonById = (req, res) => {
  const { id } = req.params; // id is a string!
  const person = people.find((p) => p.id === id); // Won't match!
};

// ✅ CORRECT - Convert to number first
const getPersonById = (req, res) => {
  const { id } = req.params;
  const personId = parseInt(id); // Convert to number
  const person = people.find((p) => p.id === personId);
};
```

### Array Mutation Issues

**Error**: Not properly removing items
```javascript
// ❌ WRONG - Modifying array incorrectly
const deletePerson = (req, res) => {
  const index = people.findIndex((p) => p.id === personId);
  people.splice(index, 1); // Works but less clear
};

// ✅ BETTER - Using filter
const deletePerson = (req, res) => {
  people = people.filter((p) => p.id !== personId);
  res.status(200).json({ success: true, data: people });
};
```

### Missing Error Handling

**Error**: Not handling missing data
```javascript
// ❌ WRONG - No validation
const addPerson = (req, res) => {
  const newPerson = {
    id: people.length + 1,
    name: req.body.name // What if name is undefined?
  };
  people.push(newPerson);
  res.status(201).json({ success: true });
};

// ✅ CORRECT - Validate input
const addPerson = (req, res) => {
  const { name } = req.body;
  
  if (!name) {
    return res.status(400).json({ 
      success: false, 
      message: 'Please provide a name' 
    });
  }
  
  // Continue with valid data...
};
```

### Optional Assignment Issues

**Error**: Not checking for cookie in auth middleware
```javascript
// ❌ WRONG - Always calls next()
const auth = (req, res, next) => {
  req.user = req.cookies.name;
  next(); // Always continues, even if no cookie!
};

// ✅ CORRECT - Check if cookie exists
const auth = (req, res, next) => {
  if (req.cookies.name) {
    req.user = req.cookies.name;
    next();
  } else {
    res.status(401).json({ 
      success: false, 
      message: 'Unauthorized' 
    });
    // Don't call next() here!
  }
};
```

## Key Concepts to Verify

### Middleware Understanding
- Student knows middleware functions take `(req, res, next)` parameters
- Student calls `next()` to pass control to next middleware/route
- Student understands middleware order matters
- Student can apply middleware globally with `app.use()` or to specific routes

### HTTP Method Understanding
- **GET**: Retrieve data (200 OK)
- **POST**: Create new resource (201 Created)
- **PUT**: Update existing resource (200 OK)
- **DELETE**: Remove resource (200 OK)
- **Error responses**: 400 (Bad Request), 404 (Not Found), 401 (Unauthorized)

### Refactoring Skills
- Separated concerns: routes define endpoints, controllers handle logic
- Proper module exports and imports
- Router paths are relative to mount point in `app.use()`
- Controller functions handle all request/response logic

### Request Handling
- Body parsing with `express.json()` and `express.urlencoded()`
- Accessing route parameters with `req.params`
- Accessing request body with `req.body`
- Returning appropriate status codes and JSON responses

## File Structure Checklist

Students should have:
```
02-express-tutorial/
├── app.js                 # Main application file
├── data.js                # Data file (people & products)
├── routes/
│   └── people.js          # People router
├── controllers/
│   └── people.js          # People controller functions
├── methods-public/        # Static frontend files
└── node_modules/
```

## Testing Checklist

Verify students can test with Postman:
- [ ] GET all people - returns array
- [ ] POST new person - returns 201 with success
- [ ] POST without name - returns 400 error
- [ ] GET person by ID - returns person object
- [ ] GET person with invalid ID - returns 404
- [ ] PUT to update person - returns updated person
- [ ] DELETE person - returns updated array
- [ ] Logger logs to console for all requests
