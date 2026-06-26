### Structural Problems : 
**Core Pattern:** **Bottom-Up DFS**. 
**Intuition:** "I cannot know my own property (Depth, Count, Symmetry) until I measure my children."

- Maximum depth
```cpp
int maxDepth(TreeNode* root) {
	if(!root) return 0;
	
	int leftDepth = maxDepth(root->left);
	int rightDepth = maxDepth(root->right);
	
	return 1 + max(leftDepth, rightDepth);
}
```

- Minimum depth
![[Pasted image 20260110114110.png]]

```cpp
int minDepth(TreeNode* root) {
	if(!root) return 0;
	
	if(!root->left) return 1 + minDepth(root->right);
	if(!root->right) return 1 + minDepth(root->left);
	
	return 1 + min(minDepth(root->left), minDepth(root->right));
}
```


Queue method : Checking for first Leaf Node
```cpp
int minDepth(TreeNode* root) {
	if(!root) return 0;
	
	int level = 1;
	queue<TreeNode*> q;
	q.push(root);
	
	while(!q.empty()) {
		int size = q.size();
		for(int i=0; i<size; i++) {
			TreeNode* node = q.front(); q.pop();
			
			if(!node->left && !node->right) return level;
			
			if(node->left) q.push(node->left);
			if(node->right) q.push(node->right);
		}
		
		level++;
	}
	
	return -1;
	
}
```

- Count nodes
![[Pasted image 20260110124245.png]]

```cpp
int countNodes(TreeNode* root) {
	if(!root) return 0;
	
	int leftCount = countNodes(root->left);
	int rightCount = countNodes(root->right);
	
	return leftCount + rightCount + 1;
}
```

- Sum of nodes

```cpp
int sumBT(Node* root) {
    if(!root) return 0;
        
    return sumBT(root->left) + sumBT(root->right) + root->data;  
}
```

- Invert binary tree
	Do not swap values, swap the entire node
	![[Pasted image 20260110141229.png]]
	```cpp
	TreeNode* invertTree(TreeNode* root) {
		if(!root) return nullptr;
		
		TreeNode* left = invertTree(root->left);
		TreeNode* right = invertTree(root->right);
		
		root->left = right;
		root->right = left;
		
		return true;
	}
	```

- Same tree

- Symmetric tree

- Diameter of Tree
	The diameter is the maximum of leftHeight + rightHeight over all nodes, not just the root.
	```cpp
	int diamater = 0;
	
	int dfs(TreeNode* root) {
		if(!root) return 0;
		
		int leftDepth = dfs(root->left);
		int rightDepth = dfs(root->right);
		
		diameter = max(diameter, leftDepth + rightDepth);
		
		return 1 + max(leftDepth, rightDepth);
	}
	
	int diameterOfBinaryTree(TreeNodde* root) {
		dfs(root);
		return diameter;
	}
	```


### Path-Based Problems

- Root-to-leaf path sum

- Path sum II

- Binary tree paths

- Sum root-to-leaf numbers