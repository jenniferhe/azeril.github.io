---
layout: post  
title: 编程算法 Tree
subtitle: 
header-img: "img/seagulls.jpg"
categories: [blog ]  
tags: [leetcode]
description: 「Leetcode 解题思路」  
---  

1. **Full and complete** **tree**: All leaves are at the bottom of the tree and all non-lef nodes have exactly two children. It has 2^n-1 nodes exactly.
2. Be able to do in-order, post-order and pre-order traversal
3. Running time of operations on trees
4. **Tries**
5. Graph traversal: BFS, DFS



例题

#### 104. Maximum Depth of Binary Tree

Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node. VERY SIMPLE

```
class Solution {
    public int maxDepth(TreeNode root) {
        if(root == null)return 0;
        return 1+Math.max(maxDepth(root.left),maxDepth(root.right));
    }
}
```



#### 173. Binary Search Tree Iterator

mplement an iterator over a binary search tree (BST). Your iterator will be initialized with the root node of a BST.

Calling `next()` will return the next smallest number in the BST.

**Note: **`next()` and `hasNext()` should run in average O(1) time and uses O(*h*) memory, where *h* is the height of the tree.

思路：从小到大output的意思也就是left-mid-right travesal

```
public class BSTIterator {
    private Stack<TreeNode> stack = new Stack<TreeNode>();
    public BSTIterator(TreeNode root) {
        pushAll(root);
    }

    /** @return whether we have a next smallest number */
    public boolean hasNext() {
        return !stack.isEmpty();
    }

    /** @return the next smallest number */
    public int next() {
        TreeNode tmp = stack.pop();
        pushAll(tmp.right);
        return tmp.val;
    }
    private void pushAll(TreeNode node) {//Only push the left nodes
        for (; node != null; stack.push(node), node = node.left);
    }
}
```





#### 617. Merge Two Binary Trees

Given two binary trees and imagine that when you put one of them to cover the other, some nodes of the two trees are overlapped while the others are not.

You need to merge them into a new binary tree. The merge rule is that if two nodes overlap, then sum node values up as the new value of the merged node. Otherwise, the NOT null node will be used as the node of new tree.

**Example 1:**

```
Input: 
	Tree 1                     Tree 2                  
          1                         2                             
         / \                       / \                            
        3   2                     1   3                        
       /                           \   \                      
      5                             4   7                  
Output: 
Merged tree:
	     3
	    / \
	   4   5
	  / \   \ 
	 5   4   7

```

**Note:** The merging process must start from the root nodes of both trees.



思路：没啥说的就recursion

```
class Solution {
    public TreeNode mergeTrees(TreeNode t1, TreeNode t2) {
        if(t1 == null && t2 == null)return null;
        int val = ((t1==null)?0:t1.val )+((t2==null)?0:t2.val);
        TreeNode tmp = new TreeNode(val);
        tmp.left = mergeTrees((t1==null)?null:t1.left, (t2==null)?null:t2.left);
        tmp.right = mergeTrees((t1==null)?null:t1.right,(t2==null)?null:t2.right);
        return tmp;
    }
}
```



#### 110. Balanced Binary Tree

```
Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.
```



```
class Solution {
    public boolean isBalanced(TreeNode root) {
        return getDepth(root)!=-1;
    }
    private int getDepth(TreeNode root){
        if(root == null)return 0;
        int lh = getDepth(root.left);
        int rh = getDepth(root.right);
        if(lh == -1 || rh == -1 || lh - rh > 1 || rh - lh > 1)return -1;
        return Math.max(lh,rh)+1;
    }
}
```





#### 108. Convert Sorted Array to Binary Search Tree

思路：关键在于如何设置recursion case

用i,j表示起点和终点，mid point就是（i+j）/2.

注：终点inclusive和exclusive都可以的，区别只在于在偶数个数的时候，选取的是中点左侧的数。

inclusive的话 stop case就是i>j，exclusive的话stop case就是i==j.

