# Complete List of All 57 LeetCode Problems

## Easy Problems

<details>
<summary>1. Two Sum</summary>

Given an array of integers and a target sum, find the indices of two numbers that add up to the target.

Input: nums = [2,7,11,15], target = 9; Output: [0,1]

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> hMap = new HashMap<>();
        
        for(int i = 0; i < nums.length; i++) {
            int expectedNum = target - nums[i];
            if(hMap.containsKey(expectedNum)) {
                return new int[]{i, hMap.get(expectedNum)};
            }
            hMap.put(nums[i], i);
        }
        return new int[0];  // Or throw exception if guaranteed solution exists
    }
}
```
</details>

<details>
<summary>20. Valid Parentheses</summary>

Determine if a string containing only parentheses is valid, meaning every opening bracket has a matching closing bracket in the correct order.

Input: s = "()"; Output: true

```java
class Solution {
    public boolean isValid(String s) {
        Deque<Character> st = new ArrayDeque<>();
        char[] letters = s.toCharArray();
        
        if(s.length() == 1) return false;
        
        for(char c: letters) {
            if(isOpening(c)) {
                st.push(c);
            } else {
                if(st.size() == 0) return false;
                char expectedOpening = matchingOpen(c);
                char actualOpening = st.pop();
                if(expectedOpening != actualOpening) return false;
            }
        }
        return st.size() == 0;
    }
    
    public boolean isOpening(char ch) {
        return ch == '{' || ch == '(' || ch == '[';
    }
    
    public char matchingOpen(char ch) {
        switch(ch) {
            case '}': return '{';
            case ']': return '[';
            case ')': return '(';
            default: return '.';
        }
    }
}
```
</details>

<details>

<summary>448. Find All Numbers Disappeared in an Array</summary>

Given an array nums of n integers where nums[i] is in the range [1, n], return an array of all the integers in the range [1, n] that do not appear in nums.

Input: nums = [4,3,2,7,8,2,3,1]; Output: [5,6]

```java
class Solution {
    public List<Integer> findDisappearedNumbers(int[] nums) {

        HashSet<Integer> hSet = new HashSet<>();

        ArrayList<Integer> aL = new ArrayList<>();
    

        for(int n:nums){
            hSet.add(n);
        }

        for(int i=1; i<=nums.length; i++){

            if(!hSet.contains(i)){
                aL.add(i);
            }
        }

        return aL;
    }
}

class Solution {
    public List<Integer> findDisappearedNumbers(int[] nums) {
        int n = nums.length;
        
        // Mark present numbers by setting their index to n+1
        for(int i = 0; i < n; i++) {
            int index = Math.abs(nums[i]);
            if(index <= n) {  // Only process valid numbers
                index--;  // Convert to 0-based index
                if(nums[index] <= n) {  // Not yet marked
                    nums[index] += n;  // Mark by adding n
                }
            }
        }
        
        // Collect indices where value <= n (unmarked)
        List<Integer> result = new ArrayList<>();
        for(int i = 0; i < n; i++) {
            if(nums[i] <= n) {
                result.add(i + 1);
            }
        }
        
        return result;
    }
}
```
</details>


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
<summary>28. Find the Index of the First Occurrence in a String</summary>

Given two strings haystack and needle, return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

Input: haystack = "sadbutsad", needle = "sad"; Output: 0

```java
class Solution {
    public int strStr(String haystack, String needle) {
        return haystack.indexOf(needle);
    }
}

class Solution {
    public int strStr(String haystack, String needle) {
        int hLen = haystack.length();
        int nLen = needle.length();
        
        if(nLen > hLen) return -1;
        
        for(int i = 0; i <= hLen - nLen; i++) {
            int j = 0;
            while(j < nLen && haystack.charAt(i + j) == needle.charAt(j)) {
                j++;
            }
            if(j == nLen) return i;
        }
        return -1;
    }
}


```
</details>

<details>
<summary>70. Climbing Stairs</summary>

You are climbing a staircase. It takes n steps to reach the top. Each time you can climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Input: n = 2; Output: 2

```java
class Solution {
    public int climbStairs(int n) {
        if(n <= 2) return n;
        
        int a = 1, b = 2;
        for(int i = 3; i <= n; i++) {
            int c = a + b;
            a = b;
            b = c;
        }
        return b;
    }
}
```
</details>

<details>
<summary>121. Best Time to Buy and Sell Stock</summary>

You are given an array prices where prices[i] is the price of a given stock on the ith day. You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock. Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

Input: prices = [7,1,5,3,6,4]; Output: 5

```java
class Solution {
    public int maxProfit(int[] prices) {
        int maxProfit = 0;
        int minPrice = Integer.MAX_VALUE;
        
        for(int i = 0; i < prices.length; i++) {
            int currentPrize = prices[i];
            if(currentPrize < minPrice) {
                minPrice = currentPrize;
            } else {
                maxProfit = Math.max(maxProfit, currentPrize - minPrice);
            }
        }
        return maxProfit;
    }
}

class Solution {
    public int maxProfit(int[] prices) {
        int maxProfit = 0;
        int minPrice = prices[0];
        
        for(int i = 1; i < prices.length; i++) {  // Start from 1
            int currentPrice = prices[i];
            maxProfit = Math.max(maxProfit, currentPrice - minPrice);
            minPrice = Math.min(minPrice, currentPrice);
        }
        return maxProfit;
    }
}

