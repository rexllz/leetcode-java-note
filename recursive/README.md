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

# 