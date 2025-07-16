# Week 2: NPM & Async Patterns — Group Mentor Guide

Welcome to Week 2! This week, students learned about:

- Using `npm` and managing project dependencies
- Writing asynchronous code with Promises and `async/await`
- Node’s EventEmitter system and streams

They continued working in the `01-node-tutorial/answers` directory using the same repo they set up last week.

## 🧊 Warm-Up (5–10 minutes)

Choose **one** of these to build connection or review past content:

**👋 Relationship-Building**
- What’s a small win you had this week (coding or non-coding)?
- What’s one piece of tech you use every day that you don’t fully understand?

**💡 Check for Understanding (from Week 1)**
- What’s one thing you remember about how Node handles files?
- Who remembers what `__dirname` is?
- What was confusing about setting up your repo or project structure?

## 🧭 Explore vs. Apply — Session Formats

**Explore Sessions** → Big-picture understanding, discussion, mini-demos  
**Apply Sessions** → Practice with guidance, code review, debugging

**Mix-and-match** is totally fine!

## ⏱️ Sample Timing for 1-Hour Session

| Time      | Activity                            |
|-----------|-------------------------------------|
| 0:00–0:10 | Warm-up + review of last week       |
| 0:10–0:30 | Explore concepts or code walkthrough |
| 0:30–0:50 | Apply: troubleshoot assignment code  |
| 0:50–1:00 | Wrap-up + reflection/check-in        |

## ❓ CFU (Check for Understanding) Questions

Before diving into coding or discussion, use 2–3 of these to check where students are:

- What’s the difference between `npm install` and `npm install --save-dev`?
- What’s a Promise? When do you use `await`?
- Why might we use `try/catch` with async code?
- What does `EventEmitter` let us do?

## 🧑‍🏫 Explore Prompts (Pick 1–2)

Use these for live practice, assignment troubleshooting, or group problem-solving. Remember to use the ["I Do, We Do, You Do" model of gradual release](https://coda.io/d/_dAM9Xiy8hnR/Teaching-Notes_suWDehoD) for mentor sessions.

- Why is async programming so important in Node?
- When might you use `.then()` chaining instead of `await`?
- How does an event-driven system help scalability?
- What exactly happens when you run `npm install`?

## 🛠️ Apply Prompts (Pick 1–2)

Use these for live practice, assignment troubleshooting, or group problem-solving. Remember to use the ["I Do, We Do, You Do" model of gradual release](https://coda.io/d/_dAM9Xiy8hnR/Teaching-Notes_suWDehoD) for mentor sessions.

Focus on the actual code students are writing. Share screens or live-code as a group.

### 🔧 Assignment Hotspots
- Forgot to `await` inside `async` functions
- Not wrapping async code in `try/catch`
- Using `await` outside of an `async` function (syntax error)
- Misunderstanding what `.then()` returns or when `.catch()` runs

### ✅ Try This Live

> “Let’s write a tiny async program together!”

<pre><code class="language-js">
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
</code></pre>

Ask:
- “What happens if you forget `await`?”
- “Can we rewrite this using `.then()` chaining?”

## 💬 Engagement Strategies (if students are quiet)

- **Think Time + Chat**: “Take a minute to try this yourself. Then post your code or question in the chat.”
- **Pick One**: “Which of these async patterns would *you* rather use and why: `async/await` or `.then()`?”
- **Vote + Explain**: “Raise your hand (or emoji) if you’ve ever seen a `Promise {<pending>}` in your terminal — what caused it?”
- **Start Messy**: “Let’s write some broken code and fix it together!”

## 💡 Optional Challenges

For advanced students or extra practice:

- Emit a custom event after writing to a file
- Chain three Promises using `.then()`
- Create an event handler that waits for an event using a Promise

## 📎 Resources & Links

- [Assignment Instructions (Week 2)](https://raw.githubusercontent.com/Code-the-Dream-School/node-v3/refs/heads/main/assignments/02NPMandAsyncPatterns.md)
- [Mentor Guidebook: Node.js](https://github.com/Code-the-Dream-School/node-express-guidebook/wiki/Curriculum-and-Teaching-Resources)
- [MDN: Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
- [Video: What the heck is the event loop anyway?](https://www.youtube.com/watch?v=8aGhZQkoFbQ)

## ✅ Mentor To-Do

- [ ] Run a session based on the options above
- [ ] Help students debug async code or assignment logic
- [ ] Submit your [Mentor Session Report](https://airtable.com/appoSRJMlXH9KvE6w/shrp0jjRtoMyTXRzh) after class
