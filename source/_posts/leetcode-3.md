---
title: Leetcode#3 无重复字符的最长子串
date: 2020-02-02 14:04:54
cover_img: https://res.cloudinary.com/dmqrfncz7/image/upload/v1579533135/timg_1_o6pkuf.jpg
feature_img:
description:
keywords: leetcode,字符串
tags: leetcode
categories: leetcode
---


# 3.无重复字符的最长子串

## 题目
给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。
示例 1:
```
输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```
示例 2:
```
输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```
示例 3:
```
输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```


## 题解

用时：4ms
[start,end-1]的滑窗是检测的子串，每次将end指向的字符加入字串，并判断有无重复，若有重复的，则将start移动到重复字符后一位。
```
class Solution {
public:
    
    int lengthOfLongestSubstring(string s) {
        vector<int> mask(128,-1);    //存储字符出现的位置
        int start=-1,maxLength=0;
        
        for(int end=0;end<s.size();end++)
        {
            if(mask[s[end]]>=start)    //end端新加入的字符在[start，end-1]出现过
            {
                start=mask[s[end]]+1;  //将起始端跳转到重复字符后一位
            }
            mask[s[end]]=end;  
            maxLength=max(maxLength,end-start+1);
        }
        return maxLength;
    }
};
```