class Solution {
    public int maxProfit(int[] prices) {
        if(prices.length < 3) return 0;
        
        int maxProfit = 0;
        int minPrice = prices[0];
        
        for(int i = 2; i < prices.length; i++) {
            int currentPrice = prices[i];
            
            // Sell on day i (bought on day i-2 or earlier)
            maxProfit = Math.max(maxProfit, currentPrice - minPrice);
            
            // Update minPrice with day i-1 (to maintain 2-day holding)
            minPrice = Math.min(minPrice, prices[i-1]);
        }
        return maxProfit;
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
<summary>643. Maximum Average Subarray I - Easy</summary>

You are given an integer array nums consisting of n elements, and an integer k. Find a contiguous subarray whose length is equal to k that has the maximum average value and return this value. Any answer with a calculation error less than 10^-5 will be accepted.

Input: nums = [1,12,-5,-6,50,3], k = 4; Output: 12.75

```java
class Solution {
    public double findMaxAverage(int[] nums, int k) {
        double maxAverage = Integer.MIN_VALUE;
        double currentSum = 0;
        
        for (int i = 0; i < nums.length; i++) {
            currentSum += nums[i];
            
            if (i >= k - 1) {
                double average = currentSum / k;
                maxAverage = Math.max(maxAverage, average);
                currentSum -= nums[i - k + 1];
            }
        }
        
        return maxAverage;
    }
}
```
</details>

<details>
<summary>217. Contains Duplicate</summary>

Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

Input: nums = [1,2,3,1]; Output: true

```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        HashSet<Integer> hSet = new HashSet<>();
        
        for(int in: nums) {
            if(!hSet.add(in)) {
                return true;
            }
        }
        return false;
    }
}
```
</details>

<details>
<summary>225. Implement Stack using Queues</summary>

Implement a last-in-first-out (LIFO) stack using only two queues. The implemented stack should support all the functions of a normal stack (push, top, pop, and empty).

MyStack myStack = new MyStack(); myStack.push(1); myStack.push(2); myStack.top(); // return 2; myStack.pop(); // return 2; myStack.empty(); // return false;

```java
class MyStack {
    Queue<Integer> q1;
    Queue<Integer> q2;
    
    public MyStack() {
        q1 = new LinkedList<>();
        q2 = new LinkedList<>();
    }
    
    public void push(int x) {
        q2.offer(x);
        while(!q1.isEmpty()) {
            q2.offer(q1.poll());
        }
        Queue<Integer> temp = q1;
        q1 = q2;
        q2 = temp;
    }
    
    public int pop() {
        return q1.poll();
    }
    
    public int top() {
        return q1.peek();
    }
    
    public boolean empty() {
        return q1.isEmpty();
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
<summary>268. Missing Number</summary>

Given an array nums containing n distinct numbers in the range [0, n], return the only number in the range that is missing from the array.

Input: nums = [3,0,1]; Output: 2

```java
class Solution {
    public int missingNumber(int[] nums) {
        int expectedSum = 0;
        for(int i = 0; i <= nums.length; i++) {
            expectedSum += i;
        }
        
        int actualSum = 0;
        for(int j = 0; j < nums.length; j++) {
            actualSum += nums[j];
        }
        
        return expectedSum - actualSum;
    }
}

class Solution {
    public int missingNumber(int[] nums) {
        int n = nums.length;
        int expectedSum = n * (n + 1) / 2;  // Formula: 0+1+2+...+n
        
        int actualSum = 0;
        for(int num : nums) {
            actualSum += num;
        }
        
        return expectedSum - actualSum;
    }
}
class Solution {
    public int missingNumber(int[] nums) {
        int result = nums.length;
        for(int i = 0; i < nums.length; i++) {
            result = result ^ i ^ nums[i];
        }
        return result;
    }
}
```
</details>

<details>
<summary>303. Range Sum Query - Immutable</summary>

Given an integer array nums, handle multiple queries of the following type: Calculate the sum of the elements of nums between indices left and right inclusive where left <= right. Implement the NumArray class.

NumArray numArray = new NumArray([-2, 0, 3, -5, 2, -1]); numArray.sumRange(0, 2); // return (-2) + 0 + 3 = 1; numArray.sumRange(2, 5); // return 3 + (-5) + 2 + (-1) = -1

```java
class NumArray {
    int[] numArr;
    
    public NumArray(int[] nums) {
        numArr = nums;
    }
    
    public int sumRange(int left, int right) {
        int sum = 0;
        for(int i = left; i <= right; i++) {
            sum += this.numArr[i];
        }
        return sum;
    }
}
```
</details>

<details>
<summary>338. Counting Bits</summary>

Given an integer n, return an array ans of length n + 1 such that for each i (0 <= i <= n), ans[i] is the number of 1's in the binary representation of i.

Input: n = 2; Output: [0,1,1]

```java
class Solution {
    public int[] countBits(int n) {
        int[] ans = new int[n + 1];
        
        for(int i = 0; i <= n; i++) {
            ans[i] = popCount(i);
        }
        return ans;
    }
    
    public int popCount(int n) {
        int count = 0;
        while(n > 0) {
            n &= n - 1;
            count++;
        }
        return count;
    }
}
```
</details>

<details>
<summary>344. Reverse String</summary>

Write a function that reverses a string. The input string is given as an array of characters s.

Input: s = ["h","e","l","l","o"]; Output: ["o","l","l","e","h"]

```java
class Solution {
    public void reverseString(char[] s) {
        int left = 0;
        int right = s.length - 1;
        
        while(left < right) {
            char temp = s[left];
            s[left] = s[right];
            s[right] = temp;
            left++;
            right--;
        }
    }
}
```
</details>


<details>
<summary>459. Repeated Substring Pattern</summary>

Given a string s, check if it can be constructed by taking a substring of it and appending multiple copies of the substring together.

Input: s = "abab"; Output: true

```java
class Solution {
    public boolean repeatedSubstringPattern(String s) {
        String concat = s + s;
        return concat.substring(1, concat.length() - 1).contains(s);
    }
}
```
</details>

<details>
<summary>485. Max Consecutive Ones</summary>

Given a binary array nums, return the maximum number of consecutive 1's in the array.

Input: nums = [1,1,0,1,1,1]; Output: 3

```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int maxCount = 0;
        int counter = 0;
        
        for(int i = 0; i < nums.length; i++) {
            if(nums[i] == 1) {
                counter++;
            } else {
                maxCount = Math.max(maxCount, counter);
                counter = 0;
            }
        }
        maxCount = Math.max(maxCount, counter);
        return maxCount;
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
```
</details>

<details>
<summary>977. Squares of a Sorted Array</summary>

Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.

Input: nums = [-4,-1,0,3,10]; Output: [0,1,9,16,100]

```java
class Solution {
    public int[] sortedSquares(int[] nums) {
        int len = nums.length;
        int leftPoint = 0;
        int rightPoint = len - 1;
        int[] ans = new int[len];
        int index = len - 1;
        
        while(leftPoint <= rightPoint) {
            int leftProd = nums[leftPoint] * nums[leftPoint];
            int rightProd = nums[rightPoint] * nums[rightPoint];
            
            if(leftProd > rightProd) {
                ans[index--] = leftProd;
                leftPoint++;
            } else {
                ans[index--] = rightProd;
                rightPoint--;
            }
        }
        return ans;
    }
}
```
</details>

<details>
<summary>1200. Minimum Absolute Difference</summary>

Given an array of distinct integers arr, find all pairs of elements with the minimum absolute difference of any two elements. Return a list of pairs in ascending order.

Input: arr = [4,2,1,3]; Output: [[1,2],[2,3],[3,4]]

```java
class Solution {
    public List<List<Integer>> minimumAbsDifference(int[] arr) {
        int len = arr.length;
        Arrays.sort(arr);
        int minDiff = Integer.MAX_VALUE;
        List<List<Integer>> arrList = new ArrayList<>();
        
        for(int i = 1; i < len; i++) {
            int currentElem = arr[i];
            int prevElement = arr[i - 1];
            int currentDiff = currentElem - prevElement;
            
            if(currentDiff < minDiff) {
                minDiff = currentDiff;
                arrList.clear();
            }
            
            if(currentDiff == minDiff) {
                arrList.add(Arrays.asList(prevElement, currentElem));
            }
        }
        return arrList;
    }
}
```
</details>

<details>
<summary>1365. How Many Numbers Are Smaller Than the Current Number</summary>

Given the array nums, for each nums[i] find out how many numbers in the array are smaller than it. That is, for each nums[i] you have to count the number of valid j's such that j != i and nums[j] < nums[i]. Return the answer in an array.

Input: nums = [8,1,2,2,3]; Output: [4,0,1,1,3]

```java
class Solution {
    public int[] smallerNumbersThanCurrent(int[] nums) {
        int len = nums.length;
        int[] numsCopy = nums.clone();
        int[] ans = new int[len];
        Arrays.sort(numsCopy);
        
        HashMap<Integer, Integer> hMap = new HashMap<>();
        for(int i = 0; i < len; i++) {
            hMap.putIfAbsent(numsCopy[i], i);
        }
        
        for(int j = 0; j < len; j++) {
            ans[j] = hMap.get(nums[j]);
        }
        return ans;
    }
}
```
</details>

<details>
<summary>1592. Rearrange Spaces Between Words</summary>

You are given a string text of words that are placed among some number of spaces. Each word consists of one or more lowercase English letters and are separated by at least one space. It's guaranteed that text contains at least one word. Rearrange the spaces so that there are an equal number of spaces between every pair of adjacent words and that number is maximized. If you cannot redistribute all the spaces equally, place the extra spaces at the end, meaning the returned string should be the same length as text. Return the string after rearranging the spaces.

Input: text = "  this   is  a sentence "; Output: "this   is   a   sentence"

```java
class Solution {
    public String reorderSpaces(String text) {
        int totalSpaces = 0;
        for(char ch: text.toCharArray()) {
            if(ch == ' ') totalSpaces++;
        }
        
        String[] totalNoWords = text.trim().split("\\s+");
        int gaps = totalNoWords.length - 1;
        int spacesBetweenWords = gaps == 0 ? 0 : totalSpaces / gaps;
        int spacesAtTheEnd = gaps == 0 ? totalSpaces : totalSpaces % gaps;
        
        StringBuilder sb = new StringBuilder();
        String spaces = " ".repeat(spacesBetweenWords);
        
        for(int i = 0; i < totalNoWords.length; i++) {
            sb.append(totalNoWords[i]);
            if(i < totalNoWords.length - 1) {
                sb.append(spaces);
            }
        }
        sb.append(" ".repeat(spacesAtTheEnd));
        return sb.toString();
    }
}
```
</details>

<details>
<summary>1668. Maximum Repeating Substring</summary>

For a string sequence, return the maximum k-repeating value of word in sequence. A word is k-repeating if word concatenated k times is a substring of sequence. Note that the word's maximum k-repeating value is the highest value k where word repeated k times is a substring of sequence. If word is not a substring of sequence, word's k-repeating value is 0.

Input: sequence = "ababc", word = "ab"; Output: 2

```java
class Solution {
    public int maxRepeating(String sequence, String word) {
        int count = 0;
        String pattern = word;
        
        while(sequence.contains(pattern)) {
            count++;
            pattern += word;
        }
        return count;
    }
}
```
</details>

<details>
<summary>1672. Richest Customer Wealth</summary>

You are given an m x n integer grid accounts where accounts[i][j] is the amount of money the i-th customer has in the j-th bank. Return the wealth that the richest customer has. A customer's wealth is the amount of money they have in all their bank accounts. The richest customer is the customer that has the maximum wealth.

Input: accounts = [[1,2,3],[3,2,1]]; Output: 6

```java
class Solution {
    public int maximumWealth(int[][] accounts) {
        int richestSoFar = 0;
        for(int[] acc: accounts) {
            int tempRich = 0;
            for(int we: acc) {
                tempRich += we;
            }
            richestSoFar = Math.max(richestSoFar, tempRich);
        }
        return richestSoFar;
    }
}
```
</details>

<details>
<summary>2073. Time Needed to Buy Tickets</summary>

There are n people in a line queuing to buy tickets, where the 0th person is at the front of the line and the (n - 1)th person is at the back. You are given a 0-indexed integer array tickets of length n where the number tickets[i] represents the number of tickets that the ith person would like to buy. You are standing at position k. Each second, the first person in line will buy a ticket and the number of tickets they want to buy decreases by 1. If they have no more tickets to buy, they will leave the line. If there are people left in the line, the next person becomes the front. Return the time taken for you (i.e. the person at position k) to buy the last ticket you want to buy.

Input: tickets = [2,3,2], k = 2; Output: 6

```java
class Solution {
    public int timeRequiredToBuy(int[] tickets, int k) {
        int totalTime = 0;
        int targetTickets = tickets[k];
        
        for(int i = 0; i < tickets.length; i++) {
            if(i <= k) {
                totalTime += Math.min(tickets[i], targetTickets);
            } else {
                totalTime += Math.min(tickets[i], targetTickets - 1);
            }
        }
        return totalTime;
    }
}
```
</details>

<details>
<summary>2423. Remove Letter To Equalize Frequency</summary>

You are given a 0-indexed string word, consisting of lowercase English letters. You need to select one index and remove the letter at that index from word so that the frequency of every letter present in word is equal. Return true if it is possible to do this, and false otherwise. The frequency of a letter x is the number of times it occurs in the string. You must remove exactly one letter and cannot choose to do nothing.

Input: word = "abcc"; Output: true

```java
public class Solution {
    public boolean equalFrequency(String word) {
        HashMap<Character, Integer> hMap = new HashMap<>();
        
        for(char ch: word.toCharArray()) {
            hMap.put(ch, hMap.getOrDefault(ch, 0) + 1);
        }
        
        for(char ch: word.toCharArray()) {
            hMap.put(ch, hMap.get(ch) - 1);
            if(hMap.get(ch) == 0) {
                hMap.remove(ch);
            }
            
            HashSet<Integer> hSet = new HashSet<>(hMap.values());
            if(hSet.size() == 1) {
                return true;
            }
            
            hMap.put(ch, hMap.getOrDefault(ch, 0) + 1);
        }
        return false;
    }
}
```
</details>

## Medium Problems 

<details>
<summary>3. Longest Substring Without Repeating Characters</summary>

Given a string s, find the length of the longest substring without repeating characters.

Input: s = "abcabcbb"; Output: 3

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        HashMap<Character, Integer> hMap = new HashMap<>();
        int longestNumber = 0, start = 0;
        
        for(int i = 0; i < s.length(); i++) {
            char chh = s.charAt(i);
            if(hMap.containsKey(chh) && hMap.get(chh) >= start) {
                start = hMap.get(chh) + 1;
            }
            hMap.put(chh, i);
            longestNumber = Math.max(longestNumber, i - start + 1);
        }
        return longestNumber;
    }
}
```
</details>

<details>
<summary>15. 3Sum</summary>

Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0. Notice that the solution set must not contain duplicate triplets.

Input: nums = [-1,0,1,2,-1,-4]; Output: [[-1,-1,2],[-1,0,1]]

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(nums);
        
        for(int i = 0; i < nums.length - 2; i++) {
            if(i > 0 && nums[i] == nums[i - 1]) continue;
            
            int left = i + 1;
            int right = nums.length - 1;
            
            while(left < right) {
                int sum = nums[i] + nums[left] + nums[right];
                
                if(sum == 0) {
                    result.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    
                    while(left < right && nums[left] == nums[left + 1]) left++;
                    while(left < right && nums[right] == nums[right - 1]) right--;
                    
                    left++;
                    right--;
                } else if(sum < 0) {
                    left++;
                } else {
                    right--;
                }
            }
        }
        return result;
    }
}
```
</details>

<details>
<summary>36. Valid Sudoku</summary>

Determine if a 9 x 9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules: Each row must contain the digits 1-9 without repetition. Each column must contain the digits 1-9 without repetition. Each of the nine 3 x 3 sub-boxes of the grid must contain the digits 1-9 without repetition. Note: A Sudoku board (partially filled) could be valid but is not necessarily solvable. Only the filled cells need to be validated according to the mentioned rules.

Input: board = [["5","3",".",".","7",".",".",".","."],["6",".",".","1","9","5",".",".","."],[".","9","8",".",".",".",".","6","."],["8",".",".",".","6",".",".",".","3"],["4",".",".","8",".","3",".",".","1"],["7",".",".",".","2",".",".",".","6"],[".","6",".",".",".",".","2","8","."],[".",".",".","4","1","9",".",".","5"],[".",".",".",".","8",".",".","7","9"]]; Output: true

```java
class Solution {
    public boolean isValidSudoku(char[][] board) {
        Set seen = new HashSet();
        for(int i = 0; i < board.length; i++) {
            for(int j = 0; j < board[i].length; j++) {
                char num = board[i][j];
                if(num != '.') {
                    if(!seen.add("Number " + num + " in row " + i) ||
                       !seen.add("Number " + num + " in col " + j) ||
                       !seen.add("Number " + num + " in grid" + i/3 + "-" + j/3)) {
                        return false;
                    }
                }
            }
        }
        return true;
    }
}
```
</details>

<details>
<summary>53. Maximum Subarray</summary>

Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

Input: nums = [-2,1,-3,4,-1,2,1,-5,4]; Output: 6

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int currentSum = nums[0];
        int ans = nums[0];
        
        for(int i = 1; i < nums.length; i++) {
            currentSum = Math.max(nums[i], currentSum + nums[i]);
            ans = Math.max(ans, currentSum);
        }
        return ans;
    }
}
```
</details>

