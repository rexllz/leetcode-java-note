# Linked List

## 206. Reverse Linked List

Reverse a singly linked list.

**Example:**

```
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
```

**Follow up:**

A linked list can be reversed either iteratively or recursively. Could you implement both?

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    public ListNode reverseList(ListNode head) {

        if(head == null || head.next == null)
            return head;
        ListNode nextNode = head.next;
        ListNode newHead = reverseList(head.next);
        nextNode.next = head;
        head.next = null;
        return newHead;
    }
}
```

## 203. Remove Linked List Elements

Remove all elements from a linked list of integers that have value **val**.

**Example:**

```
Input:  1->2->6->3->4->5->6, val = 6
Output: 1->2->3->4->5
```

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode removeElements(ListNode head, int val) {
        if(head==null)return null;
        head.next = removeElements(head.next,val);
        if(head.val==val)return head.next;
        else return head;   
    }    
}
```

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode removeElements(ListNode head, int val) {
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        ListNode pre = dummy;
        while(pre.next!=null){
            if(pre.next.val==val)pre.next=pre.next.next;
            else pre = pre.next;
        }
        return dummy.next;
    }    
}
```

## 21. Merge Two Sorted Lists

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

**Example:**

```
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if(l1==null)return l2;
        if(l2==null)return l1;
        ListNode dummy = new ListNode(-1);
        ListNode pre = dummy;
        while(l1 != null && l2 != null){
            if(l1.val > l2.val){
                pre.next = l2;
                l2 = l2.next;
            }else {
                pre.next = l1;
                l1 = l1.next;
            }
            pre = pre.next;
        }
        while(l1 != null){
            pre.next = l1;
            l1 = l1.next;
            pre = pre.next;
        }
        while(l2 != null){
            pre.next = l2;
            l2 = l2.next;
            pre = pre.next;
        }
        /**
        if (l1 != null) {
            pre.next = l1;
        }
        if (l2 != null) {
            pre.next = l2;
        }
        **/
        return dummy.next;
    }     
}
```

```java
public class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if(l1 == null)return l2;
        if(l2 == null)return l1;
        if(l1.val > l2.val){
            l2.next = mergeTwoLists(l1,l2.next);
            return l2;
        }
        else {
            l1.next = mergeTwoLists(l1.next,l2);
            return l1;
        }
    }
}
```

## 24. Swap Nodes in Pairs

Given a linked list, swap every two adjacent nodes and return its head.

You may **not** modify the values in the list's nodes, only nodes itself may be changed.

 

**Example:**

```
Given 1->2->3->4, you should return the list as 2->1->4->3.
```

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode swapPairs(ListNode head) {
        if(head == null || head.next == null){
            return head;
        }
        ListNode start = head.next;
        head.next = swapPairs(head.next.next);
        start.next = head;
        return start;
    }
}
```

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode swapPairs(ListNode head) {
        if(head == null || head.next == null){
            return head;
        }
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        ListNode pre = dummy; 
        while(pre.next != null && pre.next.next != null){
            ListNode cur = pre.next;
            ListNode fast = cur.next;
            cur.next = fast.next;
            fast.next = cur;
            pre.next = fast;
            pre = pre.next.next;
        }
        return dummy.next;
    }
}
```

## 147. Insertion Sort List

Sort a linked list using insertion sort.

![img](https://upload.wikimedia.org/wikipedia/commons/0/0f/Insertion-sort-example-300px.gif)
A graphical example of insertion sort. The partial sorted list (black) initially contains only the first element in the list.
With each iteration one element (red) is removed from the input data and inserted in-place into the sorted list

**Algorithm of Insertion Sort:**

1. Insertion sort iterates, consuming one input element each repetition, and growing a sorted output list.
2. At each iteration, insertion sort removes one element from the input data, finds the location it belongs within the sorted list, and inserts it there.
3. It repeats until no input elements remain.

**Example 1:**

```
Input: 4->2->1->3
Output: 1->2->3->4
```

**Example 2:**

```
Input: -1->5->3->4->0
Output: -1->0->3->4->5
```

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode insertionSortList(ListNode head) {
		if( head == null ){
			return head;
		}
		ListNode helper = new ListNode(0); //new starter of the sorted list
		ListNode cur = head; //the node will be inserted
		ListNode pre = helper; //insert node between pre and pre.next
		ListNode next = null; //the next node will be inserted
		//not the end of input list
		while( cur != null ){
			next = cur.next;
			//find the right place to insert
			while( pre.next != null && pre.next.val < cur.val ){
				pre = pre.next;
			}
			//insert between pre and pre.next
			cur.next = pre.next;
			pre.next = cur;
			pre = helper;
			cur = next;
		}
        return helper.next;
	}
}
```

# 