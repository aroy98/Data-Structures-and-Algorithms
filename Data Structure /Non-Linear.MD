# 🌳 Non-Linear Data Structure

---

## 🧩 1. What Are Non-Linear Data Structures?

A **Non-Linear Data Structure** is one in which data elements are **not arranged sequentially**. Each element (or node) can be connected to multiple elements, forming **hierarchical or networked relationships**.

### ✅ Characteristics:

* Elements are connected in a **hierarchical or network** manner.
* Traversal may not be sequential (e.g., recursive or breadth-first).
* Provides greater **flexibility** for complex relationships.

---

## 🌲 2. Types of Non-Linear Data Structures

1. **Tree** — Hierarchical structure with parent-child relationships.
2. **Graph** — Collection of nodes connected by edges (can form cycles).
3. **Heap** — Specialized tree used for priority-based access.
4. **Trie** — Tree-like structure for storing strings efficiently.

---

## 🌳 3. Tree Data Structure

### 💡 Concept

A **Tree** is a hierarchical structure made up of **nodes**, where each node has:

* A **value**
* References to its **child nodes**

### 🧱 Terminology

* **Root** — Topmost node
* **Leaf** — Node with no children
* **Parent/Child** — Relationship between nodes
* **Height** — Longest path from root to a leaf

### 💻 Example (Binary Tree in JavaScript)

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.left = null;
    this.right = null;
  }
}

class BinaryTree {
  constructor() { this.root = null; }
  insert(value) {
    const newNode = new Node(value);
    if (!this.root) { this.root = newNode; return; }
    const queue = [this.root];
    while (queue.length) {
      const node = queue.shift();
      if (!node.left) { node.left = newNode; return; }
      else if (!node.right) { node.right = newNode; return; }
      else {
        queue.push(node.left);
        queue.push(node.right);
      }
    }
  }
}
```

### ⚙️ Common Tree Traversals

| Traversal       | Order               | Description          |
| --------------- | ------------------- | -------------------- |
| **Inorder**     | Left → Root → Right | Sorted order for BST |
| **Preorder**    | Root → Left → Right | Used to copy tree    |
| **Postorder**   | Left → Right → Root | Used to delete tree  |
| **Level Order** | Level by Level      | BFS traversal        |

### 💻 Example (DFS Traversal)

```javascript
function inorder(root) {
  if (!root) return;
  inorder(root.left);
  console.log(root.value);
  inorder(root.right);
}
```

### 🧩 Practice Problems — With Solutions & Explanations

#### Problem 1 — Find Height of a Binary Tree

```javascript
function treeHeight(root) {
  if (!root) return 0;
  return 1 + Math.max(treeHeight(root.left), treeHeight(root.right));
}
```

**Explanation:** Recursively compute height of left and right subtrees. O(n) time.

#### Problem 2 — Count Leaf Nodes

```javascript
function countLeaves(root) {
  if (!root) return 0;
  if (!root.left && !root.right) return 1;
  return countLeaves(root.left) + countLeaves(root.right);
}
```

**Explanation:** Leaf nodes have no children. Count recursively.

#### Problem 3 — Check if Tree is Symmetric

```javascript
function isSymmetric(root) {
  if (!root) return true;
  function mirror(a, b) {
    if (!a && !b) return true;
    if (!a || !b || a.value !== b.value) return false;
    return mirror(a.left, b.right) && mirror(a.right, b.left);
  }
  return mirror(root.left, root.right);
}
```

**Explanation:** Compare mirror subtrees recursively.

---

## 🌉 4. Graph Data Structure

### 💡 Concept

A **Graph** consists of **nodes (vertices)** connected by **edges**.

### 🧱 Types of Graphs

* **Directed vs Undirected** — Edges have direction or not.
* **Weighted vs Unweighted** — Edges may have weights.
* **Cyclic vs Acyclic** — May or may not contain cycles.

### 💻 Example (Adjacency List Representation)

```javascript
class Graph {
  constructor() { this.adjList = new Map(); }
  addVertex(v) { if (!this.adjList.has(v)) this.adjList.set(v, []); }
  addEdge(v, w) {
    this.adjList.get(v).push(w);
    this.adjList.get(w).push(v); // For undirected
  }
}
```

### ⚙️ Traversal Techniques

1. **Depth-First Search (DFS)**
2. **Breadth-First Search (BFS)**

### 💻 Example (DFS & BFS)

```javascript
function dfs(graph, start, visited = new Set()) {
  console.log(start);
  visited.add(start);
  for (const neighbor of graph.adjList.get(start)) {
    if (!visited.has(neighbor)) dfs(graph, neighbor, visited);
  }
}