<details>
<summary>54. Spiral Matrix</summary>

Given an m x n matrix, return all elements of the matrix in spiral order.

Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]; Output: [1,2,3,6,9,8,7,4,5]

```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> result = new ArrayList<>();
        int top = 0, bottom = matrix.length - 1;
        int left = 0, right = matrix[0].length - 1;
        
        while(left <= right && top <= bottom) {
            for(int i = left; i <= right; i++) {
                result.add(matrix[top][i]);
            }
            top++;
            
            for(int i = top; i <= bottom; i++) {
                result.add(matrix[i][right]);
            }
            right--;
            
            if(top <= bottom) {
                for(int i = right; i >= left; i--) {
                    result.add(matrix[bottom][i]);
                }
                bottom--;
            }
            
            if(left <= right) {
                for(int i = bottom; i >= top; i--) {
                    result.add(matrix[i][left]);
                }
                left++;
            }
        }
        return result;
    }
}
```
</details>

<details>
<summary>122. Best Time to Buy and Sell Stock II</summary>

You are given an integer array prices where prices[i] is the price of a given stock on the ith day. On each day, you may decide to buy and/or sell the stock. You can only hold at most one share of the stock at any time. However, you can buy it then immediately sell it on the same day. Find and return the maximum profit you can achieve.

Input: prices = [7,1,5,3,6,4]; Output: 7

