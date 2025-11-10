# 🤩 Product of Array Except Self — All Approaches with Explanation

> **Problem:**  
> Given an integer array `nums`, return an array `answer` such that `answer[i]` is equal to the product of all elements of `nums` except `nums[i]`.  
> You must solve it **without using division** and in **O(n)** time.

---

## 🧠 Example

### Input

```js
nums = [1, 2, 3, 4];
Output
js
Copy code
[24, 12, 8, 6];
Explanation
For index 0: 2 × 3 × 4 = 24

For index 1: 1 × 3 × 4 = 12

For index 2: 1 × 2 × 4 = 8

For index 3: 1 × 2 × 3 = 6

🧏‍♂️ 1. Brute Force Approach
🔹 Idea
For every element, multiply all other elements except itself.

🔹 Code
js
Copy code
var productExceptSelf = function (nums) {
  const n = nums.length;
  const result = [];

  for (let i = 0; i < n; i++) {
    let product = 1;
    for (let j = 0; j < n; j++) {
      if (i !== j) product *= nums[j];
    }
    result[i] = product;
  }

  return result;
};
⏱️ Time Complexity
O(n²) — two nested loops.

💾 Space Complexity
O(1) — no extra structures (excluding output).

✅ Pros
Simple and easy to understand.

❌ Cons
Very slow for large arrays.

⚙️ 2. Division Method (⚠️ Not Allowed in Most Interviews)
🔹 Idea
Multiply all numbers to get the total product, then divide by each element.
Handle zeros carefully.

🔹 Code
js
Copy code
var productExceptSelf = function (nums) {
  let totalProduct = 1;
  let zeroCount = 0;

  for (let num of nums) {
    if (num === 0) zeroCount++;
    else totalProduct *= num;
  }

  const result = new Array(nums.length).fill(0);

  if (zeroCount > 1) return result; // Multiple zeros → all zero

  for (let i = 0; i < nums.length; i++) {
    if (zeroCount === 0) result[i] = totalProduct / nums[i];
    else if (nums[i] === 0) result[i] = totalProduct;
  }

  return result;
};
⏱️ Time Complexity
O(n) — single traversal and result computation.

💾 Space Complexity
O(1) — constant extra space.

✅ Pros
Easy to code and short.

❌ Cons
❌ Division not allowed in problem statement.

❌ Must handle zeros carefully.

👨‍🔧 3. Prefix and Suffix Arrays (Without Division)
🔹 Idea
Compute the product of all numbers before an index (prefix)
and product of all numbers after it (suffix).
Then multiply both to get the final result.

🔹 Code
js
Copy code
var productExceptSelf = function (nums) {
  const n = nums.length;
  const prefix = new Array(n).fill(1);
  const suffix = new Array(n).fill(1);
  const result = new Array(n);

  // Prefix array
  for (let i = 1; i < n; i++) {
    prefix[i] = prefix[i - 1] * nums[i - 1];
  }

  // Suffix array
  for (let i = n - 2; i >= 0; i--) {
    suffix[i] = suffix[i + 1] * nums[i + 1];
  }

  // Multiply prefix and suffix
  for (let i = 0; i < n; i++) {
    result[i] = prefix[i] * suffix[i];
  }

  return result;
};
⏱️ Time Complexity
O(n) — three linear passes.

💾 Space Complexity
O(n) — prefix and suffix arrays.

✅ Pros
Easy to understand.

Works without division.

❌ Cons
Uses extra space.

🥇 4. Optimized Prefix–Suffix (Best Approach)
🔹 Idea
Use a single result array:

Compute prefix products (left → right).

Multiply suffix products (right → left) in the same array.

🔹 Code
js
Copy code
var productExceptSelf = function (nums) {
  const n = nums.length;
  const result = new Array(n).fill(1);

  // Step 1: Prefix
  let prefix = 1;
  for (let i = 0; i < n; i++) {
    result[i] = prefix;
    prefix *= nums[i];
  }

  // Step 2: Suffix
  let suffix = 1;
  for (let i = n - 1; i >= 0; i--) {
    result[i] *= suffix;
    suffix *= nums[i];
  }

  return result;
};
⏱️ Time Complexity
O(n) — two linear passes.

💾 Space Complexity
O(1) — constant space (output excluded).

✅ Pros
✅ Fastest approach.

✅ No division used.

✅ O(1) extra space.

❌ Cons
Slightly tricky to reason about initially.

🧩 Step-by-Step Example
For nums = [1, 2, 3, 4]:

i	nums[i]	prefix before	result (after prefix)	suffix before	result (final)
0	1	1	1	24	24
1	2	1	1	12	12
2	3	2	2	4	8
3	4	6	6	1	6

✅ Final Output: [24, 12, 8, 6]

🧾 Summary Table
Approach	Uses Division	Time Complexity	Space Complexity	Works Efficiently?	Notes
Brute Force	❌	O(n²)	O(1)	❌	Too slow
Division	✅	O(n)	O(1)	⚠️	Not allowed
Prefix + Suffix Arrays	❌	O(n)	O(n)	✅	Clear logic
Optimized Prefix–Suffix	❌	O(n)	O(1)	✅✅✅	Best approach
```
