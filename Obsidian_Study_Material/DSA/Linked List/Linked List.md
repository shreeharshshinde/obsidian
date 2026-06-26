## 1. Intuition
- **Structure:** Nodes with pointers to the next node.
- **Strength:** Dynamic size, easy splicing ($O(1)$).
- **Weakness:** No random access ($O(n)$ scan).
- **Meta-Strategy:** Almost all medium/hard problems involve **multiple pointers** (Fast/Slow) or a **Dummy Node** to handle edge cases.

## 2. Core Algorithms

### 2.1 Fast & Slow Pointers (Floyd's Cycle Detection)

- **When to use:** Cycle detection, finding middle, Nth from end.
- **Complexity:** $O(n)$.
- **Notes:** Always safeguard `fast -> next` and `fast`.

#### Getting middle element of LinkedList 

```cpp
ListNode* getMiddle(ListNode* head) {
    ListNode* slow = head;
    ListNode* fast = head;
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
    }
    return slow;
}
```

#### Cycle Detection using Fast and Slow Pointers
Problem : Linked List Cycle Detection

```cpp
bool hasCycle(ListNode *head) {
	ListNode* fast = head;
	ListNode* slow = head;
	
	while(fast && fast->next) {          
		slow = slow->next;
		fast = fast->next->next;
		
		if(slow == fast) return true;
	}
    
    return false;
}
```


##### Advanced Variation : [Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/description/)
Not only do you detect a cycle, but you must **find the exact node where the cycle begins**.

![[Pasted image 20251211223604.png]]

```cpp
ListNode* detectCycle(ListNode* head) {
	ListNode* fast = head;
	ListNode* slow = head;
	
	while(fast && fast->next) {
		slow = slow->next;
		fast = fast->next->next;
		
		if(fast == slow) {
			fast = head;
			
			while(fast != slow) {
				slow = slow->next;
				fast = fast->next;
			}
			
			return fast;
		}
	}
	
	return nullptr;
}
```

![[Pasted image 20251211223451.png]]

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

![[Pasted image 20251212170333.png]]
