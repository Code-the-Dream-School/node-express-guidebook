# Lesson 2: NPM & Async Patterns — Group Mentor Guide

Welcome to Week 2! This week, students learned about:

- Using `npm` and managing project dependencies
- Writing asynchronous code with Promises and `async/await`
- Using Node's built-in `fs.promises`
- Handling errors with `try/catch` and `.then().catch()`
- Creating and handling custom events with `EventEmitter`
- Reading data with streams

They worked primarily in the `01-node-tutorial/answers` folder.

## 🧠 Session Planning Overview

**Explore Sessions** focus on digging into new concepts through discussion and light demos.  
**Apply Sessions** focus on hands-on support, debugging, and practicing assignment patterns.

## 🧭 Explore Session Prompts

Choose 1–2 of these to spark discussion or mini-demos:

- Why is async programming so important in Node?
- What are the pros/cons of `async/await` vs `.then()`?
- How does Node's `EventEmitter` compare to things like browser events?
- What exactly does `npm install` do behind the scenes?

🧑‍🏫 *Mini-Demo idea:*  
Open a small JS file and show how `await` only works inside `async` functions — then contrast with chaining `.then()`.

## 🛠️ Apply Session Activities

Use these for live practice, assignment troubleshooting, or group problem-solving. Remember to use the ["I Do, We Do, You Do" model of gradual release](https://coda.io/d/_dAM9Xiy8hnR/Teaching-Notes_suWDehoD) for mentor sessions.

### 🔧 Assignment Hotspots
- Forgetting to use `await` in `async` functions
- Not wrapping async calls in `try/catch`
- Confusion about how `.then()` chaining works
- Misunderstanding what `EventEmitter` is for

### ✅ Try This Live

> “Let’s write a tiny async program together!”

```js
const { writeFile, readFile } = require("fs").promises;

const writeAndRead = async () => {
  try {
    await writeFile("temp.txt", "Hello Code the Dream!");
    const result = await readFile("temp.txt", "utf8");
    console.log(result);
  } catch (err) {
    console.error("Something went wrong:", err);
  }
};

writeAndRead();
```
**Follow-up:**
  * Ask students: “What happens if you forget await?”
  * Add a second writeFile and discuss chaining

 ## 💡 Optional Challenges (Advanced or Fast Groups)
 * Modify the above to emit a custom event ("file-written") after the file is saved
 * Convert the above code into .then() chaining instead of async/await
 * Build a timer that emits an event every 3 seconds, logs it, and stops after 5 events

## 📎 Resources & Links

- [Assignment Instructions (Week 2)](https://raw.githubusercontent.com/Code-the-Dream-School/node-v3/refs/heads/main/assignments/02NPMandAsyncPatterns.md)
- [Node.js/Express Mentor Guidebook Wiki](https://github.com/Code-the-Dream-School/node-express-guidebook/wiki/Curriculum-and-Teaching-Resources)
- [MDN: Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
- [Video: What the heck is the event loop anyway?](https://www.youtube.com/watch?v=8aGhZQkoFbQ)

## ✅ Quick Checklist

- [ ] Pick an Explore or Apply focus for your session
- [ ] Try a "Live Coding" prompt with your group
- [ ] Help students identify bugs in their async code
- [ ] Submit your [Mentor Session Report](https://airtable.com/appoSRJMlXH9KvE6w/shrp0jjRtoMyTXRzh) after class
