## 1. What is it?
- A binary tree representation of an array.
- Each node represents an interval `[L, R]`.
    - **Leaf:** `[i, i]` (Single element).
    - **Internal Node:** Union of left child `[L, M]` and right child `[M+1, R]`.

## 2. Why do we need it?
To handle **Dynamic Range Queries**.
- **Static Arrays:** Prefix Sums are best ($O(1)$ query).
- **Dynamic Arrays:** Prefix Sums fail ($O(N)$ update). Segment Trees offer $O(\log N)$ for both.

## 3. Comparison Table

| Feature | Prefix Sum | Segment Tree | Fenwick Tree (BIT) |
| :--- | :--- | :--- | :--- |
| **Space** | $O(N)$ | $O(4N)$ | $O(N)$ |
| **Build** | $O(N)$ | $O(N)$ | $O(N \log N)$ or $O(N)$ |
| **Query** | $O(1)$ | $O(\log N)$ | $O(\log N)$ |
| **Update** | $O(N)$ | $O(\log N)$ | $O(\log N)$ |
| **Ops** | Sum/XOR | **Any Associative** (Sum, Min, Max, GCD) | Sum/XOR (Invertible only) |

## 4. When to use?
1.  **Range Queries** (Sum, Min, Max).
2.  **Point Updates** (Change value at index `i`).
3.  **Constraints:** $N, Q \le 10^5$.