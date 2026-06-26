### 1. Intuition
Traversing a tree means visiting **every node exactly once** to perform an operation (print, sum, modify). unlike linear arrays ($O(1)$ next element), trees require making a choice at every node: "Do I process myself, my left child, or my right child first?"

### The Two Main Strategies
1.  **Depth First Search (DFS):** Dive as deep as possible into one branch before backtracking. 
    - *Analogy:* A maze runner sticking to the left wall until they hit a dead end.
    - *Implementation:* Uses a **Stack** (implicit recursion stack or explicit `std::stack`).

2.  **Breadth First Search (BFS):** Explore neighbor by neighbor, layer by layer.
    - *Analogy:* A ripple in a pond expanding outwards.
    - *Implementation:* Uses a **Queue** (`std::queue`).

---

## 2. Complexity Analysis

### Time Complexity
**$O(n)$** for ALL traversals.
- **Reason:** We visit every node exactly once. Constant work $c$ is done per node. Total time = $c \times n$.

### Space Complexity (Auxiliary)
This is where they differ.

| Traversal Type        | Space Complexity         | Explanation                                                    |
| :-------------------- | :----------------------- | :------------------------------------------------------------- |
| **DFS (Recursive)**   | $O(h)$                   | $h$ is tree height. Stack frames build up to the deepest leaf. |
|                       | *Best Case:* $O(\log n)$ | Balanced Tree (Perfect/Complete).                              |
|                       | *Worst Case:* $O(n)$     | Skewed Tree (Line).                                            |
| **DFS (Iterative)**   | $O(h)$                   | Explicit `stack` stores path to current node.                  |
| **BFS (Level Order)** | $O(w)$                   | $w$ is max width. Queue stores the widest level.               |
|                       | *Worst Case:* $O(n)$     | Perfect Tree (Last level has $n/2$ nodes).                     |
| **Morris**            | $O(1)$                   | Modifies pointers temporarily (Threaded Binary Tree).          |

---

## 3. Core Algorithms 

### 3.1 Recursive DFS (The Standard)
Use these for 95% of problems.

```cpp
// 1. Preorder (Root -> Left -> Right)
// Best for: Cloning, Serialization, Prefix expressions
void preorder(TreeNode* root) {
    if (!root) return;
    visit(root);             // Process Node
    preorder(root->left);    // Recurse Left
    preorder(root->right);   // Recurse Right
}

// 2. Inorder (Left -> Root -> Right)
// Best for: BST (Result is Sorted), Infix expressions
void inorder(TreeNode* root) {
    if (!root) return;
    inorder(root->left);     // Recurse Left
    visit(root);             // Process Node
    inorder(root->right);    // Recurse Right
}

// 3. Postorder (Left -> Right -> Root)
// Best for: Deletion (free children first), Bottom-up calculations (Height/Diameter)
void postorder(TreeNode* root) {
    if (!root) return;
    postorder(root->left);   // Recurse Left
    postorder(root->right);  // Recurse Right
    visit(root);             // Process Node
}
```

![[Pasted image 20260108121028.png]]

### 3.2 Iterative DFS 
Use these if the interviewer forbids recursion or asks to avoid Stack Overflow.

#### Iterative Pre-order
```cpp
vector<int> preorderIterative(TreeNode* root) {
	if(!root) return {};
	
	vector<int> result;
	stack<TreeNode*> st;
	st.push(root);
	
	while(!st.empty) {
		TreeNode* node = st.top();
		st.pop();
		result.push_back(node->val);
		
		if(node->right) st.push(node->right);
		if(node->left) st.push(node->left);
	}
	
	return result;
}
```


#### Iterative In-order

![[Pasted image 20260108123024.png]]
![[Pasted image 20260108124423.png]]


```cpp
vector<int> inorderIterative(TreeNode* root) {
	if(!root) return {};
	
	vector<int> result;
	stack<TreeNode* root> st;
	TreeNode* curr = root;
	
	while(curr != nullptr || !st.empty()) {
		while(curr != nullptr) {
			st.push(curr);
			curr =  curr -> left;
		}
		
		// When curr becomes nullptr, redefine the curr with tthe st.top()
		curr = st.top(); st.pop();
		result.push_back(curr->val);
		
		curr = curr -> right;
	}
	
	return result;
}
```

### Level Order Traversal

We have to use `queue`, for achieve level wise traversal

```cpp
vector<vector<int>> levelTraversal(TreeNode* root) {
	if(!root) return {};
	
	vector<vector<int>> result;
	queue<TreeNode*> q;
	q.push(root);
	
	while(!q.empty()) {
		int size = q.size();
		vector<int> currLevel;
		for(int i=0; i<size; i++) {
			TreeNode* node = q.front(); q.pop();
			currLevel.push_back(node->val);
			
			if(node->left) q.push(node->left);
			if(node->right) q.push(node->right);
		}
		result.push_back(currLevel);
	}
	return result;
}
```
