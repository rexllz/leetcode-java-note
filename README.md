# Arrays

## 283. Move Zeroes

Given an array `nums`, write a function to move all `0`'s to the end of it while maintaining the relative order of the non-zero elements.

**Example:**

```
Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
```

copy-array:

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int len = nums.length;
        int[] tmp = new int[len];
        int k = 0;
        for(int i = 0; i<len; i++){
            if(nums[i]!=0){
                tmp[k]=nums[i];
                k++;
            }
        }
        for(int i = 0; i<k; i++){
            nums[i]=tmp[i];
        }
        for(int i = k; i<len; i++){
            nums[i]=0;
        }  
    }
}
```

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int len = nums.length;
        int index = 0;
        for(int i = 0; i<len; i++){
            if(nums[i]!=0){
                nums[index] = nums[i];
                index++;
            }else continue;
        }
        while(index<len)nums[index++]=0;
    }
}
```

## 27. Remove Element

Given an array *nums* and a value *val*, remove all instances of that value [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) and return the new length.

Do not allocate extra space for another array, you must do this by **modifying the input array in-place** with O(1) extra memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

**Example 1:**

```
Given nums = [3,2,2,3], val = 3,

Your function should return length = 2, with the first two elements of nums being 2.

It doesn't matter what you leave beyond the returned length.
```

**Example 2:**

```
Given nums = [0,1,2,2,3,0,4,2], val = 2,

Your function should return length = 5, with the first five elements of nums containing 0, 1, 3, 0, and 4.

Note that the order of those five elements can be arbitrary.

It doesn't matter what values are set beyond the returned length.
```

**Clarification:**

Confused why the returned value is an integer but your answer is an array?

Note that the input array is passed in by **reference**, which means modification to the input array will be known to the caller as well.

Internally you can think of this:

```
// nums is passed in by reference. (i.e., without making a copy)
int len = removeElement(nums, val);

// any modification to nums in your function would be known by the caller.
// using the length returned by your function, it prints the first len elements.
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int len = nums.length;
        int j = 0;
        for(int i = 0; i<len; i++){
            if(nums[i]!=val)nums[j++]=nums[i];
        }
        return j;
    }
}
```

## 26. Remove Duplicates from Sorted Array

Given a sorted array *nums*, remove the duplicates [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) such that each element appear only *once* and return the new length.

Do not allocate extra space for another array, you must do this by **modifying the input array in-place** with O(1) extra memory.

**Example 1:**

```
Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

It doesn't matter what you leave beyond the returned length.
```

**Example 2:**

```
Given nums = [0,0,1,1,1,2,2,3,3,4],

Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.

It doesn't matter what values are set beyond the returned length.
```

**Clarification:**

Confused why the returned value is an integer but your answer is an array?

Note that the input array is passed in by **reference**, which means modification to the input array will be known to the caller as well.

Internally you can think of this:

```
// nums is passed in by reference. (i.e., without making a copy)
int len = removeDuplicates(nums);

// any modification to nums in your function would be known by the caller.
// using the length returned by your function, it prints the first len elements.
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        int len = nums.length;
        int k = 0;
        for(int i = 0; i<len; i++){
            if(nums[i]!=nums[k])nums[++k]=nums[i];
        }
        return k+1;
    }
}
```

## 80. Remove Duplicates from Sorted Array II

Given a sorted array *nums*, remove the duplicates [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) such that duplicates appeared at most *twice* and return the new length.

Do not allocate extra space for another array, you must do this by **modifying the input array in-place** with O(1) extra memory.

**Example 1:**

```
Given nums = [1,1,1,2,2,3],

Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3 respectively.

It doesn't matter what you leave beyond the returned length.
```

**Example 2:**

```
Given nums = [0,0,1,1,1,1,2,3,3],

Your function should return length = 7, with the first seven elements of nums being modified to 0, 0, 1, 1, 2, 3 and 3 respectively.

It doesn't matter what values are set beyond the returned length.
```

**Clarification:**

Confused why the returned value is an integer but your answer is an array?

Note that the input array is passed in by **reference**, which means modification to the input array will be known to the caller as well.

Internally you can think of this:

```
// nums is passed in by reference. (i.e., without making a copy)
int len = removeDuplicates(nums);

// any modification to nums in your function would be known by the caller.
// using the length returned by your function, it prints the first len elements.
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums.length == 0) {return 0;}
        int pointer = 0, flag = 0;
        for (int i = 1; i < nums.length; i++) {
        if (nums[i] == nums[i - 1] && flag == 0) {
            flag = 1;
            pointer++;
        } else if (nums[i] != nums[i - 1]) {
            flag = 0;
            pointer++;
        }
        nums[pointer] = nums[i];
      }
    return pointer + 1;
    }
}
```

## 75. Sort Colors

Given an array with *n* objects colored red, white or blue, sort them **in-place** so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

**Note:** You are not suppose to use the library's sort function for this problem.

**Example:**

```
Input: [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]
```

**Follow up:**

- A rather straight forward solution is a two-pass algorithm using counting sort.
  First, iterate the array counting number of 0's, 1's, and 2's, then overwrite array with total number of 0's, then 1's and followed by 2's.
- Could you come up with a one-pass algorithm using only constant space?

count sort

```java
class Solution {
    public void sortColors(int[] nums) {
        int[] count = new int[3];
        int len = nums.length;
        for(int i = 0; i<3; i++)count[i]=0;
        for(int i = 0; i<len; i++){
            if(nums[i]==0)count[0]++;
            else if(nums[i]==1)count[1]++;
            else count[2]++;
        }
        int index = 0;
        while(count[0]>0){
            nums[index]=0;
            index++;
            count[0]--;
        }
        while(count[1]>0){
            nums[index]=1;
            index++;
            count[1]--;
        }
        while(count[2]>0){
            nums[index]=2;
            index++;
            count[2]--;
        }
    }
}
```

3-way quick sort

```java
class Solution {
    public void sortColors(int[] nums) {
        int len = nums.length;
        int index1 = -1, index2 = len;
        for(int i = 0; i<index2; ){
            if(nums[i]==1){
                i++;
            }else if(nums[i]==2){
                index2--;
                swap(nums,index2,i);
            }else{
                index1++;
                swap(nums,index1,i);
                i++;
            }
        }      
    }
    public void swap(int[] nums, int a, int b){
        int tmp = nums[a];
        nums[a] = nums[b];
        nums[b] = tmp;
    }
}
```

## 88. Merge Sorted Array

Given two sorted integer arrays *nums1* and *nums2*, merge *nums2* into *nums1* as one sorted array.

**Note:**

- The number of elements initialized in *nums1* and *nums2* are *m* and *n* respectively.
- You may assume that *nums1* has enough space (size that is greater or equal to *m* + *n*) to hold additional elements from *nums2*.

**Example:**

```
Input:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

Output: [1,2,2,3,5,6]
```

```java
class Solution {
     public void merge(int A[], int m, int B[], int n) {
        int i = m - 1, j = n - 1, k = m + n - 1;
        while(i >= 0 && j >= 0) {
            A[k--] = A[i] > B[j] ? A[i--] : B[j--];
        }
        while(j >= 0) {
            A[k--] = B[j--];
        }
    }
}
```

## 215. Kth Largest Element in an Array

Find the **k**th largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

**Example 1:**

```
Input: [3,2,1,5,6,4] and k = 2
Output: 5
```

**Example 2:**

```
Input: [3,2,3,1,2,4,5,5,6] and k = 4
Output: 4
```

