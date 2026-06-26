**Lowest Common Ancestor (LCA)** is one of the most famous tree problems. It tests your ability to reason about the relationship between nodes without traversing the entire tree unnecessarily.

## [[1. Standard LCA (Binary Tree)]]

**Problem:** Find LCA of nodes `p` and `q`.

**Pattern:** Post-order DFS

**Logic:**
- If `root == p || root == q` → return root
- Recurse left & right
- If both return non-null → current node is LCA
- Else return non-null child

**Return Type:** `TreeNode*`

---

## [[2. LCA in a Binary Search Tree (BST)]]

**Problem:** Same as standard LCA but tree is a BST.

**Pattern:** Use ordering (no DFS)

**Logic:**
- If `p.val < root.val && q.val < root.val` → go left
- If `p.val > root.val && q.val > root.val` → go right
- Else → root is LCA

**Time:** `O(h)`  
**Space:** `O(1)`

---

## [[3. LCA of Deepest Leaves (LC 865, 1123)]]

**Problem:** Find LCA of all deepest nodes.

**Pattern:** Return `{depth, node}`

**Logic:**
- Get `{depth, node}` from left & right
- If `left.depth == right.depth` → current node is LCA
- If `left.depth > right.depth` → propagate left
- Else → propagate right

**Return Type:** `pair<int, TreeNode*>`

---

## 4. Nodes Might Not Exist (LC 1644)

**Problem:** Find LCA of `p` and `q`, but one or both may be missing.

**Pitfall:** Standard LCA returns `p` even if `q` doesn’t exist.

**Fix Pattern:** Full traversal + validation

**Logic:**
- Traverse entire tree (no early return)
- Count how many of `p` and `q` are found
- Only return LCA if count == 2

**Return Type:** `TreeNode* + count`

---

## 5. LCA with Parent Pointers (LC 1650)

**Problem:** Nodes have `parent` pointer.

**Pattern:** Intersection of two linked lists

**Logic:**
- Path from `p → root` = List A
- Path from `q → root` = List B
- Use `A + B` switching trick
- First meeting point is LCA

**Time:** `O(h)`  
**Space:** `O(1)`

---

## 6. Distance Between Two Nodes

**Problem:** Find number of edges between `p` and `q`.

**Formula:**
dist(p, q) = depth(p) + depth(q) - 2 * depth(LCA)

yaml
Copy code

**Steps:**
1. Find LCA
2. Find depth of `p` and `q`
3. Apply formula

---

## 7. LCA of Multiple Nodes (Set of K Nodes)

**Problem:** Find LCA of more than two nodes.

**Pattern:** Generalized LCA

**Logic:**
- Each DFS returns `{count, node}`
- If left.count + right.count + selfMatch == K → current is LCA
- Else propagate upward

**Return Type:** `{count, TreeNode*}`

---

## Master Pattern (Unifying Insight)

| Variation | Return Information |
|--------|-------------------|
| Standard LCA | `TreeNode*` |
| Deepest Leaves | `{depth, node}` |
| Missing Nodes | `{node, foundCount}` |
| Multiple Nodes | `{count, node}` |
| Distance | `{depth}` + LCA |

> **The problem changes what you return — not the traversal.**

---

## Interview Golden Line

> “LCA problems are solved by post-order DFS where each call returns enough information to decide whether the answer lies below or at the current node.”