function bfs(graph, start) {
  const visited = new Set([start]);
  const queue = [start];
  while (queue.length) {
    const v = queue.shift();
    console.log(v);
    for (const neighbor of graph.adjList.get(v)) {
      if (!visited.has(neighbor)) {
        visited.add(neighbor);
        queue.push(neighbor);
      }
    }
  }
}
```

### 🧩 Practice Problems — With Solutions & Explanations

#### Problem 1 — Detect Cycle in Undirected Graph

```javascript
function hasCycle(graph) {
  const visited = new Set();
  function dfs(v, parent) {
    visited.add(v);
    for (const neighbor of graph.adjList.get(v)) {
      if (!visited.has(neighbor)) {
        if (dfs(neighbor, v)) return true;
      } else if (neighbor !== parent) return true;
    }
    return false;
  }
  for (const vertex of graph.adjList.keys()) {
    if (!visited.has(vertex) && dfs(vertex, null)) return true;
  }
  return false;
}
```

**Explanation:** DFS traversal checks back edges (indicating a cycle).

#### Problem 2 — Find Shortest Path (BFS)

```javascript
function shortestPath(graph, start, end) {
  const queue = [[start, [start]]];
  const visited = new Set([start]);
  while (queue.length) {
    const [node, path] = queue.shift();
    if (node === end) return path;
    for (const neighbor of graph.adjList.get(node)) {
      if (!visited.has(neighbor)) {
        visited.add(neighbor);
        queue.push([neighbor, [...path, neighbor]]);
      }
    }
  }
  return null;
}
```

**Explanation:** BFS finds the shortest path in an unweighted graph.

---

## 🏗️ 5. Heap Data Structure

### 💡 Concept

A **Heap** is a **complete binary tree** that satisfies the **heap property**:

* **Max-Heap:** Parent >= children
* **Min-Heap:** Parent <= children

### 💻 Example (Min-Heap in JavaScript)

```javascript
class MinHeap {
  constructor() { this.heap = []; }
  getParentIndex(i) { return Math.floor((i - 1) / 2); }
  getLeftIndex(i) { return 2 * i + 1; }
  getRightIndex(i) { return 2 * i + 2; }

  insert(val) {
    this.heap.push(val);
    this.bubbleUp();
  }

  bubbleUp() {
    let i = this.heap.length - 1;
    while (i > 0 && this.heap[i] < this.heap[this.getParentIndex(i)]) {
      [this.heap[i], this.heap[this.getParentIndex(i)]] = [this.heap[this.getParentIndex(i)], this.heap[i]];
      i = this.getParentIndex(i);
    }
  }

  extractMin() {
    if (this.heap.length === 0) return null;
    const min = this.heap[0];
    const end = this.heap.pop();
    if (this.heap.length > 0) {
      this.heap[0] = end;
      this.sinkDown(0);
    }
    return min;
  }

  sinkDown(i) {
    const left = this.getLeftIndex(i);
    const right = this.getRightIndex(i);
    let smallest = i;
    if (left < this.heap.length && this.heap[left] < this.heap[smallest]) smallest = left;
    if (right < this.heap.length && this.heap[right] < this.heap[smallest]) smallest = right;
    if (smallest !== i) {
      [this.heap[i], this.heap[smallest]] = [this.heap[smallest], this.heap[i]];
      this.sinkDown(smallest);
    }
  }
}
```

### ⚙️ Time Complexities

| Operation       | Time     |
| --------------- | -------- |
| Insert          | O(log n) |
| Extract Min/Max | O(log n) |
| Peek            | O(1)     |

---

## 🔠 6. Trie Data Structure

### 💡 Concept

A **Trie (Prefix Tree)** is a tree-like structure used for efficient string lookup.

Each node represents a **character**, and paths from the root represent words.

### 💻 Example (Trie Implementation)

```javascript
class TrieNode {
  constructor() { this.children = {}; this.isEnd = false; }
}

class Trie {
  constructor() { this.root = new TrieNode(); }

  insert(word) {
    let node = this.root;
    for (const ch of word) {
      if (!node.children[ch]) node.children[ch] = new TrieNode();
      node = node.children[ch];
    }
    node.isEnd = true;
  }

  search(word) {
    let node = this.root;
    for (const ch of word) {
      if (!node.children[ch]) return false;
      node = node.children[ch];
    }
    return node.isEnd;
  }

  startsWith(prefix) {
    let node = this.root;
    for (const ch of prefix) {
      if (!node.children[ch]) return false;
      node = node.children[ch];
    }
    return true;
  }
}
```

### 🧩 Practice Problem — Auto-Complete Feature

```javascript
function autoComplete(trie, prefix) {
  let node = trie.root;
  for (const ch of prefix) {
    if (!node.children[ch]) return [];
    node = node.children[ch];
  }
  const results = [];
  function dfs(current, path) {
    if (current.isEnd) results.push(prefix + path);
    for (const [ch, next] of Object.entries(current.children)) dfs(next, path + ch);
  }
  dfs(node, '');
  return results;
}
```

**Explanation:** DFS from prefix node to collect all possible completions.

---

## 🧮 7. Comparison Summary

| Structure | Hierarchy            | Key Operations          | Example Use    |
| --------- | -------------------- | ----------------------- | -------------- |
| **Tree**  | Parent-child         | Traversals, insertion   | File system    |
| **Graph** | Network              | DFS, BFS, pathfinding   | Social network |
| **Heap**  | Complete tree        | Insert, extract min/max | Priority queue |
| **Trie**  | Character-based tree | Insert, search          | Auto-complete  |

---

## 🧠 8. Mastery Tips

* Visualize tree and graph structures while coding.
* Practice recursive traversals until natural.
* Master DFS/BFS — they apply to almost all non-linear structures.
* Implement priority queues using heaps for real-world scenarios.
* Use tries for autocomplete, spell-checkers, and word searches.

---

**Next Step:** Export this document as **PDF and Markdown (MD)** for offline learning.
