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
	
	private ListNode reverse(ListNode head, ListNode prev) {
		if (head == null) return prev;
		ListNode next = head.next;
		head.next = prev;
		prev = head;
		return reverse(next, prev);
	}
}
```