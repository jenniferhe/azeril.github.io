---
layout: post  
title: 编程思路 Dynamic Programming
subtitle: 
header-img: "img/seagulls.jpg"
categories: [blog ]  
tags: [leetcode]
description: 「Leetcode 解题思路」  
---  


- Typically applied to optimization problems
- Steps
  - Characterize the structure of an optimal solution
  - Recursively define the value of an optimal solution
  - Compute the value of an optimal solution in a bottom-up fashion
  - Construct an optimal solution from computed info
- 例题



#### 276. Paint Fence

There is a fence with n posts, each post can be painted with one of the k colors.

You have to paint all the posts such that no more than two adjacent fence posts have the same color.

Return the total number of ways you can paint the fence.

**Note:**
n and k are non-negative integers.

思路：dp1[] 存与前者一样的，dp2[]存与前者不同的

```
class Solution {
    public int numWays(int n, int k) {
        if(k<1||n==0)return 0;
        if(n==1)return k;
        int[] same = new int[n];
        int[] diff = new int[n];
        same[0] = same[1] = k;
        diff[0] = k;
        diff[1] = k*(k-1);
        for(int i = 2; i < n; i++){
            same[i] = diff[i-1];
            diff[i] = (diff[i-1]+same[i-1])*(k-1);
        }
        return same[n-1]+diff[n-1];
    }
}
```



#### 265. Paint House II

There are a row of *n* houses, each house can be painted with one of the *k* colors. The cost of painting each house with a certain color is different. You have to paint all the houses such that no two adjacent houses have the same color.

The cost of painting each house with a certain color is represented by a `*n* x *k*` cost matrix. For example, `costs[0][0]` is the cost of painting house 0 with color 0; `costs[1][2]` is the cost of painting house 1 with color 2, and so on... Find the minimum cost to paint all houses.

这道题的解法真的很精妙：

DP思路，go through n个房子，每次update 该房色的cost += prev cost

prev cost有两种选择，若curr color不是上一个房子的min cost color则update其为prev min cost；不然则update其为prev 2nd min cost。

于是，需要的variable包括，prev min cost color和prev 2nd min cost color 和 current min cost color 和 current 2nd min cost color

而DP很多时候初始行set up总容易出问题，此时可以先设定prev min color啥的都为-1，然后在update的时候用个if 命令分割出这种可能性防止出现int[-1]这样的情况。

```
class Solution {
    public int minCostII(int[][] costs) {
        if(costs == null || costs.length == 0 || costs[0].length == 0) return 0;
        int n = costs.length, k = costs[0].length;
        int p1,p2,m1=-1,m2=-1;
        for(int i = 0; i < n; i++){
            p1=m1;p2=m2;m1=-1;m2=-1;
            for(int j = 0; j < k; j++){
                if(j==p1)costs[i][j]+=(i==0)?0:costs[i-1][p2];
                else costs[i][j]+=(i==0)?0:costs[i-1][p1];
                if(m1 <0 || costs[i][j]<costs[i][m1]){
                    m2=m1;m1=j;
                }else if(m2<0||costs[i][j]<costs[i][m2])
                    m2=j;
            }
        }
        return costs[n-1][m1];
    }
}
```



#### 120. Triangle

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

The minimum path sum from top to bottom is `11` (i.e., 2 + 3 + 5 + 1 = 11).

思路很巧妙：从下往上traverse。此题就是先填满第一行再move up

```
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        if(triangle==null||triangle.size()==0||triangle.get(0).size()==0)return 0;
        int[] dp = new int[triangle.size()];
        for(int i = 0; i < triangle.size();i++)dp[i]=triangle.get(triangle.size()-1).get(i);
        for(int i = triangle.size()-1; i>0; i--){//curr level
            for(int j = 0; j < i; j++){//curr element in the level
                dp[j] = Math.min(dp[j], dp[j+1])+triangle.get(i-1).get(j);
            }
        }
        return dp[0];
    }
}
```



#### 139. Word Break

Given a **non-empty** string *s* and a dictionary *wordDict* containing a list of **non-empty** words, determine if *s* can be segmented into a space-separated sequence of one or more dictionary words. You may assume the dictionary does not contain duplicate words.

For example, given
*s* = `"leetcode"`,
*dict* = `["leet", "code"]`.

