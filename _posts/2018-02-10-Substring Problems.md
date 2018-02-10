---
layout: post  
title: 编程算法 Substring Problem
subtitle: 
header-img: "img/seagulls.jpg"
categories: [blog ]  
tags: [leetcode]
description: 「Leetcode 解题思路」  
---  




##### 76. Minimum Window Substring

Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).

For example,
**S** = `"ADOBECODEBANC"`
**T** = `"ABC"`

Minimum window is `"BANC"`.

**Note:**
If there is no such window in S that covers all characters in T, return the empty string `""`.

If there are multiple such windows, you are guaranteed that there will always be only one unique minimum window in S.



思路：

首先：需要的variables包括 int map, rnum (number of char still in need), minStart and minLenth

然后：用 for loop来go through each char

在For loop里面，先update int map和rnum，然后用while loop找以此为end的最小start点。

```
class Solution {
    public String minWindow(String s, String t) {
        if(s == null || t == null) return "";
        int[] map = new int[256];
        for(char c:t.toCharArray())map[c]++;
        int minStart=0, minLen=Integer.MAX_VALUE;
        int start = 0, rnum = t.length();
        for(int end = 0; end < s.length(); end++){
            char right = s.charAt(end);
            if(map[right]>0)rnum--;
            map[right]--;
            while(rnum==0){
                if(end-start+1<minLen){
                    minLen = end-start+1;
                    minStart = start;
                }
                char left = s.charAt(start);
                map[left]++;
                if(map[left]>0)rnum++;
                start++;
            }
        }
        return (minLen == Integer.MAX_VALUE)?"":s.substring(minStart, minStart+minLen);
    }
}
```





##### Now the template

```
public String findSubstring(String s){
  int[] map = new int[256];
  for()map[c]++; //initialize map
  int counter;
  int start,end,minStart,minLen;
  for(改右边){
    update map and counter
    while(改左边){
      update mins
      update map and counter
    }
  }return;
}
```



##### 159. Longest Substring with At Most Two Distinct Characters

Given a string, find the length of the longest substring T that contains at most 2 distinct characters.

For example, Given s = `“eceba”`,

T is "ece" which its length is 3.

```
class Solution {
    public int lengthOfLongestSubstringTwoDistinct(String s) {
        int[] map = new int[256];
        int start = 0, numChar = 0, maxLen = 0;
        for(int i = 0; i < s.length(); i++){
            if(map[s.charAt(i)]==0)numChar++;
            map[s.charAt(i)]++;
            while(start >= 0 && numChar > 2){
                if(map[s.charAt(start)]==1)numChar--;
                map[s.charAt(start)]--;
                start++;
            }
            maxLen = Math.max(maxLen,i-start+1);
        }
        return maxLen;
    }
}
```

Another solution without int[] map.

```
int lengthOfLongestSubstringTwoDistinct(string s) {
        int i = 0, j = -1;
        int maxLen = 0;
        for (int k = 1; k < s.size(); k++) {
            if (s[k] == s[k-1]) continue;
            if (j > -1 && s[k] != s[j]) {
                maxLen = max(maxLen, k - i);
                i = j + 1;
            }
            j = k - 1;
        }
        return maxLen > (s.size() - i) ? maxLen : s.size() - i;
  }
```



##### 3. Longest Substring Without Repeating Characters

Given a string, find the length of the **longest substring** without repeating characters.

**Examples:**

Given `"abcabcbb"`, the answer is `"abc"`, which the length is 3.

Given `"bbbbb"`, the answer is `"b"`, with the length of 1.

Given `"pwwkew"`, the answer is `"wke"`, with the length of 3. Note that the answer must be a **substring**, `"pwke"` is a *subsequence*and not a substring.

注意细节啊，int map也可以用hashset替换

```
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int[] map = new int[256];
        int maxLen = 0, start = 0;
        for(int i = 0; i < s.length(); i++){
            map[s.charAt(i)]++;
            if(map[s.charAt(i)]>1){
                maxLen = Math.max(maxLen, i-start);
                while(map[s.charAt(i)]>1){
                    map[s.charAt(start)]--;
                    start++;
                }
            }
        }
        return Math.max(maxLen, s.length()-start);
    }
}
```

