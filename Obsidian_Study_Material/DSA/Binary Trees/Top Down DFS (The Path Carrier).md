
**"The Explorer's Backpack"**
- **Concept:** You are traveling from Root to Leaf. You carry a "backpack" (variables) containing the history of the path so far.
- **Direction:** Information flows **Parent $\to$ Child**.
- **Decision Point:** The logic usually executes at the **Leaf** ("Does my backpack content match the target?").
- **Contrast:** Unlike Bottom-Up (which waits for children), Top-Down passes data *before* recursing.

### Core Templates

#### Template A: Primitives (Fire & Forget)

**Use when:** Calculating Sums, Counts, or Boolean existence.

- **Key:** Pass variables by **value**.
- **Benefit:** No backtracking needed. Each recursive call gets its own copy of the state.

```cpp
bool hasPathSum(TreeNode* root, int currentSum, int targetSum) {
    if (!root) return false;

    // 1. Update State (Add to backpack)
    currentSum += root->val;

    // 2. Base Case: Leaf Check
    if (!root->left && !root->right) {
        return currentSum == targetSum;
    }

    // 3. Propagate (Pass new state down)
    return hasPathSum(root->left, currentSum, targetSum) || 
           hasPathSum(root->right, currentSum, targetSum);
}
```

#### Template B: Structures (Backtracking)

**Use when:** Printing paths, Collecting nodes, Valid parenthesis generation.

- **Key:** Pass large structures (`vector`, `string`) by **reference** (`&`).
- **Constraint:** You **must backtrack** (`pop_back`) to clean up the shared state before returning to the parent.

```cpp
void findPaths(TreeNode* node, int target, vector<int>& path, vector<vector<int>>& res) {
    if (!node) return;

    // 1. Choose: Add to current path
    path.push_back(node->val);
    target -= node->val;

    // 2. Explore: Check Leaf
    if (!node->left && !node->right && target == 0) {
        res.push_back(path); // Found valid path
    } else {
        // Recurse
        findPaths(node->left, target, path, res);
        findPaths(node->right, target, path, res);
    }

    // 3. Un-Choose: Backtrack
    path.pop_back(); 
}
```

### Pattern Recognition

#### Pattern: Root-to-Leaf Property

- **Trigger:** "Find a path equal to sum...", "Return all paths where...", "Form a number from root to leaf".

- **Action:** Use **Template A**. Accumulate the value as you go down.
#### Pattern: Path Construction

- **Trigger:** "Return a list of all paths", "Print the path".

- **Action:** Use **Template B**. Maintain a `vector<int>` path.

#### Pattern: Valid Sequence (String)

- **Trigger:** "Check if the tree contains the sequence..."

- **Action:** Pass an index `i` down. `if (node->val != seq[i]) return false`. Recurse with `i+1`.

### Pitfalls

- **Double Counting:** Be careful not to count a leaf twice (once for left null, once for right null). Check `!left && !right` explicitly.

- **Reference Bugs:** Forgetting `&` in Template B causes $O(N^2)$ copying time.

- **Backtrack Bugs:** Forgetting `pop_back()` in Template B leaves "garbage" from the left subtree when you visit the right subtree.

### LeetCode Practice Set

#### Easy
- [ ] **112** - Path Sum `[Template A]`
- [ ] **257** - Binary Tree Paths `[String Building]`

#### Medium
- [ ] **113** - Path Sum II `[Template B]`
- [ ] **129** - Sum Root to Leaf Numbers `[Math Accumulation]`
- [ ] **1448** - Count Good Nodes in Binary Tree `[Max So Far]`
    - _Hint:_ Pass `maxVal` seen so far down the tree. `if (node->val >= maxVal) count++`.


#### Hard
- [ ] **988** - Smallest String Starting From Leaf `[Lexicographical Comparison]`