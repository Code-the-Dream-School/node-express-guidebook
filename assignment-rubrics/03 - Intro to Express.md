# Lesson 3 Rubric – Introduction to Express

## Overview
In Week 3, students transition from pure Node.js to using the Express framework, learning:
- **Express.js fundamentals** (app setup, middleware, routing)
- **Serving static files** with `express.static()`
- **Building REST APIs** with JSON responses
- **Route parameters** (`:productID`)
- **Query strings** (`?search=al&limit=5`)
- **HTTP status codes** (200, 404)

This assignment is designed to help students:
1. Understand Express application structure
2. Serve static HTML files
3. Build REST API endpoints that return JSON
4. Handle route parameters and query strings
5. Implement proper error handling with status codes

The assignment takes place in the `02-express-tutorial` directory.

---

## Completion Criteria

Mark the assignment **complete** if the student has:

### Git & Project Setup
- [ ] Merged Week 2 PR and created a new `week3` branch as instructed
- [ ] Switched to the `02-express-tutorial` directory
- [ ] Ran `npm install` to install dependencies (including Express)
- [ ] Created a `public/` folder with an `index.html` file

### Required Express Application Structure
The student must have a working `app.js` with all elements in the correct order:

1. **Require statements** – Express and data imports
2. **App creation** – `const app = express()`
3. **Middleware** – `app.use(express.static("./public"))`
4. **Route handlers** – `app.get()` statements for APIs
5. **404 handler** – `app.all()` for page not found
6. **Server start** – `app.listen()` on port 3000

### Required API Endpoints
The student must implement all of these working endpoints:

1. **`GET /api/v1/test`** – Returns `{ message: "It worked!" }`
2. **`GET /api/v1/products`** – Returns all products as JSON
3. **`GET /api/v1/products/:productID`** – Returns single product by ID
4. **`GET /api/v1/query`** – Handles search and limit query parameters
5. **Custom logic** – Student adds their own query feature

All endpoints must be testable in the browser and return proper JSON.

---

## Concept-by-Concept Rubric

### 1. Express Application Setup
**Criteria**
- [ ] `app.js` imports Express: `const express = require("express")`
- [ ] Creates app instance: `const app = express()`
- [ ] Imports products data: `const { products } = require("./data")`
- [ ] All elements appear in correct order (middleware → routes → 404 → listen)
- [ ] Server starts successfully with `npm start`

**Common Issues**
- Wrong order (routes before middleware, or 404 before routes)
- Forgetting to call `express()` to create the app
- Missing `require("./data")` import

---

### 2. Static File Serving
**Criteria**
- [ ] Created `public/` folder in `02-express-tutorial`
- [ ] Created `index.html` with basic HTML content
- [ ] Added middleware: `app.use(express.static("./public"))`
- [ ] Middleware appears **before** route handlers
- [ ] `http://localhost:3000` displays the HTML page
- [ ] Static files load correctly (HTML, CSS, JS if included)

**Common Issues**
- Wrong path in `express.static()` (e.g., `"public"` instead of `"./public"`)
- Placing middleware after routes (order matters!)
- Forgetting to create the `public/` folder

---

### 3. 404 "Page Not Found" Handler
**Criteria**
- [ ] Uses `app.all()` to catch all methods and routes
- [ ] Placed **after** all other route handlers but **before** `app.listen()`
- [ ] Returns 404 status code
- [ ] Returns appropriate message (JSON or HTML)
- [ ] Testing `http://localhost:3000/not-there` returns 404

**Example Implementation**
```javascript
app.all("*", (req, res) => {
  res.status(404).send("Page not found");
});
```

**Common Issues**
- Placing 404 handler before other routes (catches everything!)
- Forgetting `.status(404)` – returns 200 by default
- Using `app.get()` instead of `app.all()` (only catches GET requests)

---

