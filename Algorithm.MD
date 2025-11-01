# ⚙️ Algorithm

---

## 🧩 1. What Is an Algorithm?

An **algorithm** is a **step-by-step process** to solve a problem efficiently. It defines a clear sequence of actions to produce a desired output from given inputs.

### ✅ Characteristics:

* **Input & Output:** Takes input, produces output.
* **Definiteness:** Each step must be precisely defined.
* **Finiteness:** Must terminate after finite steps.
* **Effectiveness:** Each step should be executable.

---

## 🧮 2. Types of Algorithms

| Type                         | Description                                      | Example              |
| ---------------------------- | ------------------------------------------------ | -------------------- |
| **Brute Force**              | Try all possibilities                            | Linear Search        |
| **Divide & Conquer**         | Divide, solve, and combine                       | Merge Sort           |
| **Greedy**                   | Take the best current choice                     | Dijkstra’s Algorithm |
| **Dynamic Programming (DP)** | Break into overlapping subproblems               | Fibonacci (DP)       |
| **Backtracking**             | Explore all possibilities but prune invalid ones | N-Queens Problem     |
| **Graph Algorithms**         | Solve problems with nodes and edges              | BFS, DFS             |

---

## 🔍 3. Searching Algorithms

### 3.1 Linear Search

**Concept:** Sequentially check each element.

```javascript
function linearSearch(arr, target) {
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === target) return i;
  }
  return -1;
}
```

**Time Complexity:** O(n)

### 3.2 Binary Search

**Concept:** Efficiently search a **sorted** array by dividing in half each time.

```javascript
function binarySearch(arr, target) {
  let low = 0, high = arr.length - 1;
  while (low <= high) {
    const mid = Math.floor((low + high) / 2);
    if (arr[mid] === target) return mid;
    else if (arr[mid] < target) low = mid + 1;
    else high = mid - 1;
  }
  return -1;
}
```

**Time Complexity:** O(log n)

---

## 🧮 4. Sorting Algorithms

### 4.1 Bubble Sort

**Concept:** Repeatedly swap adjacent elements if they are in the wrong order.

```javascript
function bubbleSort(arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length - i - 1; j++) {
      if (arr[j] > arr[j + 1]) [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
    }
  }
  return arr;
}
```

**Time Complexity:** O(n²)

### 4.2 Merge Sort

**Concept:** Divide array into halves, sort recursively, then merge.

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

**Time Complexity:** O(n log n)

### 4.3 Quick Sort

**Concept:** Choose a pivot, partition the array, and sort partitions recursively.

```javascript
function quickSort(arr) {
  if (arr.length <= 1) return arr;
  const pivot = arr[arr.length - 1];
  const left = arr.filter(x => x < pivot);
  const right = arr.filter(x => x > pivot);
  const equal = arr.filter(x => x === pivot);
  return [...quickSort(left), ...equal, ...quickSort(right)];
}
```

**Time Complexity:** O(n log n) average, O(n²) worst

---

## 💡 5. Divide and Conquer

### Example: **Binary Search (already seen)**

### Example: **Merge Sort (above)**

Another Example: **Maximum Subarray (Kadane’s Algorithm)**

```javascript
function maxSubArray(nums) {
  let maxSum = nums[0];
  let currentSum = nums[0];
  for (let i = 1; i < nums.length; i++) {
    currentSum = Math.max(nums[i], currentSum + nums[i]);
    maxSum = Math.max(maxSum, currentSum);
  }
  return maxSum;
}
```

**Time Complexity:** O(n)

---

## 🪙 6. Greedy Algorithms

### Example: **Activity Selection Problem**

```javascript
function activitySelection(activities) {
  activities.sort((a, b) => a[1] - b[1]); // sort by finish time
  const result = [activities[0]];
  let lastEnd = activities[0][1];
  for (let i = 1; i < activities.length; i++) {
    if (activities[i][0] >= lastEnd) {
      result.push(activities[i]);
      lastEnd = activities[i][1];
    }
  }
  return result;
}
```

**Explanation:** Always pick the next activity with the earliest finish time.
**Time Complexity:** O(n log n)

### Example: **Huffman Coding (Compression)**

*Builds an optimal binary tree for symbol encoding using a min-heap.*

---

## 🧠 7. Dynamic Programming (DP)

### 7.1 Fibonacci with Memoization

```javascript
function fib(n, memo = {}) {
  if (n <= 1) return n;
  if (memo[n]) return memo[n];
  return memo[n] = fib(n - 1, memo) + fib(n - 2, memo);
}
```

**Time Complexity:** O(n)

### 7.2 0/1 Knapsack Problem

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

**Explanation:** Build table for optimal substructure.
**Time Complexity:** O(n × W)

---

## ♻️ 8. Backtracking

### Example: **N-Queens Problem**

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

**Explanation:** Place queens row by row while ensuring no two attack each other.
**Time Complexity:** O(N!)

---

## 🌐 9. Graph Algorithms

### 9.1 Depth-First Search (DFS)

```javascript
function dfs(graph, start, visited = new Set()) {
  console.log(start);
  visited.add(start);
  for (const neighbor of graph[start]) {
    if (!visited.has(neighbor)) dfs(graph, neighbor, visited);
  }
}
```

### 9.2 Breadth-First Search (BFS)

```javascript
function bfs(graph, start) {
  const queue = [start];
  const visited = new Set([start]);
  while (queue.length) {
    const node = queue.shift();
    console.log(node);
    for (const neighbor of graph[node]) {
      if (!visited.has(neighbor)) {
        visited.add(neighbor);
        queue.push(neighbor);
      }
    }
  }
}
```

### 9.3 Dijkstra’s Algorithm (Shortest Path)

```javascript
function dijkstra(graph, start) {
  const dist = {}, visited = new Set();
  for (const node in graph) dist[node] = Infinity;
  dist[start] = 0;
  while (visited.size < Object.keys(graph).length) {
    const [u] = Object.entries(dist).filter(([v]) => !visited.has(v)).sort((a, b) => a[1] - b[1])[0];
    visited.add(u);
    for (const [v, w] of Object.entries(graph[u])) {
      if (!visited.has(v)) {
        const alt = dist[u] + w;
        if (alt < dist[v]) dist[v] = alt;
      }
    }
  }
  return dist;
}
```

**Explanation:** Repeatedly select node with smallest distance. O(V²) (or O(E log V) with heap)

---

## 🧮 10. Time & Space Complexity Summary

| Algorithm     | Best       | Average    | Worst      | Space    |
| ------------- | ---------- | ---------- | ---------- | -------- |
| Linear Search | O(1)       | O(n)       | O(n)       | O(1)     |
| Binary Search | O(1)       | O(log n)   | O(log n)   | O(1)     |
| Bubble Sort   | O(n)       | O(n²)      | O(n²)      | O(1)     |
| Merge Sort    | O(n log n) | O(n log n) | O(n log n) | O(n)     |
| Quick Sort    | O(n log n) | O(n log n) | O(n²)      | O(log n) |
| Dijkstra      | O(V log V) | O(V log V) | O(V²)      | O(V)     |
| Knapsack (DP) | -          | O(n×W)     | O(n×W)     | O(n×W)   |

---

## 🧠 11. Mastery Tips

* Always analyze **time and space complexity**.
* Visualize recursive and iterative approaches.
* Convert recursive to iterative for optimization.
* Master common algorithmic patterns — DP, Greedy, Backtracking.
* Solve variations of classic problems (LeetCode, HackerRank, Codeforces).

---

**Next Step:** Export this document as **PDF and Markdown (.md)** for offline learning.