```java
class Solution {
    public int maxProfit(int[] prices) {
        int profit = 0;
        
        for(int i = 1; i < prices.length; i++) {
            if(prices[i] > prices[i - 1]) {
                profit += prices[i] - prices[i - 1];
            }
        }
        return profit;
    }
}
```
</details>

<details>
<summary>128. Longest Consecutive Sequence</summary>

Given an unsorted array of integers nums, return the length of the longest consecutive elements sequence. You must write an algorithm that runs in O(n) time.

Input: nums = [100,4,200,1,3,2]; Output: 4

```java
class Solution {
    public int longestConsecutive(int[] nums) {
        int longestConsecutive = 0;
        HashSet<Integer> hSet = new HashSet<>();
        
        for(int i = 0; i < nums.length; i++) {
            hSet.add(nums[i]);
        }
        
        for(int i = 0; i < nums.length; i++) {
            int currentNum = nums[i];
            int tempLongestConsecutive = 0;
            
            if(!hSet.contains(currentNum - 1)) {
                while(hSet.contains(currentNum)) {
                    hSet.remove(currentNum);
                    currentNum++;
                    tempLongestConsecutive++;
                }
            }
            longestConsecutive = Math.max(longestConsecutive, tempLongestConsecutive);
        }
        return longestConsecutive;
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
```
</details>