### 4. Basic API Endpoint (`/api/v1/test`)
**Criteria**
- [ ] Route: `app.get("/api/v1/test", ...)`
- [ ] Returns JSON: `res.json({ message: "It worked!" })`
- [ ] Placed after middleware but before 404 handler
- [ ] Browser test at `http://localhost:3000/api/v1/test` shows JSON

**Common Issues**
- Using `res.send()` instead of `res.json()`
- Forgetting quotes around the route path
- Route placed in wrong order

---

### 5. Return All Products (`/api/v1/products`)
**Criteria**
- [ ] Route: `app.get("/api/v1/products", ...)`
- [ ] Returns entire products array: `res.json(products)`
- [ ] Browser displays array of product objects with id, name, image, price, desc

**Common Issues**
- Forgetting to import `{ products }` from `./data`
- Using `res.send(products)` instead of `res.json()`
- Typo in route path

---

### 6. Return Single Product by ID (`/api/v1/products/:productID`)
**Criteria**
- [ ] Route uses parameter: `app.get("/api/v1/products/:productID", ...)`
- [ ] Converts string to integer: `parseInt(req.params.productID)`
- [ ] Uses `Array.find()` to locate product:
  ```javascript
  const product = products.find((p) => p.id === idToFind);
  ```
- [ ] Returns product as JSON if found
- [ ] Returns 404 status with error message if not found:
  ```javascript
  if (!product) {
    return res.status(404).json({ message: "That product was not found." });
  }
  ```
- [ ] Tests successfully:
  - Valid ID (e.g., `/api/v1/products/1`) returns product
  - Invalid ID (e.g., `/api/v1/products/5000`) returns 404
  - Non-numeric ID (e.g., `/api/v1/products/nottthere`) returns 404

**Common Issues**
- Forgetting `parseInt()` – comparison fails because params are strings
- Not handling 404 case (returns undefined instead of error)
- Forgetting `return` before 404 response (code continues executing)
- Wrong parameter name (`:productId` vs `:productID`)

---

### 7. Query String Handling (`/api/v1/query`)
**Criteria**
- [ ] Route: `app.get("/api/v1/query", ...)`
- [ ] Accesses query parameters via `req.query.search` and `req.query.limit`
- [ ] Implements search filter using `Array.filter()`:
  ```javascript
  let filteredProducts = products;
  if (req.query.search) {
    filteredProducts = filteredProducts.filter((p) =>
      p.name.startsWith(req.query.search)
    );
  }
  ```
- [ ] Implements limit using `Array.slice()`:
  ```javascript
  if (req.query.limit) {
    filteredProducts = filteredProducts.slice(0, parseInt(req.query.limit));
  }
  ```
- [ ] Returns filtered results as JSON
- [ ] Tests successfully:
  - `/api/v1/query?search=al` returns products starting with "al"
  - `/api/v1/query?limit=5` returns max 5 products
  - `/api/v1/query?search=al&limit=2` combines both filters