**Note:** 
You may assume k is always valid, 1 ≤ k ≤ array's length.

```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        int len = nums.length;
        int t = 0;
        while(t<k){
            for(int i = t+1; i<len; i++){
            if(nums[i]>nums[t]){
                swap(nums,i,t);
                }
            }
            t++;
        }
        return nums[k-1];
    }
    public void swap(int[] arr, int a, int b){
        int tmp = arr[a];
        arr[a] = arr[b];
        arr[b] = tmp;
    }
}
```

```java
public class Solution {
    public int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> largeK = new PriorityQueue<Integer>(k + 1);
        for(int el : nums) {
            largeK.add(el);
            if (largeK.size() > k) {
                largeK.poll();
            }
        }
        return largeK.poll();
    }
}
```

# HashSet/Map

## 349. Intersection of Two Arrays

Given two arrays, write a function to compute their intersection.

**Example 1:**

```
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2]
```

**Example 2:**

```
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [9,4]
```

**Note:**

- Each element in the result must be unique.
- The result can be in any order.

```java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        HashSet<Integer> set = new HashSet<>();
        HashSet<Integer> set1 = new HashSet<>();
        for(int i = 0; i<nums1.length; i++){
            set.add(nums1[i]);
        }
        for(int i = 0; i<nums2.length; i++){
            if(set.contains(nums2[i]))set1.add(nums2[i]);
        }
        int size = set1.size();
        int[] out = new int[size];
        int i = 0;
        for(Integer x : set1)out[i++]=x;
        return out;
    }
}
```

## 350. Intersection of Two Arrays II

Given two arrays, write a function to compute their intersection.

**Example 1:**

```
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2,2]
```

**Example 2:**

```
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [4,9]
```

**Note:**

- Each element in the result should appear as many times as it shows in both arrays.
- The result can be in any order.

**Follow up:**

- What if the given array is already sorted? How would you optimize your algorithm?
- What if *nums1*'s size is small compared to *nums2*'s size? Which algorithm is better?
- What if elements of *nums2* are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?

```java
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        HashMap<Integer, Integer> map = new HashMap<>();
        int start = 0;
        for(int i = 0; i<nums1.length; i++){
            map.put(nums1[i],map.getOrDefault(nums1[i],0)+1);
        }
        for(int i = 0; i<nums2.length; i++){
            if(map.containsKey(nums2[i]) && map.get(nums2[i])>0){
                nums1[start]=nums2[i];
                start++;
                map.put((nums2[i]),map.get(nums2[i])-1);
            }else continue;    
        }
        return Arrays.copyOfRange(nums1,0,start);
    }
}
```

## 202. Happy Number

Write an algorithm to determine if a number is "happy".

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

**Example:** 

```
Input: 19
Output: true
Explanation: 
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
```

```java
class Solution {
    public boolean isHappy(int n) {
        int res = 0;
        int result = n;
        boolean flag = true;
        HashSet<Integer> set = new HashSet<>();
        while(result!=1){
            while(result/10>0 || result%10!=0){
                res = res + (result%10)*(result%10);
                result /= 10;
            }
            if(set.contains(res)){
                flag = false;
                break;
            }
            result = res;
            res = 0;
            set.add(result);
        }
        return flag;
    }
}
```

## 454. 4Sum II

Given four lists A, B, C, D of integer values, compute how many tuples `(i, j, k, l)` there are such that `A[i] + B[j] + C[k] + D[l]` is zero.

To make problem a bit easier, all A, B, C, D have same length of N where 0 ≤ N ≤ 500. All integers are in the range of -228 to 228 - 1 and the result is guaranteed to be at most 231 - 1.

**Example:**

```
Input:
A = [ 1, 2]
B = [-2,-1]
C = [-1, 2]
D = [ 0, 2]

Output:
2

Explanation:
The two tuples are:
1. (0, 0, 0, 1) -> A[0] + B[0] + C[0] + D[1] = 1 + (-2) + (-1) + 2 = 0
2. (1, 1, 0, 0) -> A[1] + B[1] + C[0] + D[0] = 2 + (-1) + (-1) + 0 = 0
```

```java
class Solution {
    public int fourSumCount(int[] A, int[] B, int[] C, int[] D) {
        int len = A.length;
        int res = 0;
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        for(int i = 0; i<len; i++){
            for(int j = 0; j<len; j++){
                if(!map.containsKey(A[i]+B[j])){
                    map.put(A[i]+B[j], 1);
                }else{
                    map.put(A[i]+B[j], map.get(A[i]+B[j])+1);
                }
            }
        }
        for(int i = 0; i<len; i++)
            for(int j = 0; j<len; j++){
                if(map.containsKey(0 - C[i] - D[j])){
                    res += map.get(0 - C[i] - D[j]);
                }
            }
        return res;
    }
}
```

## 49. Group Anagrams

Given an array of strings, group anagrams together.

**Example:**

```
Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

**Note:**

- All inputs will be in lowercase.
- The order of your output does not matter.

```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        List<List<String>> list = new ArrayList<List<String>>();
        HashMap<String, List<String>> map = new HashMap<String, List<String>>();
        for(String str : strs){
            char[] cs = str.toCharArray();
            Arrays.sort(cs);
            String ketstr = String.valueOf(cs);
            if(!map.containsKey(ketstr))
                map.put(ketstr, new ArrayList<String>());
            map.get(ketstr).add(str);
        }
        for(String key : map.keySet()){
            list.add(map.get(key));
        }
        return list;
        return new ArrayList<List<String>>(map.values());
    }
}
```

## 447. Number of Boomerangs

Given *n* points in the plane that are all pairwise distinct, a "boomerang" is a tuple of points `(i, j, k)` such that the distance between `i` and `j` equals the distance between `i` and `k` (**the order of the tuple matters**).

Find the number of boomerangs. You may assume that *n* will be at most **500** and coordinates of points are all in the range **[-10000, 10000]** (inclusive).

**Example:**

```
Input:
[[0,0],[1,0],[2,0]]

Output:
2