另外要注意几个stop cases

```
class Solution {
    public TreeNode sortedArrayToBST(int[] nums) {
        if(nums == null || nums.length==0)return null;
        return helper(nums,0,nums.length-1);
    }
    private TreeNode helper(int[] nums, int i, int j){
        if(i>j)return null;
        int mid = (i+j)/2;
        TreeNode node = new TreeNode(nums[mid]);
        node.left = helper(nums,i,mid-1);
        node.right = helper(nums,mid+1,j);
        return node;
    }
}
```



#### 124. Binary Tree Maximum Path Sum

Given a binary tree, find the maximum path sum.

For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain **at least one node** and does not need to go through the root.

For example:
Given the below binary tree,

```
       1
      / \
     2   3

```

Return `6`.



思路很巧妙：

需要的helper method是计算当前node单向的depth，然后在每个node 停留的时候update一下经过此点的max值。即dfs go through nodes, at each nodes, calculate both max and one way depth.

```
class Solution {
    int max = Integer.MIN_VALUE;
    public int maxPathSum(TreeNode root) {
        if(root == null )return 0;
        helper(root);
        return max;
    }
    private int helper(TreeNode root){
        if(root == null)return 0;
        int left = Math.max(0, helper(root.left));
        int right = Math.max(0,helper(root.right));
        max = Math.max(root.val+left+right,max);
        return root.val + Math.max(left, right);
    }
}
```





#### 105. Construct Binary Tree from Preorder and Inorder Traversal

思路：给定pre和in order的两个array怎样建立tree。

pre 是 root left right顺序，in order是left root right顺序，先考虑手工计算如何算

STEP 1: pre的0号位是Root，然后在inorder中找到root element所在位置，其左侧是所有left nodes，右侧是所有right nodes

STEP 2: pre中同样大小的部分是left nodes，然后是right nodes 分别 recursive run就好了

所以这个题的要点是 1.找到recursion的variables 2. 找到recursion correct values

需要的variables包括pre order的start(表示 root)，in order的start 和 end，还有两个array

注：容易忽略的是，pre order的start针对left nodes就是简单的 pre++，针对right nodes是pre + (left node size) +1.

```
class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        return helper(preorder,inorder,0,0,inorder.length);
    }
    private TreeNode helper(int[] pre, int[] in, int preIndex, int i, int j){
        if(preIndex>pre.length-1 || i >= j || i == -1)return null;
        TreeNode root = new TreeNode(pre[preIndex]);
        System.out.println("Current node contains " + pre[preIndex]);
        int mid = -1;
        for(int tmp = i; tmp < j; tmp++){
            if(in[tmp]==pre[preIndex])mid = tmp;
        }
        root.left = helper(pre,in,preIndex+1,i,mid);
        root.right = helper(pre,in,preIndex+mid-i+1,mid+1,j);
        return root;
    }
}
```



#### 99. Recover Binary Search Tree

把tree中两个异位的elements 换过来

思路：建立一个travese method把两个异位数找出来。

此时用in order travesal，当prev > curr则prev 设为异位值1

再当prev > curr则把curr设为异位值2

通过travesal可以把tree想成一个increasing array中间有两个位置错的，第一个是前一个比现在这个大的话那么前一个有问题，第二个是，前一个比当前大的话，后一个有问题。

```
class Solution {
    TreeNode first,second;
    TreeNode prev = new TreeNode(Integer.MIN_VALUE);
    public void recoverTree(TreeNode root) {
        traverse(root);
        int tmp = first.val;
        first.val = second.val;
        second.val = tmp;
    }
    private void traverse(TreeNode root){
        if(root==null)return;
        traverse(root.left);
        if(first == null && prev.val>=root.val)first = prev;
        if(first != null && prev.val>=root.val)second = root;
        prev = root;
        traverse(root.right);
    }
}
```







总结一下：

关键点：travesal, recursion, iterator, 配用stack更方便哟~