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

# 