# Lesson Plan 01 – Introduction to Node.js

## About This Week
This week introduces students to **Node.js** — what it is, how it runs JavaScript outside the browser, and how to use its built-in modules.  
By the end of the week, students should be able to:
- Run Node programs from the command line  
- Use global variables and environment variables  
- Import and export modules using `require` and `module.exports`  
- Work with built-in Node modules (`os`, `path`, `fs`, `http`)  
- Understand basic asynchronous behavior with callbacks  

The goal is to build familiarity with Node as a runtime environment, laying the foundation for backend and API development.

---

## Explore Session (60 minutes)

**Purpose:** Help students understand what Node is and what makes it different from browser-based JavaScript.  
**Materials:** Mentor slides (Explore section), terminal demo, `node-express-course` starter repo, and optionally the FreeCodeCamp Node.js video (0:00–1:45:57).

---

### Segment 1 – Warm-Up (5 min)
Ask:
- “What do you already know about Node.js?”
- “Why might we want to run JavaScript outside a web browser?”

Quick chat poll:
> “True or false: Node is a framework, like React.”  

Use this to clarify that Node is a **runtime environment**, not a framework.

**Mentor Tip:** Encourage students to think of Node as the “engine” that powers many web tools.

---

### Segment 2 – I Do (10 min)
Demonstrate running Node locally.

Example commands:

    node --version
    node
    > console.log("Hello from Node!");

Explain:
- Node runs JavaScript without the browser.
- You can run `.js` files directly with `node filename.js`.
- The terminal output replaces the browser console.

Show a simple file (`01-intro.js`):

    console.log("Running Node program...");

**CFU Questions**
- “How is running code in Node different from running it in a browser console?”
- “Where does output appear when we use console.log in Node?”

---

### Segment 3 – We Do (20 min)
Collaborate on simple module examples.

**Step 1: Exporting and Importing**

    // 04-names.js
    const first = "Jazmine";
    const last = "Nguyen";
    module.exports = { first, last };

    // 03-modules.js
    const names = require("./04-names");
    console.log(`Full name: ${names.first} ${names.last}`);

**Step 2: Built-in Modules**

    const os = require("os");
    console.log("Platform:", os.platform());
    console.log("Uptime:", os.uptime());

    const path = require("path");
    console.log("File path example:", path.join(__dirname, "folder", "file.txt"));

**CFU Questions**
- “What’s the difference between `require()` and `import` in JavaScript?”
- “Why do we use `path.join` instead of just concatenating strings?”

---

### Segment 4 – You Do (20 min)
Students practice hands-on:

> Create a new file `02-globals.js` that logs `__dirname`, `__filename`, and an environment variable `process.env.MY_VAR`.

Steps:
1. In terminal:  
       export MY_VAR="Hi there!"
2. In the file:  
       console.log("Directory:", __dirname);
       console.log("Environment variable:", process.env.MY_VAR);

Mentor walks around or checks in on Slack as students test their code.

**CFU Prompt:**  
> “What happens if you run your file without setting the environment variable first?”

---

### Segment 5 – Wrap-Up (5 min)
Recap:
- Node runs JavaScript outside the browser.
- Node uses the CommonJS module system.
- You can require built-in or custom modules.
- Globals like `__dirname` and `process` are part of Node’s runtime.

Ask:
> “What’s one thing about Node that surprised you?”  
> “What’s one question you still have?”

Preview the Apply session: reading/writing files, async functions, and a simple HTTP server.

---

## Apply Session (60 minutes)

**Purpose:** Guide students through real-world use of Node modules, asynchronous code, and a simple server.  
**Materials:** Mentor slides (Apply section), VS Code or Replit, `node-express-course` repo.

---

### Segment 1 – Quick Recap (5 min)
Ask:
- “Who was able to run their first Node file successfully?”
- “What’s something you learned about `require` or environment variables?”

Address common issues:
- `Cannot find module` → missing `./` in path  
- `ReferenceError: module is not defined` → missing `module.exports`

---

### Segment 2 – Guided Coding (25 min)

**Part A: File System (Sync)**

    const { writeFileSync, readFileSync } = require("fs");
    writeFileSync("./temporary/fileA.txt", "Line 1\n");
    writeFileSync("./temporary/fileA.txt", "Line 2\n", { flag: "a" });
    writeFileSync("./temporary/fileA.txt", "Line 3\n", { flag: "a" });

    const result = readFileSync("./temporary/fileA.txt", "utf8");
    console.log(result);

Discuss:
- Sync vs async methods  
- The `{ flag: "a" }` option for appending  
- Using `.gitignore` to exclude `temporary/` files

**Part B: File System (Async)**

    const { writeFile } = require("fs");
    writeFile("./temporary/fileB.txt", "Line 1\n", (err) => {
      if (err) return console.log(err);
      writeFile("./temporary/fileB.txt", "Line 2\n", { flag: "a" }, (err) => {
        if (err) return console.log(err);
        writeFile("./temporary/fileB.txt", "Line 3\n", { flag: "a" }, (err) => {
          if (err) return console.log(err);
          console.log("Finished writing!");
        });
      });
    });

Discuss:
- “Callback hell” and why async code can look messy.  
- We’ll later solve this with **Promises** and **async/await**.

**CFU Questions**
- “What’s the difference between `writeFileSync` and `writeFile`?”
- “What happens if you forget `{ flag: 'a' }` in the second call?”

---

### Segment 3 – HTTP Server (20 min)
Demo a simple web server.

    const http = require("http");

    const server = http.createServer((req, res) => {
      if (req.url === "/") {
        res.end("Welcome to my Node server!");
      } else if (req.url === "/about") {
        res.end("This is the about page.");
      } else {
        res.end("404 - Page not found");
      }
    });

    server.listen(3000, () => {
      console.log("Server running on port 3000...");
    });

Students test:
1. Run `node 12-http.js`  
2. Visit [http://localhost:3000](http://localhost:3000)

**CFU Questions**
- “What happens if you forget to call `.end()`?”
- “How does Node know when a request is complete?”

---

### Segment 4 – Wrap-Up and Reflection (10 min)
Discussion prompts:
> “Which Node module did you find most interesting or confusing?”  
> “What’s one thing you want to try with Node next?”

Remind students:
- Commit changes with clear messages.  
- Push their `week1` branch and create a pull request.  
- Submit the PR link via the submission form.

*Mentor Tip:* Students who experiment with the `prompter.js` file (e.g., color picker or guessing game) should be encouraged — creativity helps reinforce understanding!

---

## Notes for Mentors
- Keep the focus on **what Node is** and **how to run code**.  
- Prioritize **hands-on experimentation** over theory.  
- Model debugging: run files, break them, fix them live.  
- Show how small scripts lead into web servers and APIs.  
- Celebrate the first successful HTTP server — it’s a milestone!

---

### Optional Extensions
If time allows:
- Show how `console.log` order changes in async code.  
- Demo `os.userInfo()` or `os.totalmem()` to explore Node’s environment.  
- Discuss how Node differs from Deno or Bun (conceptually only).
