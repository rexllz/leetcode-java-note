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

# 