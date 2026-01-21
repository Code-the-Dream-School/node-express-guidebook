### Group Mentor Guide**

#### **Week 9: Jobs API Part 1 — Group Mentor Guide**
Welcome to Week 9! This week, students begin an iterative project—the **Jobs API**—which they may choose to adapt into their final project. The focus is on **Authentication with JWT**, **Access Control**, and creating a data model with **Mongoose**.

#### **Warm-Up (5–10 minutes)**
Choose one:
**Relationship-Building (Mindset: Willingness to Experiment)**
* How do you usually feel when you see a "bright red error message"? Does it feel like a failure or a gift?
* Share a time you failed at something multiple times before getting it right (sports, gaming, etc.). How did you stay motivated?

**Check for Understanding (from JWT Basics)**
* What information do we typically store in a User record in MongoDB? (Answer: Name, email, and hashed password).
* Why don't we store passwords in plain text?.

#### **Explore vs. Apply — Session Formats**
* **Explore Sessions** → Walk through the **User model** setup, demonstrating how `bcryptjs` hashes passwords in a pre-save middleware.
* **Apply Sessions** → Debugging **Postman** tests, setting up the new Git repository, or helping students brainstorm their own custom models.

#### **Sample Timing for 1-Hour Session**
| Time | Activity |
| ------ | ------ |
| 0:00–0:10 | Warm-up + Review mindset: Embracing failure as a key to learning |
| 0:10–0:30 | Explore: JWT generation, `bcryptjs` hashing, and the `this` keyword |
| 0:30–0:50 | Apply: Live testing routes in Postman or refining custom models |
| 0:50–1:00 | Wrap-up + Final questions |

#### **Check for Understanding (Ask 2–3)**
* Why must we use the `function` keyword instead of arrow functions when adding instance methods to the User model? (Answer: To ensure the `this` variable correctly refers to the user instance).
* What is an `enum` type, and when should you use it in your model?.
* How does the `createdBy` field help with access control?.
* Where is the User ID stored after the authentication middleware checks the JWT? (Answer: `req.user`).

#### **Explore Prompts**
* **Hashing Middleware:** Let's look at the `.save()` operation. How does the middleware know to run *before* the data is saved?.
* **Custom Models:** If you aren't building a Jobs API, what kind of application would you like to invent? What attributes (strings, numbers, dates) would your model need?.
* **JWT Flow:** Let's trace a request from Postman through the authentication middleware to a protected route.

#### **Apply Prompts (Assignment Hotspots)**
* **Repository Setup:** Ensure students forked the *new* repository and are not working inside the old `node-express-course` folder.
* **Missing `createdBy`:** Check if the student's model includes a `createdBy` attribute with the type `mongoose.Types.ObjectId`.
* **Postman Testing:** If a route isn't working, let's look at the error message together—remember, these messages are a "gift" for debugging!.

#### **Optional Challenges**
* **Iterative Design:** Discuss how this project can be extended for a final project using either a front end or server-side rendering.
* **Flexbox Break:** If the group needs a mental break, play **Flexbox Froggy** or **Grid Garden** to keep CSS skills sharp.
