# 🧭 Linear Data Structure Mastery

---

## 🧩 1. What Are Linear Data Structures?

A **Linear Data Structure** is one in which data elements are arranged **in a sequence**, where each element is connected to its **previous and next** element.

### ✅ Characteristics:

* Elements are stored sequentially
* Traversal happens one element at a time
* Easy implementation but limited flexibility

---

## 🌿 Types of Linear Data Structures

1. **Array**
2. **Linked List**
3. **Stack**
4. **Queue**

---

## 📘 2. Arrays

### 💡 Concept

An **Array** is a fixed-size collection of elements stored in contiguous memory locations.
It allows random access using **indexing**.

### 💻 Example (JavaScript)

```javascript
let arr = [10, 20, 30, 40];

// Access
console.log(arr[2]); // 30

// Insert at end
arr.push(50);

// Delete last element
arr.pop();

console.log(arr); // [10, 20, 30, 40]
```

### ⚙️ Operations & Complexities

| Operation          | Description             | Time Complexity  |
| ------------------ | ----------------------- | ---------------- |
| Access             | arr[i]                  | O(1)             |
| Insertion (end)    | arr.push()              | O(1)             |
| Insertion (middle) | splice(index, 0, value) | O(n)             |
| Deletion (end)     | arr.pop()               | O(1)             |
| Search             | Linear or Binary Search | O(n) or O(log n) |

### 🧩 Practice Problems — With Solutions & Explanations

#### Problem 1 — Reverse an array

**Prompt:** Reverse an array in-place.

**Solution (JS):**

```javascript
function reverseArray(arr) {
  let i = 0, j = arr.length - 1;
  while (i < j) {
    const tmp = arr[i];
    arr[i] = arr[j];
    arr[j] = tmp;
    i++; j--;
  }
  return arr;
}
// Example
console.log(reverseArray([1,2,3,4])); // [4,3,2,1]
```

**Explanation:** Use two-pointer technique. Swap outer elements and move inward. In-place O(1) extra space, O(n) time.

---

#### Problem 2 — Find max & min element

**Prompt:** Return both maximum and minimum values from an array.

**Solution (JS):**

```javascript
function minMax(arr) {
  if (!arr.length) return null;
  let min = arr[0], max = arr[0];
  for (let i = 1; i < arr.length; i++) {
    if (arr[i] < min) min = arr[i];
    if (arr[i] > max) max = arr[i];
  }
  return {min, max};
}
```

**Explanation:** Single pass linear scan, O(n) time, O(1) space. Avoids sorting which would be O(n log n).

---

#### Problem 3 — Remove duplicates (preserve order)

**Prompt:** Given an array, return a new array with duplicates removed (first occurrence kept).

**Solution (JS):**

```javascript
function removeDuplicates(arr) {
  const seen = new Set();
  const res = [];
  for (const x of arr) {
    if (!seen.has(x)) {
      seen.add(x);
      res.push(x);
    }
  }
  return res;
}
// Example
console.log(removeDuplicates([1,2,1,3,2])); // [1,2,3]
```

**Explanation:** Use a hash set to track seen values for O(1) membership test. O(n) time, O(n) extra space.

---

#### Problem 4 — Rotate array by k positions (to the right)

**Prompt:** Rotate the array to the right by k steps.

**Solution (JS, in-place):**

```javascript
function rotate(arr, k) {
  const n = arr.length;
  k = k % n;
  function reverse(a, i, j) {
    while (i < j) {
      [a[i], a[j]] = [a[j], a[i]];
      i++; j--;
    }
  }
  reverse(arr, 0, n-1);
  reverse(arr, 0, k-1);
  reverse(arr, k, n-1);
}
// Example
const a = [1,2,3,4,5]; rotate(a, 2); console.log(a); // [4,5,1,2,3]
```

**Explanation:** Use triple-reverse trick. Time O(n), space O(1). Avoids creating a copy.

---

#### Problem 5 — Find second largest element

**Prompt:** Return the second largest distinct element.

**Solution (JS):**

```javascript
function secondLargest(arr) {
  let max = -Infinity, second = -Infinity;
  for (const x of arr) {
    if (x > max) { second = max; max = x; }
    else if (x > second && x < max) { second = x; }
  }
  return (second === -Infinity) ? null : second;
}
```

**Explanation:** Single pass tracking top two distinct values. Time O(n), space O(1).

---

## 📘 3. Linked List

### 💡 Concept

A **Linked List** is a collection of nodes, where each node contains:

* **Data**
* **Pointer (Reference)** to the next node

### 🧱 Types

* **Singly Linked List** → Each node points to the next node.
* **Doubly Linked List** → Each node points to both next and previous nodes.
* **Circular Linked List** → Last node points back to the first node.

