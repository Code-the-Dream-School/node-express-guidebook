### Assignment Review Guide**

#### **Lesson 9: Jobs API Part 1**
| Week | Topic | Learning Objective |
| ------ | ------ | ------ |
| 9 | Jobs API Part 1 | Students will begin a CRUD API project, implement JWT authentication, hash passwords with bcryptjs, and establish access control using Mongoose models. |

#### **Assignment Rubric**
You can mark the student's assignment as complete if they:
* [ ] Forked and cloned the specific `06-jobs-api` repository (not working in the starter directory of the old course repo).
* [ ] Created a `week9` git branch.
* [ ] Implemented a **User model** that hashes passwords using `bcryptjs` and includes JWT generation methods.
* [ ] Created either a **Job model** or a **custom model** (e.g., for a final project idea).
* [ ] Included a `createdBy` field in their model linked to `mongoose.Types.ObjectId`.
* [ ] Used an `enum` type for at least one model attribute.
* [ ] Tested all API routes using **Postman**.

#### **What to Look For**
* **Authentication Middleware:** Ensure routes are protected and that the User ID from the JWT is being stored in `req.user`.
* **Access Control:** In the controllers, check if the student is including the User ID in Mongoose queries to ensure users only modify their own records.
* **Instance Methods:** Verify they used the `function` keyword for methods involving `this` (like generating tokens or validating passwords).
* **Security:** Confirm passwords are not stored in plain text and that `bcryptjs` is used in a pre-save routine.

#### **Sample Code Reference**
*Required User Model Instance Method Syntax:*
```javascript
// Correct use of function keyword for 'this' binding
userSchema.methods.createJWT = function () {
  return jwt.sign({ userId: this._id, name: this.name }, ...);
}
```

*Required createdBy Reference:*
```javascript
createdBy: {
  type: mongoose.Types.ObjectId,
  ref: 'User',
  required: [true, 'Please provide user']
}
```
