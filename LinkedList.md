# Linked List LeetCode Problems

<details>
<summary>21. Merge Two Sorted Lists</summary>

Merge two sorted linked lists and return it as a sorted list. The list should be made by splicing together the nodes of the first two lists.

Input: list1 = [1,2,4], list2 = [1,3,4]; Output: [1,1,2,3,4,4]

```java
class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        List<Integer> arrList = new ArrayList();
        
        ListNode headList1 = list1;
        while(headList1 != null) {
            arrList.add(headList1.val);
            headList1 = headList1.next;
        }
        
        ListNode headList2 = list2;
        while(headList2 != null) {
            arrList.add(headList2.val);
            headList2 = headList2.next;
        }
        
        Collections.sort(arrList);
        ListNode dummyNode = new ListNode(-1);
        ListNode currentNode = dummyNode;
        for(int n: arrList) {
            currentNode.next = new ListNode(n);
            currentNode = currentNode.next;
        }
        
        return dummyNode.next;
    }
}

class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        ListNode dummy = new ListNode(-1);
        ListNode current = dummy;
        
        while(list1 != null && list2 != null) {
            if(list1.val <= list2.val) {
                current.next = list1;
                list1 = list1.next;
            } else {
                current.next = list2;
                list2 = list2.next;
            }
            current = current.next;
        }
        
        // Attach remaining nodes
        current.next = (list1 != null) ? list1 : list2;
        
        return dummy.next;
    }
}
```
</details>



<details>
<summary>141. Linked List Cycle</summary>

Given head, the head of a linked list, determine if the linked list has a cycle in it.

Input: head = [3,2,0,-4], pos = 1; Output: true

```java
public class Solution {
    public boolean hasCycle(ListNode head) {
        if(head == null || head.next == null) return false;
        
        ListNode slow = head;
        ListNode fast = head.next;
        
        while(slow != fast) {
            if(fast == null || fast.next == null) return false;
            slow = slow.next;
            fast = fast.next.next;
        }
        return true;
    }
}

public boolean hasCycle(ListNode head) {
    ListNode slow = head;
    ListNode fast = head;
    
    while(fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
        if(slow == fast) return true;
    }
    return false;
}

public boolean hasCycle(ListNode head) {
    HashSet<ListNode> seen = new HashSet<>();
    
    while(head != null) {
        if(seen.contains(head)) return true;
        seen.add(head);
        head = head.next;
    }
    return false;
}
```
</details>


<details>
<summary>203. Remove Linked List Elements</summary>

Given the head of a linked list and an integer val, remove all the nodes of the linked list that has Node.val == val, and return the new head.

Input: head = [1,2,6,3,4,5,6], val = 6; Output: [1,2,3,4,5]

```java
class Solution {
    public ListNode removeElements(ListNode head, int val) {
        ListNode curr = head;
        ListNode dummyNode = new ListNode(0);
        dummyNode.next = head;
        ListNode prevNode = dummyNode;
        
        while(curr != null) {
            if(curr.val == val) {
                prevNode.next = curr.next;
            } else {
                prevNode = curr;
            }
            curr = curr.next;
        }
        return dummyNode.next;
    }
}
```
</details>



<details>
<summary>206. Reverse Linked List</summary>

Given the head of a singly linked list, reverse the list, and return the reversed list.

Input: head = [1,2,3,4,5]; Output: [5,4,3,2,1]

```java
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode prevNode = null;
        ListNode currentNode = head;
        
        while(currentNode != null) {
            ListNode nextNode = currentNode.next;
            currentNode.next = prevNode;
            prevNode = currentNode;
            currentNode = nextNode;
        }
        return prevNode;
    }
}
```
</details>


<details>
<summary>234. Palindrome Linked List</summary>

Given the head of a singly linked list, return true if it is a palindrome.

Input: head = [1,2,2,1]; Output: true

