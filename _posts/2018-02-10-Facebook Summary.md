---
layout: post  
title: 面试总结 Facebook Summary
subtitle: 
header-img: "img/seagulls.jpg"
categories: [blog ]  
tags: [leetcode]
description: 「Leetcode 解题思路」  
---  



- LC13 - Roman to Int: 关键在于如何判断当前该加还是减。 

  ​					for1 string -> int, for 2: +=sum

- LC15 -  3 sum 2 pointer + a while loop outside, remember to sort

- LC17. Letter Combinations of a Phone Number: LinkedList 用来当Queue

- LC23 Merge K sorted list - 变体 iterator

  此题先想到priorityqueue with modified comparator. Time complexity是O(nlogk)

  也可Merge sort思路 helper method merge 2 lists every time 是O(nklogn)

- LC28 - impement strStr()

- LC29 - Divide 2 Integers - bit manipulation

  Preprocess ： make positive

  while loop 左移divisor到头，res += <<同样位数。update dividend。再循环直到dividend < divisor

- LC31 - Next Permutation: Ex. 1322 -> 2123

- LC33 - Search in Rotated Sorted Array: Binary Search, edge case

- LC43 - 右往左 第i位x第j位 res 存在第i+j和i+j+1位

- LC46,47 -Permutation - Backtrack

- LC49 - Group Anagrams: 先sort 再hashmap查找；prime number

- LC56 - Merge Intervals - 分别sort先

- LC65 - Valid Number - Set booleans up front and run through by for loop with list of if statements

- LC67 - Add Binary

- LC71 - Simplify path Stack + HashSet

- LC75 - Sort Colors - 2 Pointers 大约只需4line code但很容易出错 *

- LC76 - Min Window Substring - Substring类题 注意细节

- LC91 - Decode ways DP

- LC93 - Restore IP Address -  3 nested for loop

- LC98 - **Tree Question** https://leetcode.com/problems/validate-binary-search-tree/discuss/

- LC102 - Binary Tree Level Order Traversal - DFS or Queue

- LC106 Construct Binary Tree from Inorder and Postorder Travesal

- LC114 - Flatten Binary Tree to LinkedList 

- LC125 - Two Pointer

- LC133 - Clone Graph HashMap 存 label -> node

- LC138 - Copy List with Random Pointer - 易有小错

- LC139,**140** **Word Break** DP DFS with a hashmap (s -> linkedlist) 

  ​						return that linkedlist

- LC146 LRU Cache - DLinkedListNode

- LC158 - Read 4K  Outside of loop create a char[] a

- LC173 - Binary Search Tree Iterator Nothing Tricky, use stack + left traversal

- LC189 - Rotate Array remember to convert k to a pivot index

- LC191 - Number of 1 Bits - Bit Manipulation

   - >>>和>>的区别是unsign和sign，然后 if的condition是n!=0而不是n>0

- LC200 - Number of Islands - BFS

- LC202 - Happy Number

- LC203 - Remove LinkedList Elements

- LC211 Add and Search Word - Data Structure Tree with Node[26] child

- LC227 Basic Calculator II For loop + stack pop in */

- LC230 - Kth Smallest Element in a BST - Tree Iterator, Binary Search

- LC 252, 253 Meeting Rooms **253 Meeting rooms II** priorityQueue to sort all intervals and then for loop to add

- LC257 Binary Tree Paths

- LC266 Palindrome Permutation - HashSet add then remove

- **LC273 - Integer to English Words**

  - 0-9; 10- 19; 20-90
  - helper() check below 10,20,100,1000,1000000,1000000000 and call helper recursively

- LC277 - Find Celebrity 2 Pass first to find celebrity, second to make sure it does not know anyone

- LC278 - First Bad Version - Get to middle and subdivide, while loop inclusive

- **LC297** - Serialize and Deserialize Binary Tree - In order traversal with X representing NULL

  - 要求序列化输出 list，那么就不能用字符形式表达空节点。确认了下树每个数值范围有限，面试官说INT_MAX可以用

- **LC301 Remove invalid parentheses** DFS (res, s, index, stringbuilder, numl,numr,open )

- LC304 Range Sum Query DP

- **LC311 Sparse Matrix Multiplication** array[] or hashmap

- **LC314** Binary Tree Vertical Order traversal

- LC348 Design Tic-tac-toe +1-1

- LC350





- Behavior Questions List
- 标黑题目要会做
- 回顾+写总结 ie Stack, Queue的methods





BQ：

- Linkedin Internship:

  With Linkedin Marketing Solution, Ads API.

  Maintain Ads Database and support internal and external use of ads related data

  Team - > profit making

  My role was to implement a private logging system that can record personal identifiable info

  - Design phase: elasticsearch, couchbase, oracle database, security
    - Acquire large amount of info in a short period
  - Implemention phase: school projects tiny sizes VS the real big sizes
  - Distributed System/Hadoop

- Richmond research:

  - Detect bird spiece based on image of it
  - SVM, CNN

- Nacho Operating Ssytem

- Why not linkedin? 1. Project harder than expected (security,mentor change) 2. Team not looking for new grad 3. I myself is not perfect

Where were you this summer? 

- Want to learn more so I was studyinging and traveling
- Illness

Why Facebook?

- Best place for engineering
- Culture and feeling: young exciting challenging move fast
- Instagram



- What team? Ads, Payment, Distributed System
- What question do you have for me?
  - Do you like working at fb and what part do you like the most?



- use english version
- ask, then write
- Edge cases



culture; transparency, openness 