**Common Issues**
- Case sensitivity issues (search doesn't match capitalization)
- Not converting limit to integer
- Using `Array.find()` instead of `Array.filter()`
- Forgetting to handle when query params are undefined

---

### 8. Custom Query Logic (Student Choice)
**Criteria**
- [ ] Student adds at least one additional query feature
- [ ] Feature works correctly and is testable
- [ ] Code demonstrates understanding of filtering/manipulating arrays

**Examples of Good Custom Logic**
- Price filtering: `?maxPrice=20`
- Regular expression search: `?pattern=chair`
- Sorting: `?sort=price` or `?sort=name`
- Minimum price: `?minPrice=10`
- Multiple word search: `?search=wood+chair`

**Common Issues**
- Not implementing any custom logic (requirement missed)
- Logic doesn't actually work or return results
- No way to test the feature

---

### 9. Optional: Frontend Button with Fetch
**Criteria** (if completed)
- [ ] Button added to `index.html`
- [ ] JavaScript (inline or separate file) makes fetch request to `/api/v1/products`
- [ ] Response data is displayed in the page (in a div or other element)
- [ ] Demonstrates understanding of client-server communication

**Common Issues**
- CORS errors (shouldn't happen since same origin)
- Fetch not using correct URL
- Not handling the promise correctly
- Not displaying results in the DOM

---

## Mentor Notes

### Key Teaching Points This Week
- **Order matters in Express**: middleware → routes → 404 → listen
- **`res.json()` vs `res.send()`**: Always use `res.json()` for APIs
- **Route parameters** (`:productID`) vs **query strings** (`?search=al`)
- **Always use `return`** before error responses to prevent further execution
- **Status codes matter**: 404 for not found, 200 is default for success

### Common Conceptual Issues
1. **Not understanding Express middleware flow** – Students place middleware after routes
2. **Forgetting that params/query are strings** – Need `parseInt()` for IDs
3. **Not handling error cases** – Forgetting 404 responses for missing products
4. **Confusion between route params and query strings** – When to use each

### What Students Should Understand
By the end of this week, students should be able to:
- Explain the structure of an Express application
- Differentiate between middleware, route handlers, and error handlers
- Build RESTful API endpoints that return JSON
- Use route parameters for resource IDs
- Use query strings for filtering/searching
- Handle error cases with appropriate status codes

### If a Student is Struggling
- Have them draw out the request flow (browser → Express → response)
- Console.log `req.params` and `req.query` to see what data looks like
- Test each endpoint individually before moving to the next
- Use Postman or browser dev tools to inspect responses

---

## Mentor Scoring (Optional)

| Category | Description | Points |
|----------|-------------|--------|
| **Express Setup** | Correct app structure, middleware, listen | 2 |
| **Static Files** | Serves HTML from public folder | 1 |
| **Basic Endpoints** | Test endpoint and all products work | 1 |
| **Route Parameters** | Product by ID with 404 handling | 2 |
| **Query Strings** | Search and limit work correctly | 2 |
| **Custom Logic** | Student's own query feature | 1 |
| **GitHub Submission** | Correct branch, PR link submitted | 1 |
| **Total** |  | **/10** |

---

## Mentor Checklist Summary

Before marking as complete:
- [ ] Express app structure follows correct order
- [ ] Static HTML file loads at root URL
- [ ] All required API endpoints exist and return JSON
- [ ] Route parameter endpoint handles valid and invalid IDs
- [ ] Query string endpoint filters by search and limit
- [ ] Student added custom query logic
- [ ] 404 handler catches invalid routes
- [ ] Student created PR from `week3` branch
- [ ] You provided constructive feedback

---

## Example Mentor Feedback

### For a Strong Submission
> Excellent work on Week 3! Your Express application is well-structured, and all your API endpoints work correctly. I especially liked your custom query logic for filtering by price – that's a practical feature. Your 404 handling is solid, and you correctly used `parseInt()` for the product ID parameter.  
> One small note: consider using `.toLowerCase()` on both sides of your search comparison to make it case-insensitive. That would improve the user experience.  
> Great job overall – you clearly understand REST API basics. Next week we'll refactor these routes into separate modules!

### For a Submission Needing Improvement
> Good start on Week 3! Your Express app runs and serves static files correctly. However, I noticed a few issues with your product-by-ID endpoint:
> 1. You're not using `parseInt()` on the productID, so the comparison fails when you test with `/api/v1/products/1`
> 2. You're missing the 404 response when a product isn't found
> 
> Try adding these fixes:
> ```javascript
> const idToFind = parseInt(req.params.productID);
> const product = products.find((p) => p.id === idToFind);
> if (!product) {
>   return res.status(404).json({ message: "That product was not found." });
> }
> res.json(product);
> ```
> 
> Also, remember that your 404 handler (`app.all()`) should come *after* all your other routes. Right now it's catching everything before your API routes can run.  
> Please make these corrections and let me know when you've pushed the updates!

---

## Additional Resources for Students

If students want to deepen their understanding:
- **Express documentation**: https://expressjs.com/
- **REST API design**: https://restfulapi.net/
- **HTTP status codes**: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status
- **Array methods**: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array