Explanation:
The two boomerangs are [[1,0],[0,0],[2,0]] and [[1,0],[2,0],[0,0]]
```

```java
class Solution {
    public int numberOfBoomerangs(int[][] points) {
        int len = points.length;
        int count = 0;
        double dis = 0;
        for(int i = 0; i<len; i++){
            HashMap<Double, Integer> map = new HashMap<Double, Integer>();
            for(int j = 0; j<len; j++){
                if(i != j){
                    dis = Math.pow(points[i][0] - points[j][0], 2) + 
                    Math.pow(points[i][1] - points[j][1], 2);
                    if(!map.containsKey(dis))map.put(dis, 1);
                    else map.put(dis, map.get(dis)+1);
                }
            }
            for(Double x : map.keySet()){
                if(map.get(x) == 1)continue;
                int sum = map.get(x)*(map.get(x)-1);
                count += sum;
            }
        }
        return count;
    }
}
```

## 219. Contains Duplicate II

Given an array of integers and an integer *k*, find out whether there are two distinct indices *i* and *j* in the array such that **nums[i] = nums[j]** and the **absolute** difference between *i* and *j* is at most *k*.

**Example 1:**

```
Input: nums = [1,2,3,1], k = 3
Output: true
```

**Example 2:**

```
Input: nums = [1,0,1,1], k = 1
Output: true
```

**Example 3:**

```
Input: nums = [1,2,3,1,2,3], k = 2
Output: false
```

```java
class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        
        HashMap<Integer,Integer> map = new HashMap<>();
        
        for(int i = 0; i<nums.length; i++){
            
            if(map.containsKey(nums[i])){
                if(i-map.get(nums[i])<=k)return true;
            }
            map.put(nums[i], i);
        }
        return false;
    }
}
```

## 220. Contains Duplicate III

Given an array of integers, find out whether there are two distinct indices *i* and *j* in the array such that the **absolute** difference between **nums[i]** and **nums[j]** is at most *t* and the **absolute** difference between *i* and *j* is at most *k*.

**Example 1:**

```
Input: nums = [1,2,3,1], k = 3, t = 0
Output: true
```

**Example 2:**

```
Input: nums = [1,0,1,1], k = 1, t = 2
Output: true
```

**Example 3:**

```
Input: nums = [1,5,9,1,5,9], k = 2, t = 3
Output: false
```

```java
class Solution {
    public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
/*handle special case*/
    if(nums.length <= 1 || t < 0 || k < 1) {return false;}
    TreeSet<Long> set = new TreeSet<Long>();
    for(int i = 0; i < nums.length; i++){
        long min = Math.min((long)nums[i] - t,(long)nums[i] + t + 1);
        long max = Math.max((long)nums[i] - t, (long)nums[i] + t + 1);
    /*1.if the subset is not empty, means that we have the element that satisfy the requirement 
      2.if we cannot add the element to the set, that means we already have the element*/
        if(!set.subSet(min,max).isEmpty() || !set.add((long)nums[i])) {return true;}
        set.add((long)nums[i]);
        if(i >= k) {set.remove((long)nums[i - k]);}
    }
    return false;
  }
}
```

## 209. Minimum Size Subarray Sum

Given an array of **n** positive integers and a positive integer **s**, find the minimal length of a **contiguous** subarray of which the sum ≥ **s**. If there isn't one, return 0 instead.

**Example:** 

```
Input: s = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: the subarray [4,3] has the minimal length under the problem constraint.
```

**Follow up:**

If you have figured out the *O*(*n*) solution, try coding another solution of which the time complexity is *O*(*n* log *n*). 

```java
class Solution {
    public int minSubArrayLen(int s, int[] nums) {
        int len = nums.length;
        int l = 0;
        int r = -1;
        int tmp = 0;
        int sum = len + 1;
        while(l<len){
            if(tmp<s && r+1<nums.length){
                tmp += nums[++r];
            }else {
                tmp -= nums[l++];
            }
            
            if(tmp >= s){
                sum = Math.min(sum, r-l+1);
            }
        }
        if(sum == len + 1)return 0;
        return sum;
    }
}
```

## 3. Longest Substring Without Repeating Characters

Given a string, find the length of the **longest substring** without repeating characters.

**Example 1:**

```
Input: "abcabcbb"
Output: 3 
Explanation: The answer is "abc", with the length of 3. 
```

**Example 2:**

```
Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```

**Example 3:**

```
Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3. 
             Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int count = 0;
        HashSet<Character> set = new HashSet<>();
        int l = 0;
        int r = -1;
        while(l<s.length()){
            if(r+1 < s.length() && !set.contains(s.charAt(r+1))){
                set.add(s.charAt(r+1));
                r++;
            }else{
                set.remove(s.charAt(l++));
            }
            count = Math.max(count, r-l+1);
        }
        return count;
    }
}
```

## 438. Find All Anagrams in a String

Given a string **s** and a **non-empty** string **p**, find all the start indices of **p**'s anagrams in **s**.

Strings consists of lowercase English letters only and the length of both strings **s** and **p** will not be larger than 20,100.

The order of output does not matter.

**Example 1:**

```
Input:
s: "cbaebabacd" p: "abc"

Output:
[0, 6]

Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
```



**Example 2:**

```
Input:
s: "abab" p: "ab"

Output:
[0, 1, 2]

Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
```

```java
public class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        List<Integer> bIndices = new ArrayList<>();
        if (s == null || s.length() == 0) {
            return bIndices;
        }
        Map<Character, Integer> freq = new HashMap<>();
        for (int i = 0; i < p.length(); i++) {
            char ch = p.charAt(i);
            freq.put(ch, freq.containsKey(ch) ? freq.get(ch) + 1 : 1);
        }
        for (int bIndex = 0, eIndex = 0; eIndex < s.length(); eIndex++) {
            char candidate = s.charAt(eIndex);
            while (!freq.containsKey(candidate) && bIndex <= eIndex) {
                if (bIndex < eIndex) {
                    char bch = s.charAt(bIndex);
                    freq.put(bch, freq.containsKey(bch) ? freq.get(bch) + 1 : 1);
                }
                bIndex++;
            }
            if (bIndex <= eIndex) {
                freq.put(candidate, freq.get(candidate) - 1);
                if (freq.get(candidate) == 0) {
                    freq.remove(candidate);
                }
                if (freq.size() == 0) {
                    bIndices.add(bIndex);
                    char bch = s.charAt(bIndex++);
                    freq.put(bch, freq.containsKey(bch) ? freq.get(bch) + 1 : 1);
                }
            }
        }
        return bIndices;
    }
}
```

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

# Stack

## 20. Valid Parentheses

Given a string containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

Note that an empty string is also considered valid.

**Example 1:**

```
Input: "()"
Output: true
```

**Example 2:**

```
Input: "()[]{}"
Output: true
```

**Example 3:**

```
Input: "(]"
Output: false
```

**Example 4:**

```
Input: "([)]"
Output: false
```

**Example 5:**

```
Input: "{[]}"
Output: true
```

```java
public class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();
        for(int i = 0; i < s.length(); i++) {
            char a = s.charAt(i);
            if(a == '(' || a == '[' || a == '{') stack.push(a);
            else if(stack.empty()) return false;
            else if(a == ')' && stack.pop() != '(') return false;
            else if(a == ']' && stack.pop() != '[') return false;
            else if(a == '}' && stack.pop() != '{') return false;
        }
        return stack.empty();
    }
}
```

## 150. Evaluate Reverse Polish Notation

Evaluate the value of an arithmetic expression in [Reverse Polish Notation](http://en.wikipedia.org/wiki/Reverse_Polish_notation).

Valid operators are `+`, `-`, `*`, `/`. Each operand may be an integer or another expression.

**Note:**

- Division between two integers should truncate toward zero.
- The given RPN expression is always valid. That means the expression would always evaluate to a result and there won't be any divide by zero operation.

**Example 1:**

```
Input: ["2", "1", "+", "3", "*"]
Output: 9
Explanation: ((2 + 1) * 3) = 9
```

**Example 2:**

```
Input: ["4", "13", "5", "/", "+"]
Output: 6
Explanation: (4 + (13 / 5)) = 6
```

**Example 3:**

```
Input: ["10", "6", "9", "3", "+", "-11", "*", "/", "*", "17", "+", "5", "+"]
Output: 22
Explanation: 
  ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22