Return true because `"leetcode"` can be segmented as `"leet code"`.

**UPDATE (2017/1/4):**
The *wordDict* parameter had been changed to a list of strings (instead of a set of strings). Please reload the code definition to get the latest changes.



```
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        boolean[] dp = new boolean[s.length()+1];
        dp[0] = true;
        for(int i = 1; i <= s.length(); i++){
            for(int j = 0; j < i; j++){
                if(dp[j]&&wordDict.contains(s.substring(j,i))){
                    dp[i]=true;
                    break;
                }
            }
        }
        return dp[s.length()];
    }
}
```





#### 152. Maximum Product Subarray

Find the contiguous subarray within an array (containing at least one number) which has the largest product.

For example, given the array `[2,3,-2,4]`,
the contiguous subarray `[2,3]` has the largest product = `6`.



很简单的题，只要思路对了的话。

这个题的key point是如何处理负数。我想到了这个关键却没有想到对的处理方法。

最好的处理方法是，同时keep track current min和current max，遇到负数时swap min和max再update。

```
class Solution {
    public int maxProduct(int[] nums) { 
        int max = nums[0];
        int min = nums[0];
        int res = max;
        for(int i = 1; i < nums.length; i++){
            if(nums[i]<0){
                int tmp = max;
                max = min;
                min = tmp;
            }
            max = Math.max(max*nums[i],nums[i]);
            min = Math.min(min*nums[i],nums[i]);
            res = Math.max(max, res);
        }
        return res;
    }
}
```



#### 322. Coin Change

You are given coins of different denominations and a total amount of money *amount*. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return `-1`.

**Example 1:**
coins = `[1, 2, 5]`, amount = `11`
return `3` (11 = 5 + 5 + 1)

**Example 2:**
coins = `[2]`, amount = `3`
return `-1`.

**Note**:
You may assume that you have an infinite number of each kind of coin.



思路：bottom up dynamic programming

用两个for loop循环，外层表示从1到target amount的每个value

内层表示从1到第n个coin value

中间用一个if statement即 如果当前target amount 比内层coin value大且二者之差got a valid solution，则update dp[current target amount]。

```
class Solution {
    public int coinChange(int[] coins, int amount) {
        int[] dp = new int[amount];
        int INF = Integer.MAX_VALUE;
        for(int i = 1; i < dp.length; i++){
          dp[i]=INF;
          for(int j = 0; j < coins.length; j++){
            if(i>coins[j] && dp[i-coins[j]]!=INF)
            	dp[i]=Math.min(dp[i],dp[i-coins[j]]+1);
          }
        }
        return (dp[amount]==INF)?-1:dp[amount];
    }
}
```





#### 91. Decode Ways

A message containing letters from `A-Z` is being encoded to numbers using the following mapping:

```
'A' -> 1
'B' -> 2
...
'Z' -> 26

```

Given an encoded message containing digits, determine the total number of ways to decode it.

For example,
Given encoded message `"12"`, it could be decoded as `"AB"` (1 2) or `"L"` (12).

The number of ways decoding `"12"` is 2.

思路：

DP，重点在于考虑清楚情况：

1. current char == 0
2. two char =< 26 && two char >= 9注意 >= 9 的部分很容易忘记啊

```
class Solution {
    public int numDecodings(String s) {
        if(s == null || s.length() == 0 || s.charAt(0) == '0')return 0;
        int[] dp = new int[s.length()+1];
        dp[0] = 1;
        dp[1] = s.charAt(0) !='0'?1:0;
        for(int i = 1; i< s.length(); i++){
            if(s.charAt(i)!='0')dp[i+1]+=dp[i];
            int x = Integer.parseInt(s.substring(i-1,i+1));
            if(27-x>0 && x-9>0)dp[i+1]+=dp[i-1];
        }
        return dp[s.length()];
    }
}
```







稍微总结一下：



大体来说，遇到optimization的题可以考虑DP。

最简单的方法是直接update existing variable，也可以重建一个dp map。注意initial value是否合理。

ran through for loop的时候记得考虑清楚if statement



void dp(array of some input){

1. 建立dp
2. for loop
3. if statement update dp
4. return dp[n]

}

下次再更新记得把题整理一下