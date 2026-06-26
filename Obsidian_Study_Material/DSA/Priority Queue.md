### Concept Overview

A **Priority Queue** is a queue where elements are served based on their **priority**, not insertion order.

- **Intuition:** Think of an emergency room. Patients are treated based on severity, not who arrived first.
- **Implementation:** Under the hood, it is usually a **Binary Heap** (a complete binary tree).

- **Key Operations:**
    - **Push:** Insert element ($O(\log n)$).
    - **Pop:** Remove top priority element ($O(\log n)$).
    - **Top:** Peek at top priority element ($O(1)$).

- **Types:**
    - **Max-Heap:** The largest element is always on top (C++ default).
    - **Min-Heap:** The smallest element is always on top.