```

```java
public class Solution {
    public int evalRPN(String[] tokens) {
        int a,b;
		Stack<Integer> S = new Stack<Integer>();
		for (String s : tokens) {
			if(s.equals("+")) {
				S.add(S.pop()+S.pop());
			}
			else if(s.equals("/")) {
				b = S.pop();
				a = S.pop();
				S.add(a / b);
			}
			else if(s.equals("*")) {
				S.add(S.pop() * S.pop());
			}
			else if(s.equals("-")) {
				b = S.pop();
				a = S.pop();
				S.add(a - b);
			}
			else {
				S.add(Integer.parseInt(s));
			}
		}	
		return S.pop();
	}
}
```

## 71. Simplify Path

Given an **absolute path** for a file (Unix-style), simplify it. Or in other words, convert it to the **canonical path**.

In a UNIX-style file system, a period `.` refers to the current directory. Furthermore, a double period `..` moves the directory up a level. For more information, see: [Absolute path vs relative path in Linux/Unix](https://www.linuxnix.com/abslute-path-vs-relative-path-in-linuxunix/)

Note that the returned canonical path must always begin with a slash `/`, and there must be only a single slash `/` between two directory names. The last directory name (if it exists) **must not** end with a trailing `/`. Also, the canonical path must be the **shortest** string representing the absolute path.

 

**Example 1:**

```
Input: "/home/"
Output: "/home"
Explanation: Note that there is no trailing slash after the last directory name.
```

**Example 2:**

```
Input: "/../"
Output: "/"
Explanation: Going one level up from the root directory is a no-op, as the root level is the highest level you can go.
```

**Example 3:**

```
Input: "/home//foo/"
Output: "/home/foo"
Explanation: In the canonical path, multiple consecutive slashes are replaced by a single one.
```

**Example 4:**

```
Input: "/a/./b/../../c/"
Output: "/c"
```

**Example 5:**

```
Input: "/a/../../b/../c//.//"
Output: "/c"
```

**Example 6:**

```
Input: "/a//b////c/d//././/.."
Output: "/a/b/c"
```

```java
public String simplifyPath(String path) {
    Stack<String> stack = new Stack<>();
    String[] p = path.split("/");
    for (int i = 0; i < p.length; i++) {
        if (!stack.empty() && p[i].equals(".."))
            stack.pop();
        else if (!p[i].equals(".") && !p[i].equals("") && !p[i].equals(".."))
            stack.push(p[i]);
    }
    List<String> list = new ArrayList(stack);
    return "/"+String.join("/", list);
}
```

# Queue

## 102. Binary Tree Level Order Traversal

Given a binary tree, return the *level order* traversal of its nodes' values. (ie, from left to right, level by level).

For example:
Given binary tree `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

return its level order traversal as:

```
[
  [3],
  [9,20],
  [15,7]
]
```

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        List<List<Integer>> wrapList = new LinkedList<List<Integer>>();
        
        if(root == null) return wrapList;
        
        queue.offer(root);
        while(!queue.isEmpty()){
            int levelNum = queue.size();
            List<Integer> subList = new LinkedList<Integer>();
            for(int i=0; i<levelNum; i++) {
                if(queue.peek().left != null) queue.offer(queue.peek().left);
                if(queue.peek().right != null) queue.offer(queue.peek().right);
                subList.add(queue.poll().val);
            }
            wrapList.add(subList);
        }
        return wrapList;
    }
}
```

## 103. Binary Tree Zigzag Level Order Traversal

Given a binary tree, return the *zigzag level order* traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).

For example:
Given binary tree `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

return its zigzag level order traversal as:

```
[
  [3],
  [20,9],
  [15,7]
]
```

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
    List<List<Integer>> result = new ArrayList<List<Integer>>();
    if(root == null){ return result;}
    Queue<TreeNode> queue = new LinkedList<TreeNode>();
    queue.add(root);
    boolean reverseOrder = false;
    while(!queue.isEmpty()){
        int size = queue.size();
        List<Integer> levelResult = new ArrayList<Integer>();
        for(int i = 0; i < size; i++){
            TreeNode temp = queue.remove();
            levelResult.add(temp.val);
            if(temp.left != null){ queue.add(temp.left);}
            if(temp.right != null){ queue.add(temp.right);}
        }
        if(reverseOrder){
            Collections.reverse(levelResult);
        }
        result.add(levelResult);
        reverseOrder = !reverseOrder;
    }
    return result;
}
}
```

## 199. Binary Tree Right Side View

Given a binary tree, imagine yourself standing on the *right* side of it, return the values of the nodes you can see ordered from top to bottom.

**Example:**

```
Input: [1,2,3,null,5,null,4]
Output: [1, 3, 4]
Explanation:

   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
```

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> list = new LinkedList<Integer>();
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        if(root == null)return list;
        queue.offer(root);
        while(!queue.isEmpty()){
            int num = queue.size();
            for(int i = 0; i<num; i++){
                if(queue.peek().left!=null)queue.offer(queue.peek().left);
                if(queue.peek().right!=null)queue.offer(queue.peek().right);
                if(i == num-1)list.add(queue.poll().val);
                else queue.poll();
            }
        }
        return list;
    }
}
```

## 347. Top K Frequent Elements

Given a non-empty array of integers, return the **k** most frequent elements.

**Example 1:**

```
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```

**Example 2:**

```
Input: nums = [1], k = 1
Output: [1]
```

**Note:**

- You may assume *k* is always valid, 1 ≤ *k* ≤ number of unique elements.
- Your algorithm's time complexity **must be** better than O(*n* log *n*), where *n* is the array's size.

```java
class Solution {
    public List<Integer> topKFrequent(int[] nums, int k) {
        
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        
        // count frequency
        for(int n : nums){
            map.put(n, map.getOrDefault(n, 0) + 1);
        }
        
        // create priority queue, ordering map entries with respect to the frequency
        PriorityQueue<Map.Entry<Integer, Integer>> queue = 
        new PriorityQueue<Map.Entry<Integer, Integer>>(new Comparator<Map.Entry<Integer, Integer>>()
        {
           @Override
           public int compare(Map.Entry<Integer, Integer> entry1, Map.Entry<Integer, Integer> entry2)
             {
                return entry2.getValue() - entry1.getValue();
             }
        });
        /*PriorityQueue<Map.Entry<Integer, Integer>> maxHeap = 
        new PriorityQueue<>((a,b)->(b.getValue()-a.getValue()));
        */
    
        
        // insert in the queue
        for(Map.Entry<Integer, Integer> entry : map.entrySet()){
            queue.offer(entry);
        }
        
        // poll the top k
        List<Integer> list = new LinkedList<Integer>();
        for(int i = 0; i < k; i ++){
            // Map.Entry<Integer, Integer> entry = queue.poll();
            list.add(queue.poll().getKey());
        }
        return list;
    } 
}
```

# Binary Tree

## 104. Maximum Depth of Binary Tree

Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

**Note:** A leaf is a node with no children.

**Example:**

Given binary tree `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

return its depth = 3.

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public int maxDepth(TreeNode root) {
        if(root == null)return 0;
        
        return Math.max(maxDepth(root.left),maxDepth(root.right)) + 1;
    }
}
```

## 111. Minimum Depth of Binary Tree

Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

**Note:** A leaf is a node with no children.

**Example:**

Given binary tree `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

return its minimum depth = 2.

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public int minDepth(TreeNode root) {
        if(root == null)return 0;
        if(root.left == null && root.right == null)return 1;
        else if(root.left == null) return minDepth(root.right)+1;
        else if(root.right == null) return minDepth(root.left)+1;
        else
        return Math.min(minDepth(root.left),minDepth(root.right)) + 1;
    }
}
```

## 226. Invert Binary Tree

Invert a binary tree.

**Example:**

Input:

```
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```

Output:

```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

**Trivia:**
This problem was inspired by [this original tweet](https://twitter.com/mxcl/status/608682016205344768) by [Max Howell](https://twitter.com/mxcl):

> Google: 90% of our engineers use the software you wrote (Homebrew), but you can’t invert a binary tree on a whiteboard so f*** off.

很逗哈哈

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode invertTree(TreeNode root) {
        
        if(root == null)return root;
        TreeNode tmp = root.left;
        root.left = invertTree(root.right);
        root.right = invertTree(tmp);
        return root;
    }
}
```

