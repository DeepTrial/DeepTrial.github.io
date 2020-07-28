---
title: Leetcode#53 最大子序和
date: 2020-01-20 19:42:28
cover_img: https://res.cloudinary.com/dmqrfncz7/image/upload/v1579533135/timg_1_o6pkuf.jpg
categories: leetcode
tags: leetcode
description: 动态规划,分治算法
keywords: 子序和, 复杂度，分治算法
---
# 53 最大子序和

## 题目描述
>给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。
>
>示例:
>
>输入: [-2,1,-3,4,-1,2,1,-5,4],
>
>输出: 6
>
>解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
>
>进阶:
>如果你已经实现复杂度为 O(n) 的解法，尝试使用更为精妙的分治法求解。

## 分析
抛开时间限制，最简单的方法就是使用双重循环，分别枚举起止位置，计算累加和，判断是否为最大值并保存。

考虑到时间限制为O(n)时，以上的方法就行不通了，下面介绍几种不通的方法：

### Kadane算法
此算法是美国卡耐基梅隆大学的教授Kadane发明的，是一种用于求解最大连续子序列和问题的最优算法。对于一个长度为n的数组A而言，从A[0] 到 A[j] 是一个子数组（j < n），那么以A[j]结尾的子数组之最大和，要么是 A[j]， 要么是 max(A[i]~A[j-1])+A[j] ，其中0 ≤ i ≤ j-1。这就是该算法设计的出发点。

```
class Solution {
	public:
    
    int maxSubArray(vector<int>& nums) {
        
        vector<int>::iterator it  = nums.begin();
        int maxSum = *it;
        int theSum = *it;
        
        for(it = it+1 ; it != nums.end(); it++){
            theSum = max(theSum + *it, *it);
            
            if(theSum > maxSum)
                maxSum = theSum;
        }
        
        return maxSum;
    }
};
```

从此想法中，我们可以更近一部得到推论，当A[i-1]<0时，A[i]不变，当A[i-1]>0时，A[i]=A[i]+A[i-1]。因为累加和为负数时，只会减小当前值，所以直接抛弃，当之前的累加和为正数时，会加大当前值，则继续累加。

代码如下:

```
class Solution(object):
    def maxSubArray(self, nums):
    """
    :type nums: List[int]
    :rtype: int
    """
        for i in range(1, len(nums)):  
            if nums[i-1] > 0:  
                nums[i] += nums[i-1]  
        return max(nums)
```

### 分治算法
假设数组下标有效范围是l到r,将数组分为左半部分下标为（l，mid-1）和右半部分下标为(mid+1，r)以及中间元素下标为mid，接下来递归求出左半部分的最大子序和：left=helper(nums,l,mid-1); 右半部分最大子序和right=helper(nums,mid+1,r);

接下来再将左半部分右边界，右半部分左边界以及中间元素nums[mid]整合，用了两个循环，先整合左半部分右边界和中间值，再将整合结果与右半部分左边界整合得到整合以后的最大子序和max_num，最后返回max_num，left,right的最大值即是要求的最大子序和。


```
class Solution {
public:
    int maxSubArray(vector<int>& nums) {  
        return divide(nums, 0, nums.size()-1);
    }  
    
    int divide(vector<int>& nums, int l, int r) {
        if(l == r)  return nums[l];
        if(l == r-1) return max(nums[l], max(nums[r], nums[l]+nums[r]));
        
        int mid = (l+r)>>1;
        int lret = divide(nums, l, mid-1);
        int rret = divide(nums, mid+1, r);
        
        int mret = nums[mid];
        int sum = mret;
        for(int i = mid-1; i >= l ; i --) {
            sum += nums[i];
            mret = max(mret, sum);
        }
        sum = mret;    //保存已经计算过的左边的最大子序和
        for(int i = mid+1; i <= r ; i ++) {
            sum += nums[i];
            mret = max(mret, sum);
        }
        
        return max(lret, max(rret, mret));
    }
};
```