<details>
<summary>150. Evaluate Reverse Polish Notation</summary>

Evaluate the value of an arithmetic expression in Reverse Polish Notation. Valid operators are +, -, *, and /. Each operand may be an integer or another expression. Note that division between two integers should truncate toward zero. It is guaranteed that the given RPN expression is always valid. That means the expression would always evaluate to a result, and there will not be any division by zero operation.

Input: tokens = ["2","1","+","3","*"]; Output: 9

```java
class Solution {
    public int evalRPN(String[] tokens) {
        Stack<Integer> st = new Stack<>();
        
        for(String tok: tokens) {
            if(tok.equals("+") || tok.equals("-") || tok.equals("*") || tok.equals("/")) {
                int a = st.pop();
                int b = st.pop();
                
                switch(tok) {
                    case "+": st.push(a + b); break;
                    case "-": st.push(b - a); break;
                    case "*": st.push(b * a); break;
                    case "/": st.push(b / a); break;
                }
            } else {
                st.push(Integer.parseInt(tok));
            }
        }
        return st.pop();
    }
}
```
</details>

<details>
<summary>152. Maximum Product Subarray</summary>

Given an integer array nums, find a contiguous non-empty subarray within the array that has the largest product, and return the product. The test cases are generated so that the answer will fit in a 32-bit integer.

Input: nums = [2,3,-2,4]; Output: 6

```java
class Solution {
    public int maxProduct(int[] nums) {
        int leftProduct = 1;
        int rightProduct = 1;
        int len = nums.length;
        int ans = nums[0];
        
        for(int i = 0; i < len; i++) {
            leftProduct = leftProduct == 0 ? 1 : leftProduct;
            rightProduct = rightProduct == 0 ? 1 : rightProduct;
            
            leftProduct *= nums[i];
            rightProduct *= nums[len - i - 1];
            
            ans = Math.max(ans, Math.max(leftProduct, rightProduct));
        }
        return ans;
    }
}
```
</details>

<details>
<summary>155. Min Stack</summary>

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time. Implement the MinStack class: MinStack() initializes the stack object. void push(int val) pushes the element val onto the stack. void pop() removes the element on the top of the stack. int top() gets the top element of the stack. int getMin() retrieves the minimum element in the stack. You must implement a solution with O(1) time complexity for each function.

MinStack minStack = new MinStack(); minStack.push(-2); minStack.push(0); minStack.push(-3); minStack.getMin(); // return -3; minStack.pop(); minStack.top(); // return 0; minStack.getMin(); // return -2