## Symmetric Tree

Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree `[1,2,2,3,4,4,3]` is symmetric:

```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```



But the following `[1,2,2,null,3,null,3]` is not:

```
    1
   / \
  2   2
   \   \
   3    3
```



**Note:**
Bonus points if you could solve it both recursively and iteratively.

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public boolean isSymmetric(TreeNode root) {
    return root==null || isSymmetricHelp(root.left, root.right);
    }

    private boolean isSymmetricHelp(TreeNode left, TreeNode right){
        if(left==null || right==null)
            return left==right;
        if(left.val!=right.val)
            return false;
        return 
            isSymmetricHelp(left.left, right.right) && 
            isSymmetricHelp(left.right, right.left);
    }
}
```

## 222. Count Complete Tree Nodes

Given a **complete** binary tree, count the number of nodes.

**Note:**

**Definition of a complete binary tree from Wikipedia:**
In a complete binary tree every level, except possibly the last, is completely filled, and all nodes in the last level are as far left as possible. It can have between 1 and 2h nodes inclusive at the last level h.

**Example:**

```
Input: 
    1
   / \
  2   3
 / \  /
4  5 6

Output: 6
```

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public int countNodes(TreeNode root) {
        if(root == null)return 0;
        return countNodes(root.left) + countNodes(root.right) + 1;
    }
}
```

## 110. Balanced Binary Tree

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:

> a binary tree in which the depth of the two subtrees of *every* node never differ by more than 1.

**Example 1:**

Given the following tree `[3,9,20,null,null,15,7]`:

```
    3
   / \
  9  20
    /  \
   15   7
```

Return true.

**Example 2:**

Given the following tree `[1,2,2,3,3,null,null,4,4]`:

```
       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
```

Return false.

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    private boolean result = true;

    public boolean isBalanced(TreeNode root) {
        maxDepth(root);
        return result;
    }

    public int maxDepth(TreeNode root) {
        if (root == null)
            return 0;
        int l = maxDepth(root.left);
        int r = maxDepth(root.right);
        if (Math.abs(l - r) > 1)
            result = false;
        return 1 + Math.max(l, r);
    }
}
```

## 112. Path Sum

Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

**Note:** A leaf is a node with no children.

**Example:**

Given the below binary tree and `sum = 22`,

```
      5
     / \
    4   8
   /   / \
  11  13  4
 /  \      \
7    2      1
```

return true, as there exist a root-to-leaf path `5->4->11->2` which sum is 22.

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public boolean hasPathSum(TreeNode root, int sum) {
        if(root == null)return false;
        sum = sum - root.val;
        if(root.left == null && root.right == null)
            return sum == 0;
        return hasPathSum(root.left, sum) || hasPathSum(root.right, sum);
    }
}
```

## 404. Sum of Left Leaves

Find the sum of all left leaves in a given binary tree.

**Example:**

```
    3
   / \
  9  20
    /  \
   15   7

There are two left leaves in the binary tree, with values 9 and 15 respectively. Return 24.
```

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public int sumOfLeftLeaves(TreeNode root) {
        if(root == null)return 0;
        if(root.left == null)return sumOfLeftLeaves(root.right);
        TreeNode next = root.left;
        if(next.left == null && next.right == null)
            return next.val + sumOfLeftLeaves(root.right);
        return sumOfLeftLeaves(root.left) + sumOfLeftLeaves(root.right);
    }
}
```

## 257. Binary Tree Paths

Given a binary tree, return all root-to-leaf paths.

**Note:** A leaf is a node with no children.

**Example:**

```
Input:

   1
 /   \
2     3
 \
  5

Output: ["1->2->5", "1->3"]

Explanation: All root-to-leaf paths are: 1->2->5, 1->3
```

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> list = new ArrayList<String>();
        if(root == null)return list;
        treePath(root, "", list);
        return list;
    }
    
    public void treePath(TreeNode root, String path, List<String> list){
        if(root.left == null && root.right == null)
            list.add(path + root.val);
        else if(root.left == null)
            treePath(root.right, path + root.val + "->", list);
        else if(root.right == null)
            treePath(root.left, path + root.val + "->", list);
        else {
            treePath(root.right, path + root.val + "->", list);
            treePath(root.left, path + root.val + "->", list);
        }
    }
}
```

# Recursive

## 131. Palindrome Partitioning

Given a string *s*, partition *s* such that every substring of the partition is a palindrome.

Return all possible palindrome partitioning of *s*.

**Example:**

```
Input: "aab"
Output:
[
  ["aa","b"],
  ["a","a","b"]
]
```

```java
class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> res = new ArrayList<>();
        boolean[][] dp = new boolean[s.length()][s.length()];
        for(int i = 0; i < s.length(); i++) {
            for(int j = 0; j <= i; j++) {
                if(s.charAt(i) == s.charAt(j) && (i - j <= 2 || dp[j+1][i-1])) {
                    dp[j][i] = true;
                }
            }
        }
        helper(res, new ArrayList<>(), dp, s, 0);
        return res;
    }
    
    private void helper(List<List<String>> res, List<String> path, boolean[][] dp, String s, int pos) {
        if(pos == s.length()) {
            res.add(new ArrayList<>(path));
            return;
        }
        
        for(int i = pos; i < s.length(); i++) {
            if(dp[pos][i]) {
                path.add(s.substring(pos,i+1));
                helper(res, path, dp, s, i+1);
                path.remove(path.size()-1);
            }
        }
    }
}
```

```java
public class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> res=new ArrayList<List<String>>();
        if(s.length()==0)return res;
        recur(res,new ArrayList<String>(),s);
        return res;
    }
    
    public void recur(List<List<String>> res,List<String> temp, String s){
        if(s.length()==0){
            res.add(new ArrayList<String>(temp));
            return;
        }
        for(int i=0;i<s.length();i++){
            if(isPalin(s.substring(0,i+1))){
                temp.add(s.substring(0,i+1));
                recur(res,temp,s.substring(i+1));
                temp.remove(temp.size()-1);
            }
        }
    }
    
    public boolean isPalin(String s){
        for(int i=0;i<s.length()/2;i++){
            if(s.charAt(i)!=s.charAt(s.length()-1-i))return false;
        }
        return true;
    }
}
```

## 46. Permutations

Given a collection of **distinct** integers, return all possible permutations.

**Example:**

```
Input: [1,2,3]
Output:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> list = new ArrayList<List<Integer>>();
        List<Integer> arr = new ArrayList<Integer>();
        rec(list, nums, arr);
        return list;
    }
    
    public void rec(List<List<Integer>> list, int[] nums, List<Integer> arr){
        if(arr.size() == nums.length){
            list.add(new ArrayList<>(arr));
            // list.add(arr);
            return;
        }  
        for(int i = 0; i<nums.length; i++){
            if(arr.contains(nums[i]))continue;
            arr.add(nums[i]);
            rec(list, nums, arr);
            arr.remove(arr.size()-1);
        }
    }
}
```

## 77. Combinations

Given two integers *n* and *k*, return all possible combinations of *k* numbers out of 1 ... *n*.

**Example:**

