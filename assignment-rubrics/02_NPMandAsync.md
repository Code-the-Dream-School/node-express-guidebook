# Lesson 2 Rubric – NPM, Async Patterns, Events, and Streams

## Overview
In Week 2, students extend the Node foundation from Week 1 by adding:
- **npm usage** (including dev dependencies and `package.json`)
- **Async patterns** (`async/await`, `.then()`, try/catch)
- **Event emitters and HTTP server events**
- **Streams** (reading large files in chunks)

This assignment is designed to help students:
1. Manage a Node project with npm  
2. Understand Promises and async/await  
3. Work with event emitters  
4. Process data using streams  

The assignment takes place in the same `01-node-tutorial/answers` directory as Week 1.

---

## Completion Criteria

Mark the assignment **complete** if the student has:

### Git & Project Setup
- [ ] Merged Week 1 PR and created a new `week2` branch as instructed   
- [ ] Inside `answers/`, created a **`.gitignore`** containing:  
  - `/node_modules`  
  - `.DS_Store`  
  - `temp.txt` (after writing async files)  
- [ ] Ran `npm init` inside `answers/` to generate a **package.json**  
- [ ] Installed **nodemon** as a dev dependency  
- [ ] Edited `package.json` scripts to include:  
  - `"dev": "nodemon prompter.js"`  
  - `"start": "node prompter.js"`  

### Required Programs
The student must complete *all* required files in `01-node-tutorial/answers/`:

1. **writeWithPromisesAwait.js**  
2. **writeWithPromisesThen.js**  
3. **Updated prompter.js** with `server.on("request")` listener  
4. **customEmitter.js**  
5. **16-streams.js**  

All programs must run with `node filename.js` (or `npm run dev` for prompter).

---

## Concept-by-Concept Rubric

### 1. `writeWithPromisesAwait.js` (async/await)
**Criteria**
- [ ] Uses `const { writeFile, readFile } = require("fs").promises`  
- [ ] Defines an `async` `writer()` function using **three `await writeFile()` calls**, each appending lines to `temp.txt`  
- [ ] Wraps all awaits in **try/catch**  
- [ ] Defines `reader()` using `await readFile()`  
- [ ] Defines a third async function `readWrite()` that awaits `writer()` then `reader()`  
- [ ] Calls `readWrite()` at the bottom  
- [ ] `temp.txt` is ignored via `.gitignore`  

**Common Issues**
- Forgetting `{ flag: "a" }`, causing overwritten lines  
- Calling `writer()` and `reader()` at the bottom instead of using coordinated async flow  
- Using await at top-level (not allowed)

---

### 2. `writeWithPromisesThen.js` (.then chaining)
**Criteria**
- [ ] Uses `.then()` chaining starting with a `writeFile()` call  
- [ ] Correctly chains each subsequent `.then` block  
- [ ] Includes a `.catch()` at the end  
- [ ] Reads file and logs contents in final `.then`  
- [ ] Demonstrates correct Promise flow (no mixed async/await)

**Common Issues**
- Forgetting to `return` inside `.then()`, breaking the chain  
- Incorrect file path  
- Missing .catch()  

---

### 3. Prompter modification (server "request" event)
**Criteria**
- [ ] Adds an event listener above `server.listen()`:

      server.on("request", (req) => {
        console.log("event received:", req.method, req.url);
      });

- [ ] Running `npm run dev` shows event logs in terminal during browser requests  
- [ ] No changes to server behavior (only logs added)

**Common Issues**
- Logging inside wrong location  
- Forgetting to restart nodemon  
- Listener placed after `.listen()` causing missing events  

---

### 4. `customEmitter.js` (event emitters)
**Criteria**
- [ ] Creates an instance of `EventEmitter`  
- [ ] Registers at least one `.on()` handler  
- [ ] Emits events using `.emit()`  
- [ ] Logs event output (with or without parameters)  
- [ ] Demonstrates understanding of event-driven architecture  
- [ ] Creativity encouraged (timers, chaining emitters, async waiters)

**Common Issues**
- Importing `events` incorrectly  
- Emitting before `.on()` is defined  
- Using `EventEmitter()` without `new`  

---

### 5. `16-streams.js` (streams)
**Criteria**
- [ ] Creates a **readable stream** for `../content/big.txt`  
- [ ] Uses encoding `"utf8"`  
- [ ] Sets `highWaterMark` to **200** (or other tested values)  
- [ ] Tracks number of chunks with a counter  
- [ ] Handles `"data"`, `"end"`, and `"error"` events correctly  
- [ ] Logs chunk contents and final chunk count  

**Common Issues**
- Wrong file path (`./content` instead of `../content`)  
- Forgetting to handle the `"error"` event  
- Missing encoding (output appears as buffers)  

---

## Mentor Notes

- Make sure students don’t `git init` inside `answers/` — videos show this but they must ignore it.  
- The biggest conceptual hurdles this week:  
  - Understanding async/await flow  
  - Understanding how `.then()` chaining differs  
  - Ordering async calls without mixing styles  
  - Using EventEmitter correctly  
  - Recognizing how streams break data into chunks  
- If all files run and demonstrate the right async patterns, the student has met the learning objectives.

---

## Mentor Scoring (Optional)

| Category | Description | Points |
|-----------|--------------|--------|
| **Async/Await Program** | Correct async flow, try/catch usage | 3 |
| **.then() Program** | Proper chaining and error handling | 2 |
| **Prompter Modification** | Logs request events correctly | 1 |
| **Event Emitters** | Custom event examples run properly | 2 |
| **Streams** | Reads big file in chunks, logs count | 1 |
| **GitHub Submission** | Correct branch, PR link submitted | 1 |
| **Total** |  | **/10** |

---

## Mentor Checklist Summary

Before marking as complete:
- [ ] All five required programs exist and run  
- [ ] Async/await and `.then()` patterns implemented correctly  
- [ ] Event listeners work in `prompter.js`  
- [ ] Streams file logs chunk data and total count  
- [ ] `.gitignore` prevents `node_modules/` and `temp.txt` uploads  
- [ ] Student created a PR from `week2` branch  
- [ ] You provided constructive feedback  

---

### Example Mentor Feedback
> Great job on Week 2! You implemented both async/await and `.then()` patterns correctly, and your custom event emitter shows a strong understanding of Node’s event system.  
> One small suggestion: inside your `.then()` chain, remember to `return` the next `writeFile()` to preserve the chain flow.  
> Keep up the good work — next week we’ll build on these async concepts in Express!