```java
class MinStack {
    Stack<Integer> st;
    Stack<Integer> minSt;
    
    public MinStack() {
        st = new Stack();
        minSt = new Stack();
    }
    
    public void push(int val) {
        st.push(val);
        if(minSt.isEmpty()) {
            minSt.push(val);
        } else {
            minSt.push(Math.min(val, minSt.peek()));
        }
    }
    
    public void pop() {
        minSt.pop();
        st.pop();
    }
    
    public int top() {
        return st.peek();
    }
    
    public int getMin() {
        return minSt.peek();
    }
}
```
</details>

<details>
<summary>167. Two Sum II - Input Array Is Sorted</summary>

Given a 1-indexed array of integers numbers that is already sorted in non-decreasing order, find two numbers such that they add up to a specific target number. Let these two numbers be numbers[index1] and numbers[index2] where 1 <= index1 < index2 <= numbers.length. Return the indices of the two numbers, index1 and index2, added by one as an integer array [index1, index2] of length 2. The tests are generated such that there is exactly one solution. You may not use the same element twice. Your solution must use only constant extra space.

Input: numbers = [2,7,11,15], target = 9; Output: [1,2]

```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int len = numbers.length;
        int startIndex = 0;
        int lastIndex = len - 1;
        
        while(startIndex < lastIndex) {
            int currentSum = numbers[startIndex] + numbers[lastIndex];
            
            if(currentSum > target) {
                lastIndex--;
            } else if(currentSum < target) {
                startIndex++;
            } else if(currentSum == target) {
                break;
            }
        }
        
        int[] ans = new int[2];
        ans[0] = startIndex + 1;
        ans[1] = lastIndex + 1;
        return ans;
    }
}
```
</details>

<details>
<summary>189. Rotate Array</summary>

Given an integer array nums, rotate the array to the right by k steps, where k is non-negative.

Input: nums = [1,2,3,4,5,6,7], k = 3; Output: [5,6,7,1,2,3,4]

```java
class Solution {
    public void rotate(int[] nums, int k) {
        int len = nums.length;
        int[] cloneNums = nums.clone();
        int index = 0;
        int kNeed = k % len;
        
        for(int i = len - kNeed; i < len; i++) {
            nums[index] = cloneNums[i];
            index++;
        }
        
        for(int i = 0; i < len - kNeed; i++) {
            nums[index] = cloneNums[i];
            index++;
        }
    }
}
```
</details>

<details>
<summary>209. Minimum Size Subarray Sum</summary>

Given an array of positive integers nums and a positive integer target, return the minimal length of a contiguous subarray [numsl, numsl+1, ..., numsr-1, numsr] of which the sum is greater than or equal to target. If there is no such subarray, return 0 instead.

 
Input: target = 7, nums = [2,3,1,2,4,3]  
Output: 2

```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int len = nums.length;
        int left = 0, right = 0, sumOfCurrentWindow = 0;
        int result = Integer.MAX_VALUE;
        
        for(right = 0; right < len; right++) {
            sumOfCurrentWindow += nums[right];
            
            while(sumOfCurrentWindow >= target) {
                result = Math.min(result, right - left + 1);
                sumOfCurrentWindow -= nums[left++];
            }
        }
        return result == Integer.MAX_VALUE ? 0 : result;
    }
}
```
</details>

<details>
<summary>215. Kth Largest Element in an Array</summary>

Given an integer array nums and an integer k, return the kth largest element in the array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

 
Input: nums = [3,2,1,5,6,4], k = 2  
Output: 5

```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        int len = nums.length;
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        
        for(int i = 0; i < len; i++) {
            int currentNum = nums[i];
            pq.add(currentNum);
            
            if(pq.size() > k) {
                pq.poll();
            }
        }
        return pq.peek();
    }
}
```
</details>

<details>
<summary>238. Product of Array Except Self</summary>

Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i]. The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer. You must write an algorithm that runs in O(n) time and without using the division operation.

 
Input: nums = [1,2,3,4]  
Output: [24,12,8,6]

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int len = nums.length;
        int[] leftProd = new int[len];
        int[] rightProd = new int[len];
        int[] ans = new int[len];
        
        leftProd[0] = 1;
        for(int i = 1; i < len; i++) {
            leftProd[i] = leftProd[i - 1] * nums[i - 1];
        }
        
        rightProd[len - 1] = 1;
        for(int i = len - 2; i >= 0; i--) {
            rightProd[i] = rightProd[i + 1] * nums[i + 1];
        }
        
        for(int i = 0; i < len; i++) {
            ans[i] = rightProd[i] * leftProd[i];
        }
        return ans;
    }
}
```
</details>

<details>
<summary>347. Top K Frequent Elements</summary>

Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.

 
Input: nums = [1,1,1,2,2,3], k = 2  
Output: [1,2]

```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        PriorityQueue<Map.Entry<Integer, Integer>> pq = 
            new PriorityQueue<>((a, b) -> a.getValue() - b.getValue());
        Map<Integer, Integer> hMap = new HashMap<>();
        
        for(int n: nums) {
            hMap.put(n, hMap.getOrDefault(n, 0) + 1);
        }
        
        for(Map.Entry<Integer, Integer> entry: hMap.entrySet()) {
            pq.offer(entry);
            if(pq.size() > k) {
                pq.poll();
            }
        }
        
        int[] ans = new int[pq.size()];
        for(int i = 0; i < k; i++) {
            ans[i] = pq.poll().getKey();
        }
        return ans;
    }
}
```
</details>

<details>
<summary>621. Task Scheduler</summary>

Given a characters array tasks, representing the tasks a CPU needs to do, where each letter represents a different task. Tasks could be done in any order. Each task is done in one unit of time. For each unit of time, the CPU could complete either one task or just be idle. However, there is a non-negative integer n that represents the cooldown period between two same tasks (the same letter in the array), that is that there must be at least n units of time between any two same tasks. Return the least number of units of time that the CPU will take to finish all the tasks.

 
Input: tasks = ["A","A","A","B","B","B"], n = 2  
Output: 8

```java
class Solution {
    public int leastInterval(char[] tasks, int n) {
        int[] freq = new int[26];
        
        for(int task: tasks) {
            freq[task - 'A']++;
        }
        
        Arrays.sort(freq);
        int maxFreq = freq[25];
        int totalMaxFreq = 1;
        
        for(int i = 24; i >= 0; i--) {
            if(freq[i] == maxFreq) {
                totalMaxFreq++;
            } else {
                break;
            }
        }
        
        int partCount = maxFreq - 1;
        int partLength = n + 1;
        int emptySlot = partCount * partLength + totalMaxFreq;
        
        return Math.max(emptySlot, tasks.length);
    }
}
```
</details>

<details>
<summary>622. Design Circular Queue</summary>

Design your implementation of the circular queue. The circular queue is a linear data structure in which the operations are performed based on FIFO (First In First Out) principle and the last position is connected back to the first position to make a circle. It is also called "Ring Buffer". One of the benefits of the circular queue is that we can make use of the spaces in front of the queue. In a normal queue, once the queue becomes full, we cannot insert the next element even if there is a space in front of the queue. But using the circular queue, we can use the space to store new values.

 
MyCircularQueue circularQueue = new MyCircularQueue(3); // set the size to be 3  
circularQueue.enQueue(1);  // return true  
circularQueue.enQueue(2);  // return true  
circularQueue.enQueue(3);  // return true  
circularQueue.enQueue(4);  // return false, the queue is full  
circularQueue.Rear();  // return 3  
circularQueue.isFull();  // return true  
circularQueue.deQueue();  // return true  
circularQueue.enQueue(4);  // return true  
circularQueue.Rear();  // return 4

```java
class MyCircularQueue {
    int[] queue;
    int count;
    int capacity;
    int rear;
    int front;
    
