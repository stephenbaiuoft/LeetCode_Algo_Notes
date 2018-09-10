### Reverse LinkedList

	Reverse a singly linked list.
	
	Example:
	
	Input: 1->2->3->4->5->NULL
	Output: 5->4->3->2->1->NULL
	Follow up:
	
	A linked list can be reversed either iteratively or recursively. Could you implement both?
	
### Idea 1.0
* backtracking from recursion
* prev node to constantly update and refresh
* headTail to track the tail, which happens to be the head of reversed list

	
### Solution 1.0 Recursion
	class Solution {
	    public ListNode reverseList(ListNode head) {
	        // recursion
	        if (head == null) return head; 
	        reverse(head);
	        prev.next = null;
	        return tailHead;
	    }
	    
	    private ListNode prev = null; 
	    private ListNode tailHead = null;
	    private void reverse(ListNode node) {
	        if (node == null) return;
	        reverse(node.next);
	        
	        if (prev != null) {
	            prev.next = node;
	        } 
	        else if (prev == null) {
	            // this is the tail
	            tailHead = node;
	        }
	        // update prev
	        prev = node;
	    }
	    
	}	
	
### Solution 2.0 Iterative
	class Solution {
		// cur, next, prev 3 pointers!
	    public ListNode reverseList(ListNode head) {
	        // init pointer
	        ListNode cur = head, prev = null, next = null;
	        
	        while(cur != null) {
	            next = cur.next;
	            cur.next = prev;
	            prev = cur;
	            cur = next; 
	        }
	        
	        return prev;
	    }				
	        
   	    
	}		