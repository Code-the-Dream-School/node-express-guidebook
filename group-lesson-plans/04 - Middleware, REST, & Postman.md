# Week 4: Middleware, REST Methods & Postman — Group Mentor Guide

Welcome to Week 4! This week, students:

- Learned what middleware is and how it runs before route handlers
- Implemented a `logger` middleware function
- Used Express to parse JSON and form data from requests
- Practiced creating and testing **GET, POST, PUT, PATCH, and DELETE** routes
- Tested their API using Postman
- Started refactoring code into **routes** and **controllers**

They are working in the `02-express-tutorial` folder on the `week4` branch.


## Warm-Up (5–10 minutes)

Choose **one** to start the session:

**Relationship-Building**
- What’s one app or service you use daily that you wish worked better?
- If you could instantly master one programming skill, what would it be?

**Check for Understanding (from Week 3)**
- What’s the difference between a route parameter and a query string?
- Why does the order of middleware and routes matter?
- What does `express.static()` do?

## Explore vs. Apply — Session Formats

**Explore Sessions** → Concept overviews, discussion, quick demos  
**Apply Sessions** → Live coding, debugging, Postman practice

## Sample Timing for 1-Hour Session

| Time      | Activity                                     |
|-----------|----------------------------------------------|
| 0:00–0:10 | Warm-up + quick review                       |
| 0:10–0:30 | Explore: middleware + REST methods + Postman |
| 0:30–0:50 | Apply: build/test API routes together         |
| 0:50–1:00 | Wrap-up + reflections                        |

## Check for Understanding (Pick 2–3)

- What is middleware and when does it run?
- Why must `express.json()` come before your `POST` routes?
- What’s the difference between PUT and PATCH?
- How can you test an API route without building a frontend?

## Explore Prompts (Discussion & Demos)

- Show how middleware fits into the **request → middleware → route handler** flow
- Compare HTML form submissions vs. JSON body submissions
- Demo how to:
  - Add `logger` middleware that logs method, URL, and timestamp
  - Send a GET request to `/api/v1/people` in Postman
  - Send a POST request with JSON in Postman

*Mini-Demo Idea:*  
> Add `app.use(express.json())`  
> Create a `/api/v1/people` POST route that:
> - Checks for `req.body.name`
> - Returns 400 if missing
> - Adds person if present, returning 201

## Apply Prompts (Live Coding & Troubleshooting)

### Assignment Hotspots
- Middleware placed **after** routes, so it never runs
- Forgetting to call `next()` in middleware → request hangs
- Not parsing JSON before using `req.body`
- Returning 200 for errors instead of 400/404
- Forgetting to test routes in Postman before moving on

### Try This Live

> “Let’s create a middleware + route flow together.”

```js
// logger middleware
const logger = (req, res, next) => {
  console.log(req.method, req.url, new Date().toISOString());
  next();
};

app.use(logger);

app.get("/api/v1/people", (req, res) => {
  res.json([{ id: 1, name: "Alice" }]);
});
```

Follow-up challenges:
- Add a POST `/api/v1/people` route that validates `req.body.name`
- Add a GET `/api/v1/people/:id` route that returns 404 if not found
- Try sending these requests in Postman

## Engagement Strategies (for quiet groups)

- **Postman Challenge**: Have each student send a valid POST and then a failing POST request
- **Fix This Middleware**: Give them middleware missing `next()` and let them debug why it hangs
- **Order Matters**: Move `express.json()` after your POST routes and see what happens
- **Group Build**: One student codes middleware, another codes GET, another codes POST

## Optional Challenges

For students ready to go further:

- Add PUT and DELETE routes for `/api/v1/people`
- Refactor into `routes/people.js` and `controllers/people.js`
- Add middleware that only logs requests to `/api/v1/*`

## Mentor To-Do

- [ ] Run a session using this guide  
- [ ] Help students debug middleware + route order issues  
- [ ] Encourage Postman testing before frontend integration  
- [ ] Submit your [Mentor Session Report](https://airtable.com/appoSRJMlXH9KvE6w/shrp0jjRtoMyTXRzh)  
