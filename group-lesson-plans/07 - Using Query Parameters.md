# 🌐 Node Week 7: Using Query Parameters

## 🚀 Key Concepts

### 1. **Query Parameters & Flexible Filtering**
Students are extending their API to support dynamic filtering via query parameters (e.g., `?featured=true&company=ikea`), allowing end users to query for products based on fields like:
- `featured` (boolean)
- `name` (regex match)
- `company` (exact match)
- `price` and `rating` (numeric comparisons)

They’ll learn to parse `req.query`, dynamically build a `queryObject`, and pass it into `Product.find()`.

### 2. **Thenables**
Mongoose methods like `Product.find()` return a *thenable* — an object that behaves like a promise but also allows method chaining. The full query (including `.sort()`, `.select()`, `.skip()`, `.limit()`) is only executed when the query is `await`ed.

```js
let result = Product.find(queryObject)
  .sort(sortList)
  .select(fieldsList);
const products = await result;
```

This concept may be new for students who assume every asynchronous call must be immediately awaited.

### 3. **Regular Expressions**
Students use regex to implement partial name matching. The concept won’t be taught in depth, but they’re expected to understand that `name: { $regex: name, $options: "i" }` filters based on case-insensitive substring matches.

### 4. **Pagination**
Students add support for pagination through `skip` and `limit` query parameters, e.g.:
```
?page=2&limit=10
```
This means they skip `(page - 1) * limit` and then limit the number of results returned.

## 🧠 Mindset Focus: Knowing When to Ask for Help

The mindset lesson this week revisits **asking for help** — not the *how*, but the *when*:
- Students are encouraged to move beyond asking at the first sign of trouble, but also not to wait too long out of pride.
- They’ll reflect on a model of “inner/middle/outer circles”:
  - Inner = things you know
  - Middle = things you can figure out
  - Outer = things you *won’t* figure out alone
- Mentors can guide students to identify when they’ve crossed into the outer ring and need support.

📝 Encourage students to:
- Verbally explain their approach so far (rubber duck!)
- Talk through what they’ve tested
- Compare with the solution code if they’re truly stuck

## 🔧 Common Sticking Points

### ❌ Misunderstanding Thenables
- Students might not realize why `.sort()` or `.select()` don’t return anything themselves — remind them that these are methods chaining onto a query object.

### ❌ Incorrect Parsing of Query Params
- Some students will try to destructure directly from `req.query` without checking for existence.
- Others might try to apply sort, skip, or limit logic before confirming valid values.

### ❌ Regex Confusion
- Don’t expect mastery — guide them to borrow the regex expression from the sample code.

## 🧪 Practice Prompts

### Explore
- What happens if you chain `.sort()` *before* `.find()`?
- Try logging `req.query` with different URL strings.
- How would you filter for items where `rating >= 4.5`?

### Apply
- Add support for filtering by `price` range using `numericFilters`.
- Implement support for `fields=name,price` to only return selected fields.

## 🧰 Tools & Links

- [🧪 Instructor Solution](https://github.com/Code-the-Dream-School/node-v3/tree/main/assignments/07QueryParameters.md)
- [🧠 Debugging Practices](https://www.rithmschool.com/blog/debugging-like-a-scientist)
- [📖 How to Ask for Help at Work (HBR)](https://hbr.org/2021/04/how-to-ask-for-help-at-work)
- [🧩 Regex Tutorial](https://regexone.com/)
- [🎯 RMOR Comprehension Check](https://airtable.com/appoSRJMlXH9KvE6w/shrBpqHbS6wgInoF9?prefill_Lessons=Node%20v3%3A%20Lesson%207%20-%20Using%20Query%20Parameters)

## 🧑‍🏫 Mentor Tips

- Encourage exploration of Postman queries — it’s critical for understanding how parameters interact.
- Help demystify the "magic" of chaining Mongoose methods. Once students see the `.find()` query as a *builder*, the rest clicks.
- If students aren’t using pagination correctly, have them log the computed `skip` and `limit` values.
