---
title:  Leetcode#15 三数之和
date: 2020-02-06 12:28:34
cover_img: https://res.cloudinary.com/dmqrfncz7/image/upload/v1579533135/timg_1_o6pkuf.jpg
feature_img:
description:
keywords: leetcode,搜索
tags: leetcode
categories: leetcode
---

# 15.三数之和

## 题目
给定一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？找出所有满足条件且不重复的三元组。

注意：答案中不可以包含重复的三元组。

示例：
```
给定数组 nums = [-1, 0, 1, 2, -1, -4]，

满足要求的三元组集合为：
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```
## 题解
这题最大的问题是容易超时。显而易见的解法是利用三重循环枚举所有位置，并利用hash表等判断是否有重复，但不幸的是这个方法会遇到超时问题。

重新分析问题，若三数之和为0，即a+b+c=0，则必有大于0和小于0的数字。由此可见一种可行的方法是：
- 从小到大排数数组
- 指针i枚举所有小于0的数，并且该数之前没出现过
- 指针left从i+1开始递增，指针right从数组末尾开始递减，当两者重合时结束当前i位置的搜索
    - 判断i,left,right位置的和是否为0，如果大于0，则right位置减1，否则left位置加1

代码如下：
```
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) 
    {
        vector<vector<int>> result;
        int left,right;
        if(nums.empty() || nums.size()<2)
            return result;

        sort(nums.begin(),nums.end());
        
        
        for(int i=0;i<nums.size()-2;i++)
        {
            if(nums[i]>0)
                break;
            if(i>0 && nums[i-1]==nums[i])
                continue;
            left=i+1;
            right=nums.size()-1;
            while(left<right)
            {
                if(nums[i]+nums[left]+nums[right]==0)
                {
                    result.push_back({nums[i],nums[left],nums[right]});
                    while(left<right && nums[left]==nums[left+1])
                        left++;
                    while(left<right && nums[right]==nums[right-1])
                        right--;
                    left++;
                    right--;
                }
                else
                {
                    if(nums[left]+nums[right]+nums[i]<0)
                        left++;
                    else
                        right--;
                }
            }
        }
        return result;
    }
};
```