```
Input: n = 4, k = 2
Output:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

```java
class Solution {
    public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> lists = new ArrayList<List<Integer>>();
        List<Integer> list = new ArrayList<Integer>();
        rec(lists, list, 1, n, k);
        return lists;
    }
    public static void rec(List<List<Integer>> lists, List<Integer> list, int start, int n, int k){
        if(k == 0){
            lists.add(new ArrayList<Integer>(list));
            return;
        }
        for(int i = start; i <= n; i++){
            list.add(i);
            rec(lists, list, i+1, n, k-1);
            list.remove(list.size()-1);
        }
    } 
}
```

## 78. Subsets

Given a set of **distinct** integers, *nums*, return all possible subsets (the power set).

**Note:** The solution set must not contain duplicate subsets.

**Example:**

```
Input: nums = [1,2,3]
Output:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> lists = new ArrayList<List<Integer>>();
        List<Integer> list = new ArrayList<Integer>();
        rec(lists, list, nums, 0);
        return lists;
    }
    public static void rec(List<List<Integer>> lists, List<Integer> list, int[] nums, int start){
        lists.add(new ArrayList<Integer>(list));
        for(int i = start; i<nums.length; i++){
            list.add(nums[i]);
            rec(lists, list, nums, i+1);
            list.remove(list.size()-1);
        }
    }
}
```

## 90. Subsets II

Given a collection of integers that might contain duplicates, **nums**, return all possible subsets (the power set).

**Note:** The solution set must not contain duplicate subsets.

**Example:**

```
Input: [1,2,2]
Output:
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```

```java
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<List<Integer>> lists = new ArrayList<List<Integer>>();
        List<Integer> list = new ArrayList<Integer>();
        Arrays.sort(nums);
        rec(lists, list, nums, 0);
        return lists;
    }
    public static void rec(List<List<Integer>> lists, List<Integer> list, int[] nums, int start){
        if(!lists.contains(new ArrayList<Integer>(list)))
            lists.add(new ArrayList<Integer>(list));
        for(int i = start; i<nums.length; i++){
            list.add(nums[i]);
            rec(lists, list, nums, i+1);
            list.remove(list.size()-1);
        }
    }
}
```

## 79. Word Search

Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

**Example:**

```
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

Given word = "ABCCED", return true.
Given word = "SEE", return true.
Given word = "ABCB", return false.
```

```java
class Solution {
    public boolean exist(char[][] board, String word) {
        for(int i = 0; i<board.length; i++){
            for(int j = 0; j<board[0].length; j++){
                if(search(board, word, i, j, 0))
                    return true;
            }
        }
        return false;
    }
    public static boolean search(char[][] board, String word, int x, int y, int pos){
        int high = board.length;
        int width = board[0].length;
        
        if(x >= high || x < 0 || y >= width || y < 0)
            return false;
        if(pos == word.length()-1)
           return board[x][y] == word.charAt(pos);
        if(!(board[x][y] == word.charAt(pos)))
            return false;
        
        char save = board[x][y];
        board[x][y] = '1';
        boolean res =    
            search(board, word, x - 1, y, pos + 1) || 
            search(board, word, x, y - 1, pos + 1) ||
            search(board, word, x + 1, y, pos + 1) ||
            search(board, word, x, y + 1, pos + 1);
        board[x][y] = save;
        return res;
    }
}
```

# Dynamic Programming

## 70. Climbing Stairs

You are climbing a stair case. It takes *n* steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

**Note:** Given *n* will be a positive integer.

**Example 1:**

```
Input: 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```

**Example 2:**

```
Input: 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

```java
class Solution {
    public int climbStairs(int n) {
        if(n==1)return 1;
        if(n==2)return 2;
        return climbStairs(n-1)+climbStairs(n-2);
    }
}
```

递归实现

```java
class Solution {
    public int climbStairs(int n) {
        if(n==1)return 1;
        if(n==2)return 2;
        int[] tmp = new int[n];
        tmp[0]=1;
        tmp[1]=2;
        for(int i = 2; i<n; i++){
            tmp[i]=tmp[i-1]+tmp[i-2];
        }
        return tmp[n-1];
    }
}
```

动态规划实现

## **Knapsack Problem**

