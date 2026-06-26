
## Intuition

**"The Manager's Report"**
- **Concept:** You are a manager (Node) who cannot complete your report until your subordinates (Children) file theirs.
- **Direction:** Information flows **Child $\to$ Parent**.
- **Execution Order:** Post-order (Left $\to$ Right $\to$ Root).
- **Contrast:** Unlike Top-Down (which passes data down), Bottom-Up computes values at the leaves and bubbles them up.

## Core Templates

### Template A: Pure Aggregation

**Use when:** Calculating Height, Sum of Nodes, Count of Nodes.
- **Key:** The return value is the answer for that subtree.

```cpp
int maxDepth(TreeNode* root) {
    // 1. Base Case: Null contributes 0
    if (!root) return 0;
    
    // 2. Ask Children (Wait for reports)
    int leftDepth = maxDepth(root->left);
    int rightDepth = maxDepth(root->right);
    
    // 3. Aggregate (Process reports + Self)
    return 1 + max(leftDepth, rightDepth);
}
```

### Template B: The "Hybrid" (Global Variable)

**Use when:** The answer might not pass through the root (e.g., Diameter, Max Path Sum).

- **Key:** Return a "Helper Value" (like height) to the parent to keep the recursion going, but update a `Global Variable` with the actual answer.

```cpp
class Solution {
    int globalMax = INT_MIN; // The actual answer

    int dfs(TreeNode* root) {
        if (!root) return 0; // Base case for Helper

        // 1. Get Helper Values from children
        int left = max(0, dfs(root->left));   // Handle negatives if needed
        int right = max(0, dfs(root->right));

        // 2. Update Global Answer (The "bridge" logic)
        // Example: Diameter = Left Height + Right Height
        globalMax = max(globalMax, left + right + root->val);

        // 3. Return Helper Value to Parent (Extend the path)
        return root->val + max(left, right);
    }
    
	public:
	    int maxPathSum(TreeNode* root) {
	        dfs(root);
	        return globalMax;
	    }
};
```

## Pattern Recognition

### Pattern: Tree Height / Depth

- **Trigger:** "Find maximum depth", "Find minimum depth".

- **Action:** Use **Template A**. Return `1 + max(l, r)` or `1 + min(l, r)`.

### Pattern: Balanced Binary Tree

- **Trigger:** "Check if height of subtrees differs by no more than 1".

- **Action:** Use **Template A**. If `abs(left - right) > 1`, return -1 (error code) to bubble up the failure.

### Pattern: Path "Through" Node

- **Trigger:** "Diameter of Tree" (Longest path between _any_ two nodes), "Max Path Sum".

- **Action:** Use **Template B**. The path curves at the current node (`left + right`), but the parent can only use one branch (`max(left, right)`).

## Pitfalls

- **Negative Values:** In Max Path Sum, if a child returns a negative path, ignore it (`max(0, val)`). Including it would only decrease your total.

- **Global Reset:** If solving on LeetCode with a global variable, remember to reset it or use a member variable, otherwise previous test cases will interfere.

- **Wrong Return:** Confusing what to _return_ (the single path extending up) vs what to _update_ (the bridged path inside the subtree).

## LeetCode Practice Set
### Easy

- [ ] **104** - Maximum Depth of Binary Tree `[Template A]`
- [ ] **110** - Balanced Binary Tree `[Template A + Error Code]`
- [ ] **543** - Diameter of Binary Tree `[Template B]`
    - _Note:_ Return height, Update `left + right`.

### Medium

- [ ] **687** - Longest Univalue Path `[Template B]`
- [ ] **337** - House Robber III `[DP on Trees]`
    - _Hint:_ Return pair `{money_with_root, money_without_root}`.

### Hard
- [ ] **124** - Binary Tree Maximum Path Sum `[Template B + Negatives]`
- [ ] **968** - Binary Tree Cameras `[State Logic]`
    - _Hint:_ Return state: 0=NoCam, 1=HasCam, 2=Covered.