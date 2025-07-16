# Week 3: Introduction to Express — Group Mentor Guide

Welcome to Week 3! This week, students:

- Built their first web server using Express
- Learned how to serve static files and set up basic routes
- Created API routes with route parameters and query strings
- Practiced returning JSON responses and handling 404 errors

They are working in the `02-express-tutorial` folder on the `week3` branch of their existing repo.

## 🧊 Warm-Up (5–10 minutes)

Choose **one** of the following to kick off your session:

**👋 Relationship-Building**
- What’s your favorite website or app, and why?
- If you could build any app, what would it do?

**💡 Check for Understanding (from Week 2)**
- When should you use `async/await` versus `.then()`?
- What does `EventEmitter` let us do?
- Why do we use `try/catch` with asynchronous code?

## 🧭 Explore vs. Apply — Session Formats

**Explore Sessions** → Big-picture understanding, discussion, mini-demos  
**Apply Sessions** → Practice with guidance, code review, debugging

**Mix-and-match** is totally fine!

## ⏱️ Sample Timing for 1-Hour Session

| Time      | Activity                            |
|-----------|-------------------------------------|
| 0:00–0:10 | Warm-up + review                    |
| 0:10–0:30 | Explore: routes, params, middleware |
| 0:30–0:50 | Apply: live coding or troubleshooting |
| 0:50–1:00 | Wrap-up + reflections               |

## ❓ Check for Understanding (Pick 2–3)

- What is `express.static()` and what does it do?
- What’s the difference between a route parameter and a query string?
- Why does the order of middleware and routes matter?
- How do you return a 404 error in Express?

## 🧑‍🏫 Explore Prompts (Discussion & Demos)

- Why is Express so widely used compared to vanilla Node?
- How does Express make it easier to build APIs?
- How do you test your Express routes — browser? Postman? console.log?

🧑‍💻 *Mini-Demo Idea:*  
> Show a minimal Express server that:
> - Serves `index.html` from a `public` folder
> - Has one `/api/test` route that returns `{ message: "It worked!" }`
> - Has a `404` handler at the end

## 🛠️ Apply Prompts (Live Coding & Troubleshooting)

### 🔧 Assignment Hotspots
- Middleware and routes in the wrong order (`app.use` after `app.get`)
- Using `req.params` instead of `req.query` (or vice versa)
- Forgetting to use `res.json()` or to send a response at all
- Not handling invalid product IDs (missing 404 error)

### ✅ Try This Live

> “Let’s build a new route together from scratch!”

<pre><code class="language-js">
app.get("/api/v1/hello", (req, res) => {
  res.json({ greeting: "Hey there, CTD!" });
});
</code></pre>

Follow-up challenges:
- Add a `/api/v1/greet/:name` route that returns `Hello, {name}`
- Handle a `/api/v1/query?limit=2&search=table` request

## 💬 Engagement Strategies (for quiet groups)

- **Chat First**: “Write your `app.get` line in the chat — we’ll pick one to use.”
- **Fix This Code**: Show broken route logic and have students spot the issue
- **Draw It Out**: “Who can sketch the request flow from browser to server?”
- **Group Build**: One student types, others give directions — rotate every 3 minutes

## 💡 Optional Challenges

For advanced students or extra practice:

- Add a new endpoint that filters products by price range using query params
- Set up a second static HTML page and route to it
- Create a POST route that logs JSON to the console

## 📎 Resources & Links

- [Assignment Instructions (Week 3)](https://raw.githubusercontent.com/Code-the-Dream-School/node-v3/refs/heads/main/assignments/03IntroToExpress.md)
- [Node.js Mentor Guidebook](https://github.com/Code-the-Dream-School/node-express-guidebook/wiki/Curriculum-and-Teaching-Resources)
- [Intro to Express Documentation](https://expressjs.com/en/starter/hello-world.html)
- [DigitalOcean: Intro to JSON](https://www.digitalocean.com/community/tutorials/an-introduction-to-json)

## ✅ Mentor To-Do

- [ ] Run a session using this guide
- [ ] Help students debug route/middleware issues
- [ ] Submit your [Mentor Session Report](https://airtable.com/appoSRJMlXH9KvE6w/shrp0jjRtoMyTXRzh)