![dp0](<https://raw.githubusercontent.com/rexllz/leetcode-java-note/master/dp0.jpg>)

Greedy algorithm can't get the optimal solution

![dp1](<https://raw.githubusercontent.com/rexllz/leetcode-java-note/master/dp1.jpg>)

Recursive solution

```java
public static int maxbag(int[] w, int[] v, int index, int c){
        if(index < 0 || c <=0)return 0;
        int res = maxbag(w,v,index-1,c);
        if(c>=w[index])
            res = Math.max(res, v[index]+maxbag(w,v,index-1,c-w[index]));
        return res;
    }

    public static void main(String[] args) {
        int[] w = new int[]{1,2,5};
        int[] v = new int[]{4,5,5};
        int index = w.length;
        int max = maxbag(w,v,index-1,1);
        System.out.println(max);
    }
```

记忆化

```java
    private static int[][] memo;

    public static int maxbag(int[] w, int[] v, int index, int c){

        if(index < 0 || c <=0)return 0;
        if(memo[index][c]!=-1)return memo[index][c];
        int res = maxbag(w,v,index-1,c);
        if(c>=w[index])
            res = Math.max(res, v[index]+maxbag(w,v,index-1,c-w[index]));
        memo[index][c] = res;
        return res;
    }

    public static void main(String[] args) {
        int[] w = new int[]{1,2,5};
        int[] v = new int[]{4,5,5};
        int index = w.length;
        int c = 8;
        memo= new int[index][c+1];
        for (int i = 0; i<index; i++)
            for(int j = 0; j<c+1; j++)
                memo[i][j] = -1;
        int max = maxbag(w,v,index-1,c);
        System.out.println(max);
    }
```

动态规划

```java
public static void main(String[] args) {
        int[] w = new int[]{1,2,5};
        int[] v = new int[]{4,5,5};
        int index = w.length;
        int c = 8;
        int[][] memo= new int[index][c+1];

        for (int j = 0; j<=c; j++)
            memo[0][j] = j>=w[0] ? v[0] : 0;
        for (int i = 1; i<index; i++)
            for (int j = 0; j<=c; j++){
                memo[i][j] = memo[i-1][j];
                if(j>=w[i]) memo[i][j] = Math.max(memo[i][j],v[i]+memo[i-1][j-w[i]]);
            }
        System.out.println(memo[index-1][c]);
}
```

## 416. Partition Equal Subset Sum

Given a **non-empty** array containing **only positive integers**, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.

**Note:**

1. Each of the array element will not exceed 100.
2. The array size will not exceed 200.



**Example 1:**

```
Input: [1, 5, 11, 5]

Output: true

Explanation: The array can be partitioned as [1, 5, 5] and [11].
```



**Example 2:**

```
Input: [1, 2, 3, 5]

Output: false

Explanation: The array cannot be partitioned into equal sum subsets.
```

动态规划

```java
class Solution {
    public boolean canPartition(int[] nums) {
        
        int len = nums.length;
        int sum = 0;
        for(int i = 0; i<len; i++)sum += nums[i];
        if(sum%2!=0)return false;
        sum /= 2;
        
        boolean[][] memo = new boolean[len][sum+1];
        for(int j = 0; j<=sum; j++) memo[0][j] = (nums[0]==j ? true : false);
        for(int i = 1; i<len; i++)
            for(int j = 0; j<=sum; j++){
                memo[i][j] = memo[i-1][j];
                if(j>=nums[i])
                memo[i][j] = memo[i-1][j] || memo[i-1][j-nums[i]]; 
            }
        return memo[len-1][sum];       
    }
}
```

recursive

```java
class Solution {
    public boolean canPartition(int[] nums) {
        
        int len = nums.length;
        int sum = 0;
        for(int i = 0; i<len; i++)sum += nums[i];
        if(sum%2!=0)return false;
        sum /= 2;
        return asPart(nums, len-1, sum);
    }
    
    public boolean asPart(int[] nums,int index, int sum){
        if(sum==0)return true;
        if(sum<0)return false;
        if(index <= 0)return false;
        return 
            asPart(nums, index-1, sum) || asPart(nums, index-1, sum-nums[index]); 
    }    
}
```

recursive with record

```java
class Solution {
    private static int[][] memo;
    public boolean canPartition(int[] nums) {
        
        int len = nums.length;
        int sum = 0;
        for(int i = 0; i<len; i++)sum += nums[i];
        if(sum%2!=0)return false;
        sum /= 2;
        memo = new int[len][sum+1];
        for(int i = 0; i<len; i++)
            for(int j = 0; j<=sum; j++)
                memo[i][j]=-1;
        return asPart(nums, len-1, sum);
    }
    
    public boolean asPart(int[] nums,int index, int sum){
        if(sum==0)return true;
        if(sum<0)return false;
        if(index <= 0)return false;
        if(memo[index][sum]!=-1)return memo[index][sum]==1;
        memo[index][sum] = 
            asPart(nums,index-1,sum)||asPart(nums,index-1,sum-nums[index])?1:0;
        return memo[index][sum]==1; 
    }    
}
```

## 322. Coin Change

You are given coins of different denominations and a total amount of money *amount*. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return `-1`.

**Example 1:**

```
Input: coins = [1, 2, 5], amount = 11
Output: 3 
Explanation: 11 = 5 + 5 + 1
```

**Example 2:**

```
Input: coins = [2], amount = 3
Output: -1
```

**Note**:
You may assume that you have an infinite number of each kind of coin.

```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        int min = Integer.MAX_VALUE;
        int total = 1;
        int[] dp = new int[amount + 1];
        dp[0] = 0;
        while (total <= amount) {
            min = Integer.MAX_VALUE;
            for (int i = 0; i < coins.length; i++) {
	            int diff = total - coins[i];
	            if (diff > 0 && dp[diff] > 0 || diff == 0) {
	                min = Math.min(min, dp[diff] + 1);
	            }
            }
            dp[total++] = (min == Integer.MAX_VALUE ? -1 : min);
        }
        return dp[amount];
    }
}
```

总量和元素的内外循环，要看清界定条件，比如所有同一总量结果比较，或者所有同一元素结果比较。

## 300. Longest Increasing Subsequence

Given an unsorted array of integers, find the length of longest increasing subsequence.

**Example:**

```
Input: [10,9,2,5,3,7,101,18]
Output: 4 
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4. 
```

**Note:**

- There may be more than one LIS combination, it is only necessary for you to return the length.
- Your algorithm should run in O(*n2*) complexity.

**Follow up:** Could you improve it to O(*n* log *n*) time complexity?

```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        int len = nums.length;
        if(len<1)return 0;
        int[] dp = new int[len];
        for(int i = 0; i<len; i++)dp[i]=1;
        for(int i = 1; i<len; i++){
            for(int j = 0; j<i; j++){
                if(nums[i]>nums[j])dp[i]=Math.max(dp[j]+1,dp[i]);
            }
        }
        int max = 0;
        for(int x : dp)
            max = Math.max(max,x);
        return max;
    }
}
```

## 279. Perfect Squares

Given a positive integer *n*, find the least number of perfect square numbers (for example, `1, 4, 9, 16, ...`) which sum to *n*.

**Example 1:**

```
Input: n = 12
Output: 3 
Explanation: 12 = 4 + 4 + 4.
```

**Example 2:**

```
Input: n = 13
Output: 2
Explanation: 13 = 4 + 9.
```

```java
public class Solution {
    public int numSquares(int n) {
       int[] dp = new int[n + 1];
       Arrays.fill(dp, Integer.MAX_VALUE);
       dp[0] = 0;
       for(int i = 0; i <= n; i++){
           for(int j = 1; i + j * j <= n; j++){
               dp[i  + j * j] = Math.min(dp[i + j * j], dp[i] + 1);
            }
       }
       return dp[n];
    }
}
```

## 343. Integer Break

Given a positive integer *n*, break it into the sum of **at least** two positive integers and maximize the product of those integers. Return the maximum product you can get.

**Example 1:**

```
Input: 2
Output: 1
Explanation: 2 = 1 + 1, 1 × 1 = 1.
```

**Example 2:**

```
Input: 10
Output: 36
Explanation: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36.
```

**Note**: You may assume that *n* is not less than 2 and not larger than 58.

```java
class Solution {
    public int integerBreak(int n) {
        // return find(n);
        
        int[] dp = new int[n+1];
        dp[1] = 1;
        
        for(int i = 2; i<=n; i++){
            for(int j = 1; j<i; j++){
                dp[i] = Math.max(dp[i], j*dp[i-j]);
                dp[i] = Math.max(dp[i], j*(i-j));
            }
        }
        return dp[n];
    }
}
```

## 64. Minimum Path Sum

Given a *m* x *n* grid filled with non-negative numbers, find a path from top left to bottom right which *minimizes* the sum of all numbers along its path.

**Note:** You can only move either down or right at any point in time.

**Example:**

```
Input:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
Output: 7
Explanation: Because the path 1→3→1→1→1 minimizes the sum.
```

```java
class Solution {
    public int minPathSum(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;
        int[][] path = new int[m][n];
        path[0][0] = grid[0][0];
        for(int i = 1; i<n; i++)path[0][i] = path[0][i-1] + grid[0][i];
        for(int i = 1; i<m; i++)path[i][0] = path[i-1][0] + grid[i][0];
        for(int i = 1; i<m; i++){
            for(int j = 1; j<n; j++){
                path[i][j] = Math.min(path[i-1][j],path[i][j-1])+grid[i][j];
            }
        }
        return path[m-1][n-1];
    }
}
```

## 120. Triangle

Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

For example, given the following triangle

```
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
```

The minimum path sum from top to bottom is `11` (i.e., **2** + **3** + **5** + **1** = 11).

**Note:**

Bonus point if you are able to do this using only *O*(*n*) extra space, where *n* is the total number of rows in the triangle.

```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        int sum = 0;
        int len = triangle.size();
        int min = Integer.MAX_VALUE;;
        int[][] dp = new int[len][len];
        dp[0][0] = triangle.get(0).get(0);
        if(len==1)return dp[0][0];
        for(int i = 1; i<len; i++){
            for(int j = 0; j<triangle.get(i).size(); j++){
                if(j==0)dp[i][j]=dp[i-1][0]+triangle.get(i).get(0);
                else if(j==triangle.get(i).size()-1){
                    dp[i][j]=dp[i-1][triangle.get(i-1).size()-1]+triangle.get(i).get(triangle.get(i).size()-1);
                }else{
                    dp[i][j] = Math.min(dp[i-1][j],dp[i-1][j-1])+triangle.get(i).get(j);
                }
                if(i==len-1){
                min = Math.min(min, dp[i][j]);
                }
            }
        }
        return min;
    }
}
```

## 91. Decode Ways

A message containing letters from `A-Z` is being encoded to numbers using the following mapping:

```
'A' -> 1
'B' -> 2
...
'Z' -> 26
```

Given a **non-empty** string containing only digits, determine the total number of ways to decode it.

**Example 1:**

```
Input: "12"
Output: 2
Explanation: It could be decoded as "AB" (1 2) or "L" (12).
```

**Example 2:**

```
Input: "226"
Output: 3
Explanation: It could be decoded as "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).
```

```java
class Solution {
    public int numDecodings(String s) {
        // corner case, e.g. '022' returns 0
        if (s.charAt(0) == '0') {
            return 0;
        }
        
        int[] dp = new int[s.length()];
        dp[0] = 1;
        for (int i = 1; i < s.length(); i++) {
            int n = s.charAt(i) - '0';
            int pre = s.charAt(i - 1) - '0';
            /* current digit is from 1->9, then the current number of ways of decoding
            the message is at least the number of ways calculated until the previous one */
            if (n >= 1 && n <= 9) {
                dp[i] = dp[i - 1];
            }
            /*  check whether the adjacent two digits 
                are from 10 -> 26, including 10, 20, etc */
            if (pre != 0) {
                int twoDigit = Integer.parseInt(s.substring(i - 1, i + 1));
                if (twoDigit >= 1 && twoDigit <= 26) {
                    dp[i] = (i == 1) ? (dp[i] + 1) : (dp[i] + dp[i - 2]);
                }
            }
        }
        return dp[dp.length - 1];
    }
}
```

## 62. Unique Paths

A robot is located at the top-left corner of a *m* x *n* grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

![img](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)
Above is a 7 x 3 grid. How many possible unique paths are there?

**Note:** *m* and *n* will be at most 100.

**Example 1:**

```
Input: m = 3, n = 2
Output: 3
Explanation:
From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Right -> Down
2. Right -> Down -> Right
3. Down -> Right -> Right
```

**Example 2:**

```
Input: m = 7, n = 3
Output: 28
```

```java
class Solution {
    public int uniquePaths(int m, int n) {
        int[][] path = new int[m][n];
        path[0][0] = 1;
        for(int i = 1; i<m; i++){
            path[i][0] = path[i-1][0];
        }
        for(int i = 1; i<n; i++){
            path[0][i] = path[0][i-1];
        }
        for(int i = 1; i<m; i++){
            for(int j = 1; j<n; j++){
                path[i][j] = path[i-1][j] + path[i][j-1];
            }
        }
        return path[m-1][n-1];
    }
}
```

## 63. Unique Paths II

A robot is located at the top-left corner of a *m* x *n* grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

Now consider if some obstacles are added to the grids. How many unique paths would there be?

![img](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)

An obstacle and empty space is marked as `1` and `0` respectively in the grid.

**Note:** *m* and *n* will be at most 100.

**Example 1:**

```
Input:
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
Output: 2
Explanation:
There is one obstacle in the middle of the 3x3 grid above.
There are two ways to reach the bottom-right corner:
1. Right -> Right -> Down -> Down
2. Down -> Down -> Right -> Right
```

```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int m = obstacleGrid.length;
        int n = obstacleGrid[0].length;
        obstacleGrid[0][0]=(obstacleGrid[0][0]==1 ? 0 : 1);
        for(int i = 1; i<m; i++){
            obstacleGrid[i][0]=(obstacleGrid[i][0]==1 ? 0 : obstacleGrid[i-1][0]);
        }
        for(int i = 1; i<n; i++){
            obstacleGrid[0][i]=(obstacleGrid[0][i]==1 ? 0 : obstacleGrid[0][i-1]);
        }
        for(int i = 1; i<m; i++){
            for(int j = 1; j<n; j++){
                obstacleGrid[i][j]=(obstacleGrid[i][j]==1 ? 0 : obstacleGrid[i-1][j] + obstacleGrid[i][j-1]);
            }
        }
        return obstacleGrid[m-1][n-1];
    }
}
```



# Greedy Algorithm

## 455. Assign Cookies

Assume you are an awesome parent and want to give your children some cookies. But, you should give each child at most one cookie. Each child i has a greed factor gi, which is the minimum size of a cookie that the child will be content with; and each cookie j has a size sj. If sj >= gi, we can assign the cookie j to the child i, and the child i will be content. Your goal is to maximize the number of your content children and output the maximum number.

**Note:**
You may assume the greed factor is always positive. 
You cannot assign more than one cookie to one child.

**Example 1:**

```
Input: [1,2,3], [1,1]

Output: 1

Explanation: You have 3 children and 2 cookies. The greed factors of 3 children are 1, 2, 3. 
And even though you have 2 cookies, since their size is both 1, you could only make the child whose greed factor is 1 content.
You need to output 1.
```



**Example 2:**

```
Input: [1,2], [1,2,3]

Output: 2

Explanation: You have 2 children and 3 cookies. The greed factors of 2 children are 1, 2. 
You have 3 cookies and their sizes are big enough to gratify all of the children, 
You need to output 2.
```

```java
class Solution {
    public int findContentChildren(int[] g, int[] s) {
        int leng = g.length-1; //children
        int lens = s.length-1; //cookies
        Arrays.sort(g);
        Arrays.sort(s);
        int out = 0;
        while(lens>-1&&leng>-1){
            if(s[lens]>=g[leng]){
                lens--;
                out++;
                leng--;
            }
            else leng--;
        }
        return out;      
    }
}
```

## 435. Non-overlapping Intervals

Given a collection of intervals, find the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping.

**Note:**

1. You may assume the interval's end point is always bigger than its start point.
2. Intervals like [1,2] and [2,3] have borders "touching" but they don't overlap each other.



**Example 1:**

```
Input: [ [1,2], [2,3], [3,4], [1,3] ]

Output: 1

Explanation: [1,3] can be removed and the rest of intervals are non-overlapping.
```



**Example 2:**

```
Input: [ [1,2], [1,2], [1,2] ]

Output: 2

Explanation: You need to remove two [1,2] to make the rest of intervals non-overlapping.
```



**Example 3:**

```
Input: [ [1,2], [2,3] ]

Output: 0

Explanation: You don't need to remove any of the intervals since they're already non-overlapping.
```

DP：

```java
/**
 * Definition for an interval.
 * public class Interval {
 *     int start;
 *     int end;
 *     Interval() { start = 0; end = 0; }
 *     Interval(int s, int e) { start = s; end = e; }
 * }
 */
class Solution {
    public int eraseOverlapIntervals(Interval[] intervals) {
        if(intervals.length<=1)return 0;
        Arrays.sort(intervals, new Comparator<Interval>() {
            @Override
            public int compare(Interval o1, Interval o2) {
                if(o1.start != o2.start)
                return o1.start - o2.start;
                return o1.end - o2.end;
            }
        });
        int[] dp = new int[intervals.length];
        for(int i = 0; i<dp.length; i++) dp[i]=1;
        for(int i = 1; i<intervals.length; i++){
            for(int j = 0; j<i; j++){
                if(intervals[i].start>=intervals[j].end)
                    dp[i] = Math.max(dp[j]+1,dp[i]);
            }
        }
        int max = 0;
        for(int x : dp)max = Math.max(max,x);
        return intervals.length-max;          
    }
}
```

Greedy 

```java
public class Solution {
    public int eraseOverlapIntervals(Interval[] intervals) {
        if(intervals.length <= 0) return 0;
        Arrays.sort(intervals, (Interval a,Interval b) -> a.end - b.end);
        int border = intervals[0].end;
        int erase = 0;
        for(int i = 1; i < intervals.length; i++) {
            if(intervals[i].start < border) erase++;
            else {
                border = intervals[i].end;
            }
        }
        return erase;
    }
}
```















