# Node.js: JWT Basics — Group Mentor Guide

Welcome to Week 8 of the Node.js course! This week, students are learning:

- How to implement authentication using JSON Web Tokens (JWT)
- How to hash passwords securely
- How to protect routes with authentication middleware
- How to use `jsonwebtoken` package (`jwt.sign` and `jwt.verify`)
- How to handle authentication errors properly
- How to test protected routes in Postman

Students are building an Express app with `/api/v1/logon` (POST) and `/api/v1/hello` (GET) routes.

## Warm-Up (5–10 minutes)

Choose one:

**Relationship-Building**  
- What's an app or website you log into daily? Have you ever wondered how login works behind the scenes?
- Have you ever forgotten a password? How do you think websites know if your reset request is legitimate?

**Check for Understanding (from last week)**  
- What's the difference between query parameters and route parameters?
- How do you access query parameters in Express?
- What does middleware do in Express?

## Explore vs. Apply — Session Formats

**Explore Sessions** → Walk through JWT concepts, password hashing, and authentication flow  
**Apply Sessions** → Debug JWT implementations, test with Postman, troubleshoot middleware

## Sample Timing for 1-Hour Session

| Time      | Activity                                    |
|-----------|---------------------------------------------|
| 0:00–0:10 | Warm-up + review middleware & error handling|
| 0:10–0:30 | Explore: JWT flow, signing & verifying tokens|
| 0:30–0:50 | Apply: build auth middleware & test in Postman|
| 0:50–1:00 | Wrap-up + final questions                   |

## Check for Understanding (Ask 2–3)

- What is a JWT and what problem does it solve?
- Why do we hash passwords instead of storing them as plain text?
- What's the difference between `jwt.sign()` and `jwt.verify()`?
- What does the Authorization header look like with a Bearer token?
- Why do we store the JWT secret in a `.env` file?
- What happens if a JWT is expired or invalid?

## Explore Prompts

Use these to demonstrate key concepts live:

- Let's walk through the authentication flow — what happens when a user logs in?
- How does a JWT get created? Let's look at `jwt.sign()` together.
- How does the server know if a token is valid? Let's explore `jwt.verify()`.
- What's inside a JWT? Let's decode one at jwt.io.

*Mini-Demo Ideas:*  

```javascript
// Creating a JWT
const jwt = require('jsonwebtoken');

const token = jwt.sign(
  { name: 'Alice' },           // payload
  process.env.JWT_SECRET,      // secret key
  { expiresIn: '24h' }         // options
);

// Verifying a JWT (synchronous)
try {
  const decoded = jwt.verify(token, process.env.JWT_SECRET);
  console.log(decoded.name); // 'Alice'
} catch (error) {
  console.log('Invalid token!');
}

// Bearer token format
const authHeader = "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...";
const token = authHeader.split(' ')[1]; // Get the token part
```

---

## Apply Prompts (Live Coding & Troubleshooting)

### Assignment Hotspots
* Forgetting to split the Authorization header to extract the token (need to remove "Bearer ")
* Not wrapping `jwt.verify()` in try/catch — it throws errors!
* Missing `.env` file or not loading it with `dotenv.config()`
* Using weak or guessed JWT secrets instead of generated random strings
* Forgetting to call `next()` in middleware after successful authentication
* Not setting `req.user` before calling `next()`
* Testing in Postman without setting up Bearer token authorization
* Confusing when to return 401 vs 403 status codes

### Try This Live

**Let's build authentication middleware together:**

```javascript
const jwt = require('jsonwebtoken');

const authMiddleware = (req, res, next) => {
  // Get the Authorization header
  const authHeader = req.header('Authorization');
  
  // Check if header exists and starts with "Bearer "
  if (!authHeader || !authHeader.startsWith('Bearer ')) {
    return res.status(401).json({ message: 'unauthorized' });
  }
  
  // Extract the token
  const token = authHeader.split(' ')[1];
  
  // Verify the token
  try {
    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    req.user = { name: decoded.name }; // Store user info
    next(); // Pass control to the route handler
  } catch (error) {
    return res.status(401).json({ message: 'unauthorized' });
  }
};

module.exports = authMiddleware;
```

Ask:
* What happens if we forget the `return` before `res.status(401)`?
* Why do we need try/catch around `jwt.verify()`?
* What if the token is expired? Will the catch block handle it?

## Engagement Strategies (for quiet groups)

* Debug Together: "Your token isn't working in Postman — let's check the Authorization tab."
* JWT Decoder: "Let's paste this token into jwt.io and see what's inside!"
* Error Hunt: "What status code should we return if the token is missing vs invalid?"
* Pair Testing: "One person create a token, the other verify it — does it work?"

## Postman Setup (Critical!)

**Setting up Bearer Token Authorization:**
1. Do the POST request to `/api/v1/logon`
2. Copy the token from the response
3. Go to GET request → Authorization tab
4. Select "Bearer Token" from dropdown
5. Paste the token
6. Save and send the request

**Auto-saving tokens (bonus):**
1. Create a "JWT Basics" environment in Postman
2. In POST request Tests tab, add:
   ```javascript
   const jsonData = pm.response.json();
   pm.environment.set("token", jsonData.token);
   ```
3. In GET request Authorization, use `{{token}}` as the value
4. Now the token auto-updates after each login!

## Optional Challenges

- Add a token expiration check and return a specific error message
- Create a `/api/v1/refresh` route that issues a new token
- Add a simple HTML/JS frontend in `public/` folder
- Store user roles in the JWT and check permissions
- Add error handling middleware using `StatusError` class
- Use async versions of `jwt.sign()` and `jwt.verify()`

## Security Reminders for Students

- Never commit `.env` files (add to `.gitignore`)
- Use strong, random JWT secrets (not "mysecret123")
- Tokens should expire (use `expiresIn`)
- Never store passwords in plain text
- HTTPS only in production (not covered this week, but important!)

## Mentor To-Do
- [ ] Run a session using this guide  
- [ ] Verify students have `.env` in their `.gitignore`
- [ ] Check that students are using generated secrets, not weak strings
- [ ] Help students set up Postman authorization correctly
- [ ] Submit your [Mentor Session Report](https://airtable.com/appoSRJMlXH9KvE6w/shrp0jjRtoMyTXRzh)
