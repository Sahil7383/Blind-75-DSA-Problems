# 🤩 Contains Duplicate — All Approaches with Explanation

> **Problem:**
> Given an integer array `nums`, return `true` if any value appears **at least twice** in the array, and `false` if every element is distinct.

---

## 🧏‍♂️ 1. Brute Force Approach

### 🔹 Idea

Compare every element with every other element.

### 🔹 Code

```js
var containsDuplicate = function (nums) {
  for (let i = 0; i < nums.length; i++) {
    for (let j = i + 1; j < nums.length; j++) {
      if (nums[i] === nums[j]) {
        return true;
      }
    }
  }
  return false;
};
```

### ⏱️ Time Complexity

- **O(n²)** — two nested loops.

### 💾 Space Complexity

- **O(1)** — no extra data structures.

### ✅ Pros

- Simple to understand.

### ❌ Cons

- Extremely slow for large arrays.

---

## 👨‍🔧 2. Sorting Approach

### 🔹 Idea

If the array is sorted, duplicates will appear **next to each other**.
So, sort the array and then check if any adjacent elements are equal.

### 🔹 Code

```js
var containsDuplicate = function (nums) {
  nums.sort((a, b) => a - b);
  for (let i = 0; i < nums.length - 1; i++) {
    if (nums[i] === nums[i + 1]) {
      return true;
    }
  }
  return false;
};
```

### ⏱️ Time Complexity

- **O(n log n)** — due to sorting.

### 💾 Space Complexity

- **O(1)** (or **O(n)** depending on sorting algorithm used in JS).

### ✅ Pros

- Easy to implement.
- No additional data structures (in code).

### ❌ Cons

- Slightly slower than using a hash structure.
- Sorting changes the array order (if that matters).

---

## 🥇 3. Hash Set Approach (Optimal)

### 🔹 Idea

Use a `Set` (hash-based data structure) to keep track of seen elements.
If you encounter a number already in the set → it’s a duplicate.

### 🔹 Code

```js
var containsDuplicate = function (nums) {
  const seen = new Set();

  for (const num of nums) {
    if (seen.has(num)) {
      return true;
    }
    seen.add(num);
  }
  return false;
};
```

### ⏱️ Time Complexity

- **O(n)** — each lookup and insertion in a `Set` is O(1) on average.

### 💾 Space Complexity

- **O(n)** — in the worst case, all numbers are unique and stored in the set.

### ✅ Pros

- Fastest approach.
- Very clean and readable.

### ❌ Cons

- Uses extra memory.

---

## 🔍 One-Liner (Using Set)

```js
var containsDuplicate = function (nums) {
  return new Set(nums).size !== nums.length;
};
```

### 🔹 Explanation:

- `new Set(nums)` automatically removes duplicates.
- If the set’s size is smaller than the array’s length → duplicates exist.

---

## 🧠 Summary Table

| Approach    | Time Complexity | Space Complexity | Works Efficiently? | Notes                            |
| ----------- | --------------- | ---------------- | ------------------ | -------------------------------- |
| Brute Force | O(n²)           | O(1)             | ❌                 | Very slow, only for small inputs |
| Sorting     | O(n log n)      | O(1)/O(n)        | ✅                 | Good, but changes order          |
| Hash Set    | O(n)            | O(n)             | ✅✅✅             | Fastest and most common          |
| One-Liner   | O(n)            | O(n)             | ✅                 | Compact version of Set approach  |

---

## 🚀 Recommendation

| Situation                                                  | Best Approach      |
| ---------------------------------------------------------- | ------------------ |
| You want the **simplest and fastest** solution             | ✅ **Hash Set**    |
| You need to **avoid extra space** and order doesn’t matter | ✅ **Sorting**     |
| You’re learning brute-force basics                         | ✅ **Double loop** |
