# Reverse single linke list
#### Iterative
```Java
class Solution {
	
	public ListNode reverseList(ListNode head) {
		ListNode curr = head;
		ListNode prev = null;
		
		while(curr != null) {
			ListNode next = curr.next;
			curr.next = prev;
			prev = curr;
			curr = next;
		}
		return prev;
	}
}

```
#### Recursive
```Java
class Solution {

	public ListNode reverseList(ListNode head) {
		return reverse(head, null);
	}
	
	private ListNode reverse(ListNode head, ListNode newHead) {
		if (head == null) return newHead;
		
		ListNode next = head.next;
		head.next = newHead;
		newHead = head;
		head = next;
		return reverse(head, newHead);
	}
}
```
