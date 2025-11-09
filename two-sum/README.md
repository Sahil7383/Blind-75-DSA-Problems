# 🤩 Two Sum — All Approaches with Explanation

> **Problem:**
> Given an array of integers `nums` and an integer `target`, return **indices of the two numbers** such that they add up to the target.

---

## 🧏‍♂️ 1. Brute Force Approach

### 🔹 Idea

Check every possible pair of numbers and see if they add up to the target.

### 🔹 Code

```js
var twoSum = function (nums, target) {
  for (let i = 0; i < nums.length; i++) {
    for (let j = i + 1; j < nums.length; j++) {
      if (nums[i] + nums[j] === target) {
        return [i, j];
      }
    }
  }
};
```

### ⏱️ Time Complexity

- **O(n²)** → Two nested loops.

### 💾 Space Complexity

- **O(1)** → No extra data structures used.

### ✅ Pros

- Simple and intuitive.

### ❌ Cons

- Very slow for large arrays.

---

## 🥇 2. Hash Map (Optimal O(n) Approach)

### 🔹 Idea

Use a hash map to store previously seen numbers and their indices.
For each number, check if its complement (`target - nums[i]`) exists in the map.

### 🔹 Code

```js
var twoSum = function (nums, target) {
  const map = new Map();

  for (let i = 0; i < nums.length; i++) {
    const complement = target - nums[i];
    if (map.has(complement)) {
      return [map.get(complement), i];
    }
    map.set(nums[i], i);
  }
};
```

### ⏱️ Time Complexity

- **O(n)** → Each element is visited once.

### 💾 Space Complexity

- **O(n)** → Hash map stores up to `n` elements.

### ✅ Pros

- Fastest possible solution.
- Works on unsorted arrays.

### ❌ Cons

- Slightly more space used due to the map.

---

## 🥇 3. Two-Pointer Approach (on Sorted Array)

### 🔹 Idea

If the array is **sorted**, use two pointers:
– One at the beginning (`left`)
– One at the end (`right`)
Move them inward based on the sum.

### 🔹 Code

```js
var twoSum = function (nums, target) {
  let left = 0;
  let right = nums.length - 1;

  while (left < right) {
    const sum = nums[left] + nums[right];

    if (sum === target) return [left, right];
    else if (sum < target) left++;
    else right--;
  }

  return [];
};
```

### ⏱️ Time Complexity

- **O(n)** → Each element is visited once.

### 💾 Space Complexity

- **O(1)** → Constant space.

### ✅ Pros

- Very efficient for sorted arrays.
- Clean logic.

### ❌ Cons

- Doesn’t work on unsorted arrays.

---

## 🌟 4. Two-Pointer (with Sorting while keeping original indices)

### 🔹 Idea

If the input array is **not sorted**, first pair each number with its original index, sort by value, and then apply two-pointer logic.

### 🔹 Code

```js
var twoSum = function (nums, target) {
  const arr = nums.map((num, i) => [num, i]);
  arr.sort((a, b) => a[0] - b[0]);

  let left = 0;
  let right = arr.length - 1;

  while (left < right) {
    const sum = arr[left][0] + arr[right][0];
    if (sum === target) {
      return [arr[left][1], arr[right][1]];
    } else if (sum < target) {
      left++;
    } else {
      right--;
    }
  }

  return [];
};
```

### ⏱️ Time Complexity

- **O(n log n)** → Sorting dominates.

### 💾 Space Complexity

- **O(n)** → For the paired array `[value, index]`.

### ✅ Pros

- Works on unsorted arrays.
- Still efficient.

### ❌ Cons

- Slightly slower than hash map due to sorting.
- Uses extra space.

---

## 🧠 Summary Table

| Approach                          | Works on Unsorted? | Time Complexity | Space Complexity | Notes                |
| --------------------------------- | ------------------ | --------------- | ---------------- | -------------------- |
| Brute Force                       | ✅                 | O(n²)           | O(1)             | Easiest but slow     |
| Hash Map                          | ✅                 | O(n)            | O(n)             | Fastest overall      |
| Two Pointer (sorted input)        | ❌                 | O(n)            | O(1)             | Only works if sorted |
| Two Pointer + Sort (keep indices) | ✅                 | O(n log n)      | O(n)             | Clean and efficient  |

---

## 🚀 Recommendation

| Situation                                        | Best Approach                    |
| ------------------------------------------------ | -------------------------------- |
| Array is **unsorted**                            | ✅ **Hash Map** (O(n))           |
| Array is **sorted**                              | ✅ **Two Pointers** (O(n))       |
| You want to **practice sorting + pointer logic** | ✅ **Two Pointers with sorting** |
