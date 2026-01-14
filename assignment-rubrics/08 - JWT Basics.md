# Node.js: JWT Basics

| Week | Topic      | Learning Objective |
|------|------------|--------------------|
| 8    | JWT Basics | Students will be able to implement JWT authentication; protect routes with authentication middleware; use jwt.sign() and jwt.verify(); and test protected endpoints in Postman.

## Assignment Rubric

You can mark the student's assignment as complete if they:

- [ ] Created `preferred` folder inside `05-JWT-Basics` with proper structure
- [ ] Initialized npm project and installed required packages (`express`, `jsonwebtoken`, `dotenv`)
- [ ] Created `.gitignore` with `.env` and `/node_modules`
- [ ] Organized code into `routes`, `middleware`, and `controllers` directories
- [ ] Created `.env` file with `JWT_SECRET` (strong random string) and `JWT_LIFETIME`
- [ ] Implemented POST `/api/v1/logon` route that returns a JWT
- [ ] Implemented authentication middleware that validates JWT
- [ ] Implemented protected GET `/api/v1/hello` route
- [ ] Tested both routes successfully in Postman
- [ ] (Optional) Created simple HTML/JS frontend

## Key Implementation Checkpoints

### Project Structure
```
05-JWT-Basics/
└── preferred/
    ├── .env
    ├── .gitignore
    ├── package.json
    ├── app.js
    ├── controllers/
    │   └── auth.js
    ├── middleware/
    │   └── auth.js
    └── routes/
        └── main.js
```

### .env File
```
JWT_SECRET=<long-random-string-from-generator>
JWT_LIFETIME=24h
```

### .gitignore
```
.env
/node_modules
```

### POST /api/v1/logon Controller
```javascript
const jwt = require('jsonwebtoken');

const logon = (req, res) => {
  const { name, password } = req.body;
  
  // Basic validation (optional but good practice)
  if (!name || !password) {
    return res.status(400).json({ message: 'Please provide name and password' });
  }
  
  // Create the token
  const token = jwt.sign(
    { name: name },                    // payload
    process.env.JWT_SECRET,            // secret
    { expiresIn: process.env.JWT_LIFETIME }  // options
  );
  
  res.status(200).json({ token });
};

module.exports = { logon };
```

### Authentication Middleware
```javascript
const jwt = require('jsonwebtoken');

const authMiddleware = (req, res, next) => {
  const authHeader = req.header('Authorization');
  
  if (!authHeader || !authHeader.startsWith('Bearer ')) {
    return res.status(401).json({ message: 'unauthorized' });
  }
  
  const token = authHeader.split(' ')[1];
  
  try {
    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    req.user = { name: decoded.name };
    next();
  } catch (error) {
    return res.status(401).json({ message: 'unauthorized' });
  }
};

module.exports = authMiddleware;
```

### GET /api/v1/hello Controller
```javascript
const hello = (req, res) => {
  const userName = req.user.name;
  res.status(200).json({ 
    message: `Hello, ${userName}! Welcome to the protected route.` 
  });
};

module.exports = { hello };
```

### Routes Setup
```javascript
const express = require('express');
const router = express.Router();
const { logon } = require('../controllers/auth');
const { hello } = require('../controllers/auth');
const authMiddleware = require('../middleware/auth');

router.post('/logon', logon);
router.get('/hello', authMiddleware, hello);  // Protected route

module.exports = router;
```

### App.js Setup
```javascript
require('dotenv').config();
const express = require('express');
const app = express();

const mainRouter = require('./routes/main');

// Middleware
app.use(express.json());
app.use('/api/v1', mainRouter);

const port = process.env.PORT || 3000;

const start = async () => {
  try {
    app.listen(port, () => {
      console.log(`Server is listening on port ${port}...`);
    });
  } catch (error) {
    console.log(error);
  }
};

start();
```
- Some students find middleware flow confusing — be patient
- Postman setup can be tricky — walk through if needed
- Emphasize security best practices (secrets, .gitignore, etc.)
