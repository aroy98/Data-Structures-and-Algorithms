# 🧠 Problem Solving Techniques

---

## 🧩 1. Introduction to Problem Solving

**Problem Solving** is the process of identifying a challenge, analyzing it, and developing an efficient algorithmic solution. For programmers, problem-solving means writing **correct, efficient, and scalable** code.

### ✅ Core Phases:

1. **Understand the Problem** — What are you solving?
2. **Plan the Solution** — Think of logic or algorithms.
3. **Implement** — Write clean, modular code.
4. **Test and Optimize** — Handle edge cases and improve efficiency.

---

## ⚙️ 2. General Problem-Solving Strategies

| Technique                   | Description                             | Example                                        |
| --------------------------- | --------------------------------------- | ---------------------------------------------- |
| **Brute Force**             | Try every possible solution             | Linear Search                                  |
| **Divide and Conquer**      | Break into smaller subproblems          | Merge Sort                                     |
| **Dynamic Programming**     | Use memoization to reuse sub-results    | Fibonacci Sequence                             |
| **Greedy Approach**         | Pick best option at each step           | Activity Selection                             |
| **Backtracking**            | Explore all paths, prune invalid ones   | N-Queens Problem                               |
| **Recursion**               | Define problem in terms of itself       | Factorial, Tree Traversal                      |
| **Two Pointers**            | Use two moving indices                  | Pair Sum in Sorted Array                       |
| **Sliding Window**          | Fixed or variable window to track range | Longest Substring Without Repeating Characters |
| **Binary Search on Answer** | Use binary search over potential result | Minimum Days to Make Bouquets                  |

---

## 🔍 3. Step-by-Step Problem Solving Framework

### Step 1 — Understand the Problem

* Read carefully.
* Identify **input, output**, and **constraints**.
* Ask questions like:

  * Can input be empty or negative?
  * What are edge cases?

### Step 2 — Plan the Logic

* Choose an approach (brute force or optimized).
* Write pseudocode before coding.

### Step 3 — Implement

* Start with brute-force.
* Then optimize step-by-step.

### Step 4 — Test and Optimize

* Check boundary cases.
* Measure time complexity.

---

## 🔢 4. Example Problems by Technique

### 🧮 4.1 Brute Force — *Two Sum Problem*

**Problem:** Find two numbers that sum to a target.

```javascript
function twoSum(arr, target) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[i] + arr[j] === target) return [i, j];
    }
  }
  return [];
}
```

**Time Complexity:** O(n²)

---

### ⚡ 4.2 Optimized Using Hashing

```javascript
function twoSumOptimized(arr, target) {
  const map = new Map();
  for (let i = 0; i < arr.length; i++) {
    const diff = target - arr[i];
    if (map.has(diff)) return [map.get(diff), i];
    map.set(arr[i], i);
  }
  return [];
}
```

**Time Complexity:** O(n)

---

### 🧩 4.3 Divide and Conquer — *Merge Sort*

```javascript
function mergeSort(arr) {
  if (arr.length <= 1) return arr;
  const mid = Math.floor(arr.length / 2);
  const left = mergeSort(arr.slice(0, mid));
  const right = mergeSort(arr.slice(mid));
  return merge(left, right);
}

function merge(left, right) {
  const result = [];
  let i = 0, j = 0;
  while (i < left.length && j < right.length) {
    if (left[i] < right[j]) result.push(left[i++]);
    else result.push(right[j++]);
  }
  return result.concat(left.slice(i)).concat(right.slice(j));
}
```

**Explanation:** Recursively divide and merge sorted halves.

---

### 🪙 4.4 Greedy — *Activity Selection Problem*

```javascript
function activitySelection(activities) {
  activities.sort((a, b) => a[1] - b[1]); // sort by end time
  let lastEnd = activities[0][1];
  const selected = [activities[0]];
  for (let i = 1; i < activities.length; i++) {
    if (activities[i][0] >= lastEnd) {
      selected.push(activities[i]);
      lastEnd = activities[i][1];
    }
  }
  return selected;
}
```

**Explanation:** Always pick the earliest finishing activity compatible with previous ones.

---

### 🔁 4.5 Dynamic Programming — *0/1 Knapsack*