### 💻 Example (Singly Linked List)

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedList {
  constructor() { this.head = null; }
  append(value) {
    const node = new Node(value);
    if (!this.head) { this.head = node; return; }
    let cur = this.head;
    while (cur.next) cur = cur.next;
    cur.next = node;
  }
}
```

### ⚙️ Operations & Complexities

| Operation        | Description     | Time Complexity |
| ---------------- | --------------- | --------------- |
| Traversal        | Visit each node | O(n)            |
| Insertion (head) | Add at start    | O(1)            |
| Insertion (end)  | Add at end      | O(n)            |
| Deletion         | Remove node     | O(n)            |
| Search           | Find node       | O(n)            |

### 🧩 Practice Problems — With Solutions & Explanations

#### Problem 1 — Find the middle of a linked list

**Prompt:** Return the middle node (if even length, return the second middle).

**Solution (JS):**

```javascript
function middleNode(head) {
  let slow = head, fast = head;
  while (fast && fast.next) {
    slow = slow.next;
    fast = fast.next.next;
  }
  return slow; // slow is middle
}
```

**Explanation:** Two-pointer (tortoise-hare). Fast moves 2x, slow moves 1x; when fast reaches end, slow is middle. O(n) time, O(1) space.

---

#### Problem 2 — Reverse a linked list

**Prompt:** Reverse a singly linked list and return new head.

**Solution (JS):**

```javascript
function reverseList(head) {
  let prev = null, curr = head;
  while (curr) {
    const next = curr.next;
    curr.next = prev;
    prev = curr;
    curr = next;
  }
  return prev;
}
```

**Explanation:** Iteratively reverse pointers. O(n) time, O(1) space. Easy to extend recursively but recursion uses O(n) call stack.

---

#### Problem 3 — Detect loop in a linked list

**Prompt:** Return true if there is a cycle.

**Solution (JS):**

```javascript
function hasCycle(head) {
  let slow = head, fast = head;
  while (fast && fast.next) {
    slow = slow.next;
    fast = fast.next.next;
    if (slow === fast) return true;
  }
  return false;
}
```

**Explanation:** Floyd's cycle-finding algorithm. If pointers meet, a cycle exists. O(n) time, O(1) space.

---

#### Problem 4 — Merge two sorted linked lists

**Prompt:** Given two sorted lists, merge into one sorted list.

**Solution (JS):**

```javascript
function mergeLists(l1, l2) {
  const dummy = {next: null};
  let tail = dummy;
  while (l1 && l2) {
    if (l1.value < l2.value) { tail.next = l1; l1 = l1.next; }
    else { tail.next = l2; l2 = l2.next; }
    tail = tail.next;
  }
  tail.next = l1 || l2;
  return dummy.next;
}
```

**Explanation:** Classic merge routine (like merge in merge-sort). O(n+m) time, O(1) extra space.

---

## 📘 4. Stack

### 💡 Concept

A **Stack** follows **LIFO (Last In, First Out)** principle.

### 💻 Example (JavaScript)

```javascript
let stack = [];
stack.push(10);
stack.push(20);
stack.pop();
```

### ⚙️ Operations & Complexities

| Operation | Description        | Time Complexity |
| --------- | ------------------ | --------------- |
| Push      | Add element        | O(1)            |
| Pop       | Remove top element | O(1)            |
| Peek      | Access top element | O(1)            |

### 🧩 Practice Problems — With Solutions & Explanations

#### Problem 1 — Check for balanced parentheses

**Prompt:** Given a string with brackets `()[]{}`, return true if balanced.

**Solution (JS):**

```javascript
function isBalanced(s) {
  const stack = [];
  const pairs = {')':'(', ']':'[', '}':'{'};
  for (const ch of s) {
    if (ch === '(' || ch === '[' || ch === '{') stack.push(ch);
    else {
      if (!stack.length || stack.pop() !== pairs[ch]) return false;
    }
  }
  return stack.length === 0;
}
```

**Explanation:** Push opening brackets; on closing bracket check top. O(n) time, O(n) space worst-case.

---

#### Problem 2 — Implement stack using a queue

**Prompt:** Emulate a stack (LIFO) using a single queue.

**Solution (JS):**

```javascript
class StackWithQueue {
  constructor() { this.q = []; }
  push(x) {
    this.q.push(x);
    // rotate to make pushed element at front
    for (let i = 0; i < this.q.length - 1; i++) this.q.push(this.q.shift());
  }
  pop() { return this.q.shift(); }
  top() { return this.q[0]; }
  isEmpty() { return this.q.length === 0; }
}
```

**Explanation:** After pushing, rotate queue so new element becomes front — then pop is O(1). Push becomes O(n).

---

#### Problem 3 — Evaluate postfix expression

**Prompt:** Given tokens of a postfix expression, evaluate result.

**Solution (JS):**

```javascript
function evalPostfix(tokens) {
  const stack = [];
  for (const t of tokens) {
    if (!['+','-','*','/'].includes(t)) stack.push(Number(t));
    else {
      const b = stack.pop();
      const a = stack.pop();
      let res;
      if (t === '+') res = a + b;
      if (t === '-') res = a - b;
      if (t === '*') res = a * b;
      if (t === '/') res = Math.trunc(a / b);
      stack.push(res);
    }
  }
  return stack.pop();
}
```

**Explanation:** Push numbers; when operator encountered pop two operands, compute, push result. O(n) time.

---

#### Problem 4 — Next greater element (to the right)

**Prompt:** For each element, find the next greater element to its right or -1.

**Solution (JS):**

```javascript
function nextGreater(arr) {
  const res = new Array(arr.length).fill(-1);
  const stack = []; // store indices
  for (let i = 0; i < arr.length; i++) {
    while (stack.length && arr[i] > arr[stack[stack.length-1]]) {
      const idx = stack.pop();
      res[idx] = arr[i];
    }
    stack.push(i);
  }
  return res;
}
```

**Explanation:** Use monotonic stack of indices. Each element pushed/popped once -> O(n) time.

---

## 📘 5. Queue

### 💡 Concept

A **Queue** follows **FIFO (First In, First Out)** principle.

### 💻 Example (JavaScript)

```javascript
let queue = [];
queue.push(1);
queue.push(2);
queue.shift();
```

### ⚙️ Operations & Complexities

| Operation | Description               | Time Complexity |
| --------- | ------------------------- | --------------- |
| Enqueue   | Add element to end        | O(1)            |
| Dequeue   | Remove element from front | O(1)            |
| Peek      | View front element        | O(1)            |

### 🧩 Practice Problems — With Solutions & Explanations

#### Problem 1 — Implement circular queue

**Prompt:** Design a circular queue supporting enqueue/dequeue with fixed capacity.

**Solution (JS):**

```javascript
class CircularQueue {
  constructor(k) { this.q = new Array(k); this.head = 0; this.count = 0; this.k = k; }
  enqueue(val) {
    if (this.count === this.k) return false;
    const tail = (this.head + this.count) % this.k;
    this.q[tail] = val;
    this.count++;
    return true;
  }
  dequeue() {
    if (this.count === 0) return null;
    const val = this.q[this.head];
    this.head = (this.head + 1) % this.k;
    this.count--;
    return val;
  }
  front() { return this.count===0?null:this.q[this.head]; }
  isEmpty() { return this.count===0; }
}
```

**Explanation:** Use circular indexing to reuse array slots. O(1) operations.

---

#### Problem 2 — Generate binary numbers using queue

**Prompt:** Given n, generate binary numbers from 1 to n as strings.

**Solution (JS):**

```javascript
function generateBinary(n) {
  const res = [];
  const q = ['1'];
  while (res.length < n) {
    const s = q.shift();
    res.push(s);
    q.push(s + '0');
    q.push(s + '1');
  }
  return res;
}
```

**Explanation:** BFS on an implicit tree of binary strings. Each string produces two children. O(n) time (lengths sum to O(n)).

---

#### Problem 3 — Reverse the first K elements of queue

**Prompt:** Given a queue, reverse the first k elements keeping order of rest.

**Solution (JS):**

```javascript
function reverseFirstK(q, k) {
  const stack = [];
  for (let i = 0; i < k; i++) stack.push(q.shift());
  while (stack.length) q.push(stack.pop());
  for (let i = 0; i < q.length - k; i++) q.push(q.shift());
}
```

**Explanation:** Use stack to reverse first k, then rotate remaining elements to restore order. O(n) time.

---

#### Problem 4 — Implement queue using two stacks

**Prompt:** Implement FIFO queue using two LIFO stacks.

**Solution (JS):**

```javascript
class QueueWithStacks {
  constructor(){ this.s1 = []; this.s2 = []; }
  enqueue(x){ this.s1.push(x); }
  dequeue(){
    if (!this.s2.length) while (this.s1.length) this.s2.push(this.s1.pop());
    return this.s2.pop() || null;
  }
}
```

**Explanation:** s1 used for enqueue, s2 for dequeue. Amortized O(1) per operation.

---

## 🧮 6. Comparison Summary

| Structure       | Access | Insert | Delete | Order      | Example         |
| --------------- | ------ | ------ | ------ | ---------- | --------------- |
| **Array**       | O(1)   | O(n)   | O(n)   | Sequential | Playlist        |
| **Linked List** | O(n)   | O(1)   | O(1)   | Sequential | Browser history |
| **Stack**       | O(1)   | O(1)   | O(1)   | LIFO       | Undo/Redo       |
| **Queue**       | O(1)   | O(1)   | O(1)   | FIFO       | Task scheduling |

---

## 🧠 7. Mastery Tips

* Visualize memory layout for arrays vs. linked lists.
* Practice pointer manipulation for linked lists until it feels natural.
* Use stacks & queues to transform problems (e.g., DFS, BFS, monotonic stacks).
* Time yourself solving problems and then refactor for cleaner code.

---

## 🎯 8. Next Steps

Would you like:

* A **PDF and MD** download prepared now? (I can export the current document into files you can download.)
* A **non-linear data structures** document next (trees, graphs, heaps, tries) with the same problem+solution style?

---

*Document updated: Linear Data Structure Mastery — now includes worked solutions with explanations for all practice problems.*