```java
class Solution {
    public boolean isPalindrome(ListNode head) {
        ListNode midNode = getMidNode(head);
        ListNode reveredSecondHalf = getReversedSecondHalf(midNode);
        
        ListNode firstHalfPointer = head;
        ListNode secondHalfPointer = reveredSecondHalf;
        
        while(secondHalfPointer != null) {
            if(firstHalfPointer.val != secondHalfPointer.val) {
                return false;
            }
            firstHalfPointer = firstHalfPointer.next;
            secondHalfPointer = secondHalfPointer.next;
        }
        return true;
    }
    
    ListNode getMidNode(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        
        while(fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }
    
    ListNode getReversedSecondHalf(ListNode head) {
        ListNode prevNode = null;
        ListNode currentNode = head;
        
        while(currentNode != null) {
            ListNode nextNode = currentNode.next;
            currentNode.next = prevNode;
            prevNode = currentNode;
            currentNode = nextNode;
        }
        return prevNode;
    }
}
class Solution {   
    ListNode getReversedSecondHalf(ListNode head) {
        ListNode prevNode = null;
        ListNode currentNode = head;
        
        while(currentNode != null) {
            ListNode nextNode = currentNode.next;
            currentNode.next = prevNode;
            prevNode = currentNode;
            currentNode = nextNode;
        }
        return prevNode;
    }
}

```
</details>



<details>
<summary>876. Middle of the Linked List</summary>

Given the head of a singly linked list, return the middle node of the linked list. If there are two middle nodes, return the second middle node.

Input: head = [1,2,3,4,5]; Output: [3,4,5]

```java
class Solution {
    public ListNode middleNode(ListNode head) {
        List<Integer> arrList = new ArrayList<>();
        
        ListNode tempNode = head;
        while(tempNode != null) {
            arrList.add(tempNode.val);
            tempNode = tempNode.next;
        }
        
        int start = arrList.size() / 2;
        ListNode tNode = new ListNode();
        ListNode resultNode = tNode;
        
        for(; start < arrList.size(); start++) {
            ListNode newListNode = new ListNode(arrList.get(start));
            tNode.next = newListNode;
            tNode = newListNode;
        }
        return resultNode.next;
    }
}

class Solution {
    public ListNode middleNode(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;

        while(fast != null && fast.next != null){

            slow = slow.next;
            fast = fast.next.next;
        }

        return slow;
    }
}
```
</details>



<details>
<summary>148. Sort List</summary>

Given the head of a linked list, return the list after sorting it in ascending order.

Input: head = [4,2,1,3]; Output: [1,2,3,4]

```java
class Solution {
    public ListNode sortList(ListNode head) {
        ArrayList<Integer> arrList = new ArrayList<>();
        
        ListNode tempNode = head;
        while(tempNode != null) {
            arrList.add(tempNode.val);
            tempNode = tempNode.next;
        }
        
        Collections.sort(arrList);
        ListNode tNode = new ListNode();
        ListNode resultNode = tNode;
        
        for(int i = 0; i < arrList.size(); i++) {
            ListNode newNode = new ListNode(arrList.get(i));
            tNode.next = newNode;
            tNode = newNode;
        }
        return resultNode.next;
    }
}

class Solution {
    public ListNode sortList(ListNode head) {
        if (head == null || head.next == null) return head;

        // Split list into two halves
        ListNode slow = head, fast = head, prev = null;
        while (fast != null && fast.next != null) {
            prev = slow;
            slow = slow.next;
            fast = fast.next.next;
        }
        prev.next = null; // break the list

        // Sort each half
        ListNode left = sortList(head);
        ListNode right = sortList(slow);

        // Merge sorted halves
        return merge(left, right);
    }

    private ListNode merge(ListNode a, ListNode b) {
        ListNode dummy = new ListNode(0);
        ListNode tail = dummy;

        while (a != null && b != null) {
            if (a.val < b.val) {
                tail.next = a;
                a = a.next;
            } else {
                tail.next = b;
                b = b.next;
            }
            tail = tail.next;
        }

        tail.next = (a != null) ? a : b;
        return dummy.next;
    }
}


```
</details>



<details>
<summary>23. Merge k Sorted Lists</summary>

You are given an array of k linked-lists lists, each linked-list is sorted in ascending order. Merge all the linked-lists into one sorted linked-list and return it.

Input: lists = [[1,4,5],[1,3,4],[2,6]]; Output: [1,1,2,3,4,4,5,6]

```java
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        ArrayList<Integer> arrList = new ArrayList<>();
        
        for(ListNode ln: lists) {
            ListNode tempListNode = ln;
            while(tempListNode != null) {
                arrList.add(tempListNode.val);
                tempListNode = tempListNode.next;
            }
        }
        
        Collections.sort(arrList);
        ListNode dummyNode = new ListNode(-1);
        ListNode currentNode = dummyNode;
        
        for(Integer in: arrList) {
            ListNode tempNode = currentNode;
            currentNode = new ListNode(in);
            tempNode.next = currentNode;
        }
        return dummyNode.next;
    }
}
```
</details>
