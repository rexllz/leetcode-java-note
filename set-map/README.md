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

# 