```javascript
function knapsack(weights, values, W) {
  const n = weights.length;
  const dp = Array(n + 1).fill().map(() => Array(W + 1).fill(0));
  for (let i = 1; i <= n; i++) {
    for (let w = 1; w <= W; w++) {
      if (weights[i - 1] <= w)
        dp[i][w] = Math.max(values[i - 1] + dp[i - 1][w - weights[i - 1]], dp[i - 1][w]);
      else dp[i][w] = dp[i - 1][w];
    }
  }
  return dp[n][W];
}
```

**Explanation:** Build up table from smaller subproblems.

---

### ♻️ 4.6 Backtracking — *N-Queens Problem*

```javascript
function solveNQueens(n) {
  const board = Array(n).fill().map(() => Array(n).fill('.'));
  const res = [];

  function isSafe(row, col) {
    for (let i = 0; i < row; i++) {
      if (board[i][col] === 'Q') return false;
      if (col - (row - i) >= 0 && board[i][col - (row - i)] === 'Q') return false;
      if (col + (row - i) < n && board[i][col + (row - i)] === 'Q') return false;
    }
    return true;
  }

  function solve(row) {
    if (row === n) {
      res.push(board.map(r => r.join('')));
      return;
    }
    for (let col = 0; col < n; col++) {
      if (isSafe(row, col)) {
        board[row][col] = 'Q';
        solve(row + 1);
        board[row][col] = '.';
      }
    }
  }

  solve(0);
  return res;
}
```

**Explanation:** Try placing queens row by row, backtrack when invalid.

---

### 🚀 4.7 Two Pointers — *Pair Sum in Sorted Array*

```javascript
function pairSum(arr, target) {
  let left = 0, right = arr.length - 1;
  while (left < right) {
    const sum = arr[left] + arr[right];
    if (sum === target) return [left, right];
    if (sum < target) left++;
    else right--;
  }
  return [];
}
```

**Time Complexity:** O(n)

---

### 🪟 4.8 Sliding Window — *Longest Substring Without Repeating Characters*

```javascript
function lengthOfLongestSubstring(s) {
  const set = new Set();
  let left = 0, maxLen = 0;
  for (let right = 0; right < s.length; right++) {
    while (set.has(s[right])) set.delete(s[left++]);
    set.add(s[right]);
    maxLen = Math.max(maxLen, right - left + 1);
  }
  return maxLen;
}
```

**Explanation:** Expand window until duplicate, then shrink.
**Time Complexity:** O(n)

---

### 🧭 4.9 Binary Search on Answer — *Minimum Capacity to Ship Packages*

```javascript
function shipWithinDays(weights, days) {
  let low = Math.max(...weights), high = weights.reduce((a,b)=>a+b,0);
  while (low < high) {
    const mid = Math.floor((low + high) / 2);
    let d = 1, curr = 0;
    for (const w of weights) {
      if (curr + w > mid) { d++; curr = 0; }
      curr += w;
    }
    if (d > days) low = mid + 1; else high = mid;
  }
  return low;
}
```

**Explanation:** Binary search over possible capacities.
**Time Complexity:** O(n log sum(weights))

---

## 📈 5. Complexity Analysis Recap

| Technique               | Time       | Space    | Use Case                  |
| ----------------------- | ---------- | -------- | ------------------------- |
| Brute Force             | O(n²)      | O(1)     | Small data sets           |
| Divide & Conquer        | O(n log n) | O(log n) | Sorting, Search           |
| Greedy                  | O(n log n) | O(1)     | Optimal immediate choices |
| DP                      | O(n×m)     | O(n×m)   | Overlapping subproblems   |
| Backtracking            | O(kⁿ)      | O(n²)    | Combinatorial problems    |
| Two Pointers            | O(n)       | O(1)     | Sorted arrays             |
| Sliding Window          | O(n)       | O(1)     | Substrings, subarrays     |
| Binary Search on Answer | O(n log n) | O(1)     | Optimization problems     |

---

## 🧠 6. Mastery Tips

* Start with brute force → then **optimize**.
* Practice **pattern recognition** — many problems share core ideas.
* Always analyze **time and space complexity**.
* Learn **recursion and memoization** thoroughly.
* Visualize problems using **diagrams or dry runs**.
* Revisit solved problems for better approaches.

---

**Next Step:** Export this document as **PDF and Markdown (.md)** for offline learning.
