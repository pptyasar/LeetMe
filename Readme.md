# Complete List of All 57 LeetCode Problems

## Easy Problems

<details>
<summary>1. Two Sum</summary>

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> hMap = new HashMap<>();
        int[] ans = new int[2];
        
        for(int i = 0; i < nums.length; i++) {
            int expectedNum = target - nums[i];
            if(hMap.containsKey(expectedNum) && hMap.get(expectedNum) != i) {
                ans[0] = i;
                ans[1] = hMap.get(expectedNum);
                break;
            }
            hMap.put(nums[i], i);
        }
        return ans;
    }
}
```
</details>

<details>
<summary>20. Valid Parentheses</summary>

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
```
</details>


<details>
<summary>21. Merge Two Sorted Lists</summary>

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
```
</details>

<details>
<summary>28. Find the Index of the First Occurrence in a String</summary>

```java
class Solution {
    public int strStr(String haystack, String needle) {
        char[] chN = needle.toCharArray();
        int needleLength = needle.length();
        int haystackLength = haystack.length();
        
        if(needleLength > haystackLength) return -1;
        
        for(int i = 0; i < haystackLength - needleLength + 1; i++) {
            char ch = haystack.charAt(i);
            if(ch == needle.charAt(0)) {
                int j = 0;
                int tempStartPoint = i;
                int tempCounter = 0;
                while(j < needleLength) {
                    char hayStackCha = haystack.charAt(tempStartPoint);
                    char needleCha = needle.charAt(j);
                    if(hayStackCha == needleCha) {
                        tempCounter++;
                    }
                    j++;
                    tempStartPoint++;
                }
                if(tempCounter == needleLength) {
                    return i;
                }
            }
        }
        return -1;
    }
}
```
</details>

<details>
<summary>70. Climbing Stairs</summary>

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
```
</details>

<details>
<summary>141. Linked List Cycle</summary>

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
```
</details>

<details>
<summary>203. Remove Linked List Elements</summary>

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
```
</details>

<details>
<summary>268. Missing Number</summary>

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
```
</details>

<details>
<summary>303. Range Sum Query - Immutable</summary>

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
