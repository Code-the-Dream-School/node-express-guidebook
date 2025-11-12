# Lesson 1 Rubric – Node Introduction

## Overview
This first Node.js assignment introduces students to the **Node runtime environment**, **modules**, and **core built-in libraries** such as `fs`, `path`, and `http`.  
Students will demonstrate their ability to:
- Run programs using Node from the command line  
- Use built-in globals and environment variables  
- Import and export modules  
- Read/write files synchronously and asynchronously  
- Create a basic HTTP server  

The goal is to ensure that students can navigate the Node environment confidently and understand how files, modules, and asynchronous code interact.

---

## Completion Criteria

Mark the assignment **complete** if the student:

- [ ] Forked the [Node-Express starter repository](https://github.com/Code-the-Dream-School/node-express-course) and submitted a pull request from `week1` → `main`.
- [ ] Completed all required files inside `01-node-tutorial/answers`.
- [ ] Each program runs without syntax errors using `node filename.js`.
- [ ] Demonstrates understanding of:
  - Node command-line workflow (`node file.js`)
  - Use of built-in modules (`os`, `path`, `fs`, `http`)
  - Module export/import patterns (`require` and `module.exports`)
  - Basic asynchronous behavior using callbacks
  - Environment variables (`process.env`)
- [ ] Submitted a working pull request link via the submission form.

---

## Concept-by-Concept Rubric

| File | Concept | Expected Behavior | Common Issues |
|------|----------|------------------|----------------|
| **01-intro.js** | Basic Node setup | Uses `console.log()` to output text; runs with `node 01-intro.js` | Missing `console.log()` or syntax error |
| **02-globals.js** | Globals & environment | Logs `__dirname` and `process.env.MY_VAR`; shows understanding of environment variables | Forgetting to export MY_VAR before running |
| **03-modules.js** with **04–07** | Module system | Imports from `04-names.js`, `05-utils.js`, `06-alternative-flavor.js`, and `07-mind-grenade.js`; correctly calls required functions | Wrong file paths in `require`; missing `module.exports` syntax |
| **04-names.js** | Exporting multiple values | Exports multiple names as an object | Using `export` keyword instead of Node’s `module.exports` |
| **05-utils.js** | Exporting a single function | Exports and calls a function (e.g., greeting or math operation) | Forgetting to export or call the function |
| **06-alternative-flavor.js** | Alternative export syntax | Adds exports individually using `module.exports.value = ...` | Misunderstanding export pattern |
| **07-mind-grenade.js** | Executing code upon require | Contains a function called immediately in mainline code to show side-effect execution | Function not invoked or missing `console.log()` |
| **08-os-module.js** | Built-in `os` module | Logs system info such as user, uptime, platform | Forgetting to require the module |
| **09-path-module.js** | Built-in `path` module | Uses `path.join()` to build a platform-specific path | Using string concatenation instead of `path.join()` |
| **10-fs-sync.js** | File system (sync) | Writes and reads file content with `writeFileSync` and `readFileSync`; uses `append` flag | Forgetting to create `temporary/` directory; wrong flag |
| **11-fs-async.js** | File system (async) | Writes multiple lines asynchronously using callbacks in sequence; demonstrates callback nesting (“callback hell”) | Lines written out of order; missing error handling |
| **12-http.js** | HTTP server | Uses `http.createServer()` to serve basic text at different routes; listens on port 3000 | Missing `.listen(3000)` or incorrect response handling |
| **prompter.js** | Simple interactive server | Student modifies form behavior or logic (e.g., guessing game, color picker, etc.); shows creativity | No visible change from starter code |

---

## 💬 Mentor Notes

- **Core Understanding:** The biggest goal is familiarity with how Node executes JavaScript outside the browser and how modules are imported/exported.  
- **Asynchronous Code:** If students’ async file operations are out of order or missing callbacks, that’s normal—use it as a teachable moment about callback flow.  
- **Encourage Experimentation:** Students can modify file names, logs, or server behavior to test their understanding.  
- **Minimum Completion:** All programs run without crashing; some may show console output only.

---

## Mentor Scoring (Optional)

| Category | Description | Points |
|-----------|--------------|--------|
| **Code Correctness** | Files run successfully with correct output | 4 |
| **Syntax & Structure** | Correct use of `require`, `module.exports`, indentation | 2 |
| **Async Logic** | Demonstrates understanding of callback sequencing | 2 |
| **GitHub Submission** | Proper fork, branch, PR link provided | 1 |
| **Effort & Completeness** | All exercises attempted | 1 |
| **Total** |  | **/10** |

---

## Mentor Checklist Summary

Before marking as complete:
- [ ] All files in `01-node-tutorial/answers` exist and run
- [ ] Student understands how to run Node scripts via command line
- [ ] Code demonstrates awareness of modules and async functions
- [ ] Student submitted working pull request to their own repo
- [ ] You provided a short feedback comment (see below)

---

### Example Mentor Feedback
> Great work on your first Node assignment! You’ve successfully run programs from the command line and used several core Node modules.  
> Be sure to review how callback functions work in your async file writes — understanding “callback hell” will make upcoming lessons on Promises and async/await much smoother. Keep experimenting with the HTTP server and prompter script — nice job getting everything set up!
