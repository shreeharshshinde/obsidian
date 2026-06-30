## 1. Intuition
- **Structure:** Nodes with pointers to the next node.
- **Strength:** Dynamic size, easy splicing ($O(1)$).
- **Weakness:** No random access ($O(n)$ scan).
- **Meta-Strategy:** Almost all medium/hard problems involve **multiple pointers** (Fast/Slow) or a **Dummy Node** to handle edge cases.


```cpp
ListNode* reverseList(ListNode* head) {
	ListNode* prev = nullptr;
	ListNode* curr = head;
	
	while(curr) {
		ListNode* newNode = curr->next;
		curr -> next = prev;
		prev = curr;
		curr = nextNode;
	}
	
	return prev;
}
```

![[Images/Pasted image 20251212170333.png]]