    public MyCircularQueue(int k) {
        count = 0;
        capacity = k;
        rear = 0;
        front = 0;
        queue = new int[k];
    }
    
    public boolean enQueue(int value) {
        if(isFull()) return false;
        queue[rear] = value;
        rear = (rear + 1) % capacity;
        count++;
        return true;
    }
    
    public boolean deQueue() {
        if(isEmpty()) return false;
        count--;
        front = (front + 1) % capacity;
        return true;
    }
    
    public int Front() {
        if(isEmpty()) return -1;
        return queue[front];
    }
    
    public int Rear() {
        if(isEmpty()) return -1;
        return queue[(rear - 1 + capacity) % capacity];
    }
    
    public boolean isEmpty() {
        return count == 0;
    }
    
    public boolean isFull() {
        return count == capacity;
    }
}
```
</details>

<details>
<summary>784. Letter Case Permutation</summary>

Given a string s, we can transform every letter individually to be lowercase or uppercase to create another string. Return a list of all possible strings we could create. Return the output in any order.

 
Input: s = "a1b2"  
Output: ["a1b2","a1B2","A1b2","A1B2"]

```java
class Solution {
    public List<String> letterCasePermutation(String s) {
        List<String> result = new ArrayList<>();
        Queue<String> queue = new LinkedList<>();
        queue.add("");
        
        for(char c: s.toCharArray()) {
            int size = queue.size();
            for(int i = 0; i < size; i++) {
                String current = queue.poll();
                if(Character.isLetter(c)) {
                    queue.add(current + Character.toLowerCase(c));
                    queue.add(current + Character.toUpperCase(c));
                } else {
                    queue.add(current + c);
                }
            }
        }
        result.addAll(queue);
        return result;
    }
}
```
</details>

<details>
<summary>845. Longest Mountain in Array</summary>

You may recall that an array arr is a mountain array if and only if: arr.length >= 3, there exists some index i (0-indexed) with 0 < i < arr.length - 1 such that: arr[0] < arr[1] < ... < arr[i - 1] < arr[i], arr[i] > arr[i + 1] > ... > arr[arr.length - 1]. Given an integer array arr, return the length of the longest mountain in arr. If there is no mountain, return 0.

 
Input: arr = [2,1,4,7,3,2,5]  
Output: 5

```java
class Solution {
    public int longestMountain(int[] arr) {
        int len = arr.length;
        int longest = 0;
        
        for(int i = 1; i < len - 1; i++) {
            if(arr[i] > arr[i - 1] && arr[i] > arr[i + 1]) {
                int left = i;
                int right = i;
                
                while(left > 0 && arr[left] > arr[left - 1]) {
                    left--;
                }
                
                while(right < len - 1 && arr[right] > arr[right + 1]) {
                    right++;
                }
                
                longest = Math.max(longest, right - left + 1);
            }
        }
        return longest;
    }
}
```
</details>

<details>
<summary>912. Sort an Array</summary>

Given an array of integers nums, sort the array in ascending order and return it. You must solve the problem without using any built-in functions in O(nlogn) time complexity and with the smallest space complexity possible.

 
Input: nums = [5,2,3,1]  
Output: [1,2,3,5]

```java
class Solution {
    public int[] sortArray(int[] nums) {
        int[] temp = new int[nums.length];
        mergeSort(nums, temp, 0, nums.length - 1);
        return nums;
    }
    
    private void mergeSort(int[] arr, int[] temp, int left, int right) {
        if(left >= right) return;
        
        int mid = left + (right - left) / 2;
        mergeSort(arr, temp, left, mid);
        mergeSort(arr, temp, mid + 1, right);
        merge(arr, temp, left, mid, right);
    }
    
