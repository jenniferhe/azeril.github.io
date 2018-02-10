---
layout: post  
title: 编程思路 Backtracking
subtitle: 
header-img: "img/seagulls.jpg"
categories: [blog ]  
tags: [leetcode]
description: 「Leetcode 解题思路」  
---  


#### 46. Permutation 

Basic structure goes: 

add helper method called backtrack:

if the size is full, add it to res; else, in a for loop add the value that is not in the set, then call backtrack and call remove.

##### NO.1 NO DUPLICATES (46)

```
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        backtrack(res,new ArrayList<Integer>(), nums);
        return res;
    }
    private void backtrack(List<List<Integer>> res, List<Integer> tmp, int[] nums){
        if(tmp.size()==nums.length)res.add(new ArrayList<Integer>(tmp));
        else{
            for(int i : nums){
                if(tmp.contains(i))continue;
                tmp.add(i);
                backtrack(res,tmp,nums);
                tmp.remove(tmp.size()-1);
            }
        }
    }
}
```

##### NO2. Duplicates (47)

```
class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        Arrays.sort(nums);
        backtrack(res, new ArrayList<Integer>(),nums,new boolean[nums.length]);
        return res;
    }
    private void backtrack(List<List<Integer>> res, List<Integer> tmp, int[] nums, boolean[] used){
        if(tmp.size()==nums.length)res.add(new ArrayList<Integer>(tmp));
        else{
            for(int i = 0; i < nums.length; i++){
                if(used[i] || (i>0 && nums[i] == nums[i-1] && used[i-1]))continue;
                used[i] = true;
                tmp.add(nums[i]);
                backtrack(res, tmp, nums,used);
                tmp.remove(tmp.size()-1);
                used[i] = false;
            }
        }
    }
}
```



##### 31. Next Permutation

思路：consider **1**32**2** -> **21**23变换的应该是加粗位

1. **Swap** i 和 j 位的数，i位表示nums[i]<nums[i+1], j位表示，从右往左第一个nums[i]<nums[j];
2. **Reverse** i 位后所有数

```
class Solution {
    public void nextPermutation(int[] nums) {
        if(nums == null || nums.length < 2)return;
        int i = nums.length-2;
        while(i>=0 && nums[i]>=nums[i+1])i--;
        if(i>=0){
            for(int j = nums.length-1; j > i; j--){
                if(nums[j]>nums[i]){
                    swap(nums,i,j);
                    break;
                }
            }
        }
        reverse(nums,i+1, nums.length-1);
    }
    private void swap(int[] nums, int i, int j){
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
    private void reverse(int[] nums, int i, int j){
        while(i<j)swap(nums,i++,j--);
    }
}
```



##### 267. Palindrome Permutation II

Given a string `s`, return all the palindromic permutations (without duplicates) of it. Return an empty list if no palindromic permutation could be form.

For example:

Given `s = "aabb"`, return `["abba", "baab"]`.

Given `s = "abc"`, return `[]`.



思路：backtrack，此题data structure要用int[256] 

### 一定要重做！因为之前总是有小错

```
class Solution {
    public List<String> generatePalindromes(String s) {
        List<String> res = new ArrayList<String>();
        int[] hash = new int[256];
        for(char c : s.toCharArray())hash[c]++;
        boolean flag = false;
        String mid = "";
        for(int i = 0; i < 256; i++){
            if(flag && hash[i]%2 == 1)return res;
            if(hash[i]%2 == 1){
                flag = true;
                mid = "" + (char)i;
            }
            hash[i]/=2;
        }
        backtrack(res, hash, s.length(), mid, new StringBuffer());
        return res;
    }
    private void backtrack(List<String> res, int[] hash, int length, String mid, StringBuffer sb){
        if(sb.length() == length/2){
            res.add(sb.toString() + mid + sb.reverse().toString());
            sb.reverse();
        }else{
            for(int i = 0; i < hash.length; i++){
                if(hash[i]>0){
                    hash[i]--;
                    sb.append((char)i);
                    backtrack(res, hash, length, mid, sb);
                    sb.deleteCharAt(sb.length()-1);
                    hash[i]++;
                }
            }
        }
    }
}
```

 

##### 39. Combination Sum

bug free 啊啊啊

