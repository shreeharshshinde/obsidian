Use two pointers moving at different speeds to reveal structural information in a sequence.

- **Slow Pointer:** Moves one step at a time.
- **Fast Pointer:** Moves two steps at a time.

The relative speed between the pointers allows us to discover:

- Middle of a linked list
- Cycle detection
- Cycle entry point
- Nth node from the end
- Splitting a linked list into two halves

---
# Recognition Pattern

Think of Fast & Slow Pointer whenever the problem asks:

- Find the middle.
- Detect a cycle.
- Find where a cycle begins.
- Split a linked list.
- Find Nth node from the end.
- Two objects moving at different speeds.

---

### Getting middle element of Linked List 

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

### Applications

- [876. Middle of Linked List ](https://leetcode.com/problems/middle-of-the-linked-list/description/)
- [234. Palindrome Linked List ](https://leetcode.com/problems/palindrome-linked-list/description/)
- [143. Reorder List ](https://leetcode.com/problems/reorder-list/description/)
### Cycle Detection using Fast and Slow Pointers
Problem : Linked List Cycle Detection

Imagine two runners on a circular track.
- Slow runs 1 step.
- Fast runs 2 steps.

If a cycle exists,
Fast must eventually catch Slow.

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


### Find the Start of the Cycle
##### Advanced Variation : [Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/description/)
Not only do you detect a cycle, but you must **find the exact node where the cycle begins**.

![[Images/Pasted image 20251211223604.png]]
![[Images/Pasted image 20260630144656.png]]

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


