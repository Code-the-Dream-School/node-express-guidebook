# Lesson 7: Using Query Parameters - Assignment Review Guide

| Week | Topic                    | Learning Objective |
|------|--------------------------|--------------------|
| 7    | Query Parameters with MongoDB | Students will be able to parse query parameters from REST requests, build dynamic MongoDB queries using Mongoose thenables, implement filtering by multiple attributes, add sorting and pagination, and use comparison operators for numeric fields.

## Assignment Overview

Students work in the `04-store-api/starter` directory to build an API that allows searching products by multiple criteria including:
- `featured` (boolean)
- `name` (string with regex matching)
- `price` (numeric with comparison operators)
- `rating` (numeric with comparison operators)  
- `company` (string)

Students also implement:
- Sorting (ascending/descending)
- Pagination with `skip` and `limit`
- Field selection to limit returned data

**Key File:** `controllers/product.js` - contains `getAllProducts()` and `getAllProductsStatic()`

## Assignment Rubric

You can mark the student's assignment as complete if they:

- [ ] Created a `week7` branch from an updated `main` branch with week 6 merged
- [ ] Ran `npm install` in the `04-store-api/starter` directory
- [ ] Implemented query parameter parsing in `getAllProducts()`
- [ ] Built dynamic MongoDB queries using the thenable pattern
- [ ] Implemented filtering by `featured`, `name`, `company`, `price`, and `rating`
- [ ] Added comparison operators for numeric fields (`>`, `>=`, `<`, `<=`, `=`)
- [ ] Implemented sorting with ascending/descending order
- [ ] Added pagination with `skip` and `limit` parameters
- [ ] Implemented field selection with `select()`
- [ ] Tested all functionality with Postman
- [ ] All routes return appropriate responses

## Core Concepts to Check

### 1. Thenable Pattern
Students should understand and use the pattern where Mongoose queries are chained before being executed:

```javascript
let result = Product.find(queryObject);

// Chain additional operations
if (sort) {
  result = result.sort(sortList);
}

if (fields) {
  result = result.select(fieldsList);
}

if (skip) {
  result = result.skip(Number(skip));
}

if (limit) {
  result = result.limit(Number(limit));
}

// Query only executes when awaited
const products = await result;
```

**Key points:**
- The query doesn't execute until `await` is called
- Each method returns a thenable that can be further chained
- This allows building dynamic queries based on provided parameters

### 2. Query Parameter Parsing
Students should extract and use query parameters from `req.query`:

```javascript
const getAllProducts = async (req, res) => {
  const { featured, company, name, sort, fields, skip, limit } = req.query;
  const queryObject = {};
  
  // Build query object based on provided parameters
  if (featured) {
    queryObject.featured = featured === 'true';
  }
  
  if (company) {
    queryObject.company = company;
  }
  
  if (name) {
    queryObject.name = { $regex: name, $options: 'i' };
  }
  
  // Continue building query...
};
```

### 3. Numeric Comparisons
For `price` and `rating`, students should handle comparison operators:

```javascript
// Input: ?price=>40 or ?rating=<4.5
const numericFilters = req.query.numericFilters;

if (numericFilters) {
  const operatorMap = {
    '>': '$gt',
    '>=': '$gte',
    '=': '$eq',
    '<': '$lt',
    '<=': '$lte'
  };
  
  const regEx = /\b(<|>|>=|=|<=)\b/g;
  let filters = numericFilters.replace(
    regEx,
    (match) => `-${operatorMap[match]}-`
  );
  
  const options = ['price', 'rating'];
  filters = filters.split(',').forEach((item) => {
    const [field, operator, value] = item.split('-');
    if (options.includes(field)) {
      queryObject[field] = { [operator]: Number(value) };
    }
  });
}
```

### 4. Sorting
Students should implement sorting with ascending/descending:

```javascript
if (sort) {
  const sortList = sort.split(',').join(' ');
  result = result.sort(sortList);
} else {
  result = result.sort('createdAt'); // Default sort
}
```

**Examples:**
- `?sort=name` - ascending by name
- `?sort=-price` - descending by price  
- `?sort=company,price` - sort by company, then price

### 5. Field Selection
Students should implement field limiting:

```javascript
if (fields) {
  const fieldsList = fields.split(',').join(' ');
  result = result.select(fieldsList);
} else {
  result = result.select('-__v'); // Exclude version field by default
}
```

**Examples:**
- `?fields=name,price` - only return name and price
- `?fields=-company` - return all except company

### 6. Pagination
Students should implement skip and limit:

```javascript
const page = Number(req.query.page) || 1;
const limit = Number(req.query.limit) || 10;
const skip = (page - 1) * limit;

result = result.skip(skip).limit(limit);
```

## Sample Request Examples

Students should test these scenarios in Postman:

```
GET /api/v1/products
GET /api/v1/products?featured=true
GET /api/v1/products?company=ikea
GET /api/v1/products?name=table
GET /api/v1/products?sort=price
GET /api/v1/products?sort=-rating
GET /api/v1/products?fields=name,price,company
GET /api/v1/products?numericFilters=price>40,rating>=4
GET /api/v1/products?page=2&limit=5
GET /api/v1/products?featured=true&company=ikea&sort=price&fields=name,price
```