```
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> res = new ArrayList<>();
        Arrays.sort(candidates);
        backtrack(res,new ArrayList<Integer>(),target,candidates);
        return res;
    }
    
    private void backtrack(List<List<Integer>> res, List<Integer> tmp, int target, int[] nums){
        if(target < 0)return;
        if(target == 0)res.add(new ArrayList<Integer>(tmp));
        else{
            for(int i = 0; i < nums.length; i++){
                if(tmp.size() > 0 && nums[i]<tmp.get(tmp.size()-1))continue;
                tmp.add(nums[i]);
                backtrack(res,tmp,target-nums[i],nums);
                tmp.remove(tmp.size()-1);
            }
        }
    }
}
```

##### 40. Combination sum II

Given a collection of candidate numbers (**C**) and a target number (**T**), find all unique combinations in **C** where the candidate numbers sums to **T**.

Each number in **C** may only be used **once** in the combination.

**Note:**

- All numbers (including target) will be positive integers.
- The solution set must not contain duplicate combinations.

For example, given candidate set `[10, 1, 2, 7, 6, 1, 5]` and target `8`, 
A solution set is: 

```
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
```

BUG FREE!!! 注意点：sort，skip duplicate, remove的时候remove的是index

```
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> res = new ArrayList<>();
        Arrays.sort(candidates);
        backtrack(res, new ArrayList<Integer>(), candidates, target, 0);
        return res;
    }
    
    private void backtrack(List<List<Integer>> res, List<Integer> tmp, int[] nums, int target, int curIndex){
        if(target < 0)return;
        if(target == 0)res.add(new ArrayList<Integer>(tmp));
        else{
            for(int i = curIndex; i < nums.length; i++){
                if(i > curIndex && nums[i] == nums[i-1])continue;
                tmp.add(nums[i]);
                backtrack(res,tmp,nums,target-nums[i],i+1);
                tmp.remove(tmp.size()-1);
            }
        }
    }
}
```

##### 77. Combination

Given two integers *n* and *k*, return all possible combinations of *k* numbers out of 1 ... *n*.

For example,
If *n* = 4 and *k* = 2, a solution is:

```
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

```
class Solution {
    public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> res = new ArrayList<>();
        backtrack(res, new ArrayList<Integer>(), 0,n,k);
        return res;
    }
    private void backtrack(List<List<Integer>> res, List<Integer> tmp, int cur, int n, int k){
        if(k==0)res.add(new ArrayList<Integer>(tmp));
        else{
            for(int i = cur; i < n; i++){
                tmp.add(i+1);
                backtrack(res, tmp, i+1, n, k-1);
                tmp.remove(tmp.size()-1);
            }
        }
    }
}
```



##### 78. Subsets

Given a set of **distinct** integers, *nums*, return all possible subsets.

**Note:** The solution set must not contain duplicate subsets.

For example,
If **nums** = `[1,2,3]`, a solution is:

```
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



BUG FREE!注意这个要加上empty sets所以always adds current。而不用if else

```
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        backtrack(res, new ArrayList<Integer>(), nums, 0);
        return res;
    }
    private void backtrack(List<List<Integer>> res, List<Integer> tmp, int[] nums, int index){
        res.add(new ArrayList<Integer>(tmp));
        for(int i = index; i < nums.length; i++){
            tmp.add(nums[i]);
            backtrack(res, tmp, nums, i+1);
            tmp.remove(tmp.size()-1);
        }
    }
}
```



##### 90 Subsets II

Given a collection of integers that might contain duplicates, **nums**, return all possible subsets.

**Note:** The solution set must not contain duplicate subsets.

For example,
If **nums** = `[1,2,2]`, a solution is:

```
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```



```
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        Arrays.sort(nums);
        backtrack(res, new ArrayList<Integer>(), nums, 0);
        return res;
    }
    private void backtrack(List<List<Integer>> res, List<Integer> tmp, int[] nums, int index){
        res.add(new ArrayList<Integer>(tmp));
        for(int i = index; i < nums.length; i++){
            if(i > index && nums[i] == nums[i-1])continue;
            tmp.add(nums[i]);
            backtrack(res, tmp, nums, i+1);
            tmp.remove(tmp.size()-1);
        }
    }
}
```

