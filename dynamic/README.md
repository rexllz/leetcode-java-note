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

## 198. House Robber

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police**.

**Example 1:**

```
Input: [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
```

**Example 2:**

```
Input: [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
             Total amount you can rob = 2 + 9 + 1 = 12.
```

```java
class Solution {
    public int rob(int[] nums) {
        int len = nums.length;
        if(len==0)return 0;
        if(len==1)return nums[0];
        int[] dp = new int[len];
        dp[0] = nums[0];
        dp[1] = Math.max(nums[0], nums[1]);
        for(int i = 2; i<len; i++){
            dp[i] = Math.max(dp[i-1], dp[i-2]+nums[i]);
        }
        return dp[len-1];
    }
}
```

# 