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