## Common Issues to Watch For

### Conceptual Misunderstandings
* **Not understanding thenables:** Trying to await `Product.find()` immediately instead of chaining operations
* **String vs boolean for featured:** Not converting `'true'` string to boolean `true`
* **Regex for name search:** Not using `$regex` and `$options: 'i'` for case-insensitive matching
* **Operator syntax:** Not properly replacing user-friendly operators (`>`, `<`) with MongoDB operators (`$gt`, `$lt`)

### Technical Errors
* **Not running npm install:** Missing dependencies cause crashes
* **Wrong directory:** Working in `final` instead of `starter`
* **Type conversion errors:** Not converting numeric strings to numbers for price/rating/limit/skip
* **Regex mistakes:** Students may struggle with the regular expression for operator replacement
* **Query object structure:** Incorrect nesting of MongoDB operators

### Assignment-Specific Issues
* **Testing only with getAllProductsStatic:** Not implementing in `getAllProducts()` 
* **Copying from final without understanding:** Code works but student can't explain it
* **Missing error handling:** Not wrapping in try-catch blocks
* **Hardcoded values:** Using specific values instead of dynamic query parameters

## Sample Correct Implementation

```javascript
const getAllProducts = async (req, res) => {
  try {
    const { featured, company, name, sort, fields, numericFilters } = req.query;
    const queryObject = {};

    // Boolean filter
    if (featured) {
      queryObject.featured = featured === 'true';
    }

    // String filters
    if (company) {
      queryObject.company = company;
    }

    if (name) {
      queryObject.name = { $regex: name, $options: 'i' };
    }

    // Numeric filters
    if (numericFilters) {
      const operatorMap = {
        '>': '$gt',
        '>=': '$gte',
        '=': '$eq',
        '<': '$lt',
        '<=': '$lte',
      };
      const regEx = /\b(<|>|>=|=|<=)\b/g;
      let filters = numericFilters.replace(
        regEx,
        (match) => `-${operatorMap[match]}-`
      );
      const options = ['price', 'rating'];
      filters.split(',').forEach((item) => {
        const [field, operator, value] = item.split('-');
        if (options.includes(field)) {
          queryObject[field] = { [operator]: Number(value) };
        }
      });
    }

    // Start building query
    let result = Product.find(queryObject);

    // Sorting
    if (sort) {
      const sortList = sort.split(',').join(' ');
      result = result.sort(sortList);
    } else {
      result = result.sort('createdAt');
    }

    // Field selection
    if (fields) {
      const fieldsList = fields.split(',').join(' ');
      result = result.select(fieldsList);
    }

    // Pagination
    const page = Number(req.query.page) || 1;
    const limit = Number(req.query.limit) || 10;
    const skip = (page - 1) * limit;

    result = result.skip(skip).limit(limit);

    // Execute query
    const products = await result;

    res.status(200).json({ products, nbHits: products.length });
  } catch (error) {
    res.status(500).json({ msg: error.message });
  }
};
```

## Variations That Are Acceptable

* **Different default sort:** Some students may use different default sorting
* **Different default limit:** Pagination defaults may vary
* **Additional filters:** Students may add extra filtering capabilities
* **Different error messages:** As long as errors are handled appropriately
* **Variable naming:** Different names for intermediate variables (e.g., `filters` vs `numericFilters`)

## Red Flags (Request Revisions)

* **No dynamic query building:** Hardcoded filters instead of using query parameters
* **No thenable chaining:** Not building up the query before awaiting
* **Missing numeric comparisons:** Not implementing operators for price/rating
* **No regex for name:** Using exact match instead of pattern matching
* **Not tested:** Student can't demonstrate working queries in Postman
* **Copied without understanding:** Student can't explain the operator replacement regex

## Debugging Tips to Share

**If queries aren't working:**
1. Console.log the `queryObject` to see what's being sent to MongoDB
2. Check Postman to ensure query parameters are formatted correctly
3. Verify the data in MongoDB matches what you're querying for
4. Test each filter individually before combining them

**For numeric filters:**
1. Log the `numericFilters` string before processing
2. Log after regex replacement to see the transformation
3. Check that fields are being converted to numbers
4. Verify operator names match MongoDB's format (`$gt`, not `gt`)

## Feedback Tips

**Encourage:**
* "Great job implementing the thenable pattern - this keeps queries flexible!"
* "Your numeric filter logic correctly handles multiple operators"
* "Nice work testing all the different query combinations"

**Suggest improvements:**
* "Try adding validation to ensure numeric values are actually numbers"
* "Consider adding bounds checking for pagination (page must be positive)"
* "Your code works but could benefit from comments explaining the regex replacement"

**For corrections:**
* "The `featured` parameter is coming in as a string - you'll need to convert 'true' to boolean true"
* "Remember to chain operations on the `result` variable before awaiting"
* "The regex pattern needs to match MongoDB's field names exactly - check your spelling"