    private void merge(int[] arr, int[] temp, int left, int mid, int right) {
        int i = left;
        int j = mid + 1;
        int k = left;
        
        while(i <= mid && j <= right) {
            if(arr[i] <= arr[j]) {
                temp[k++] = arr[i++];
            } else {
                temp[k++] = arr[j++];
            }
        }
        
        while(i <= mid) temp[k++] = arr[i++];
        while(j <= right) temp[k++] = arr[j++];
        
        for(int idx = left; idx <= right; idx++) {
            arr[idx] = temp[idx];
        }
    }
}
```
</details>

<details>
<summary>973. K Closest Points to Origin</summary>

Given an array of points where points[i] = [xi, yi] represents a point on the X-Y plane and an integer k, return the k closest points to the origin (0, 0). The distance between two points on the X-Y plane is the Euclidean distance (i.e., √(x1 - x2)2 + (y1 - y2)2). You may return the answer in any order. The answer is guaranteed to be unique (except for the order that it is in).

 
Input: points = [[1,3],[-2,2]], k = 1  
Output: [[-2,2]]

```java
class Solution {
    static class Point implements Comparable<Point> {
        int x, y;
        int distanceFromOrigin;
        int idx;
        
        Point(int x, int y, int distanceFromOrigin, int idx) {
            this.x = x;
            this.y = y;
            this.distanceFromOrigin = distanceFromOrigin;
            this.idx = idx;
        }
        
        @Override
        public int compareTo(Point p2) {
            return this.distanceFromOrigin - p2.distanceFromOrigin;
        }
    }
    
    public int[][] kClosest(int[][] points, int k) {
        PriorityQueue<Point> pq = new PriorityQueue<>();
        
        for(int i = 0; i < points.length; i++) {
            int distanceFromOrigin = points[i][0] * points[i][0] + points[i][1] * points[i][1];
            pq.add(new Point(points[i][0], points[i][1], distanceFromOrigin, i));
        }
        
        int[][] result = new int[k][2];
        for(int j = 0; j < k; j++) {
            Point point = pq.remove();
            result[j][0] = point.x;
            result[j][1] = point.y;
        }
        return result;
    }
}
```
</details>

<details>
<summary>1004. Max Consecutive Ones III</summary>

Given a binary array nums and an integer k, return the maximum number of consecutive 1's in the array if you can flip at most k 0's.

 
Input: nums = [1,1,1,0,0,0,1,1,1,1,0], k = 2  
Output: 6

```java
class Solution {
    public int longestOnes(int[] nums, int k) {
        int l = 0, r = 0, ans = 0, zeroCount = 0;
        int n = nums.length;
        
        while(r < n) {
            if(nums[r] == 0) {
                zeroCount++;
            }
            
            while(zeroCount > k) {
                if(nums[l] == 0) {
                    zeroCount--;
                }
                l++;
            }
            
            ans = Math.max(ans, r - l + 1);
            r++;
        }
        return ans;
    }
}
```
</details>

<details>
<summary>1186. Maximum Subarray Sum with One Deletion</summary>

Given an array of integers, return the maximum sum for a non-empty subarray (contiguous elements) with at most one element deletion. In other words, you want to choose a subarray and optionally delete one element from it so that there is still at least one element left and the sum of the remaining elements is maximum possible.

 
Input: arr = [1,-2,0,3]  
Output: 4

```java
class Solution {
    public int maximumSum(int[] nums) {
        int maxSumNoDelete = nums[0];
        int maxSumOneDelete = 0;
        int maxSum = nums[0];
        
        for(int i = 1; i < nums.length; i++) {
            int currentNum = nums[i];
            maxSumOneDelete = Math.max(currentNum + maxSumOneDelete, maxSumNoDelete);
            maxSumNoDelete = Math.max(currentNum + maxSumNoDelete, currentNum);
            maxSum = Math.max(maxSum, Math.max(maxSumOneDelete, maxSumNoDelete));
        }
        return maxSum;
    }
}
```
</details>

<details>
<summary>2461. Maximum Sum of Distinct Subarrays With Length K</summary>

You are given an integer array nums and an integer k. Find the maximum subarray sum of all the subarrays of nums that meet the following conditions: The length of the subarray is k, and All the elements of the subarray are distinct. Return the maximum subarray sum of all the subarrays that meet the conditions. If no subarray meets the conditions, return 0.

 
Input: nums = [1,5,4,2,9,9,9], k = 3  
Output: 15

```java
class Solution {
    public long maximumSubarraySum(int[] nums, int k) {
        long maxSum = 0, currentSum = 0;
        HashMap<Integer, Integer> hMap = new HashMap<>();
        int n = nums.length;
        
        for(int i = 0; i < n; i++) {
            int currentNum = nums[i];
            currentSum += currentNum;
            hMap.put(currentNum, hMap.getOrDefault(currentNum, 0) + 1);
            
            if(i >= k) {
                int remove = nums[i - k];
                currentSum -= remove;
                hMap.put(remove, hMap.get(remove) - 1);
                if(hMap.get(remove) == 0) {
                    hMap.remove(remove);
                }
            }
            
            if(i >= k - 1 && hMap.size() == k) {
                maxSum = Math.max(maxSum, currentSum);
            }
        }
        return maxSum;
    }
}
```
</details>

## Hard Problems

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

<details>
<summary>1392. Longest Happy Prefix</summary>

A string is called a happy prefix if is a non-empty prefix which is also a suffix (excluding itself). Given a string s, return the longest happy prefix of s. Return an empty string "" if no such prefix exists.

Input: s = "level"; Output: "l"

```java
class Solution {
    public String longestPrefix(String s) {
        int n = s.length();
        int[] lps = new int[n];
        int len = 0;
        
        for(int i = 1; i < n; i++) {
            while(len > 0 && s.charAt(i) != s.charAt(len)) {
                len = lps[len - 1];
            }
            if(s.charAt(i) == s.charAt(len)) {
                len++;
                lps[i] = len;
            }
        }
        return s.substring(0, lps[n - 1]);
    }
}
```
</details>
