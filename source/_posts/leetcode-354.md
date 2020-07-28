---
title: Leetcode#354 俄罗斯套娃信封问题
date: 2020-02-17 17:13:25
cover_img: https://res.cloudinary.com/dmqrfncz7/image/upload/v1579533135/timg_1_o6pkuf.jpg
feature_img:
description:
keywords:
tags: leetcode
---

# 354 俄罗斯套娃信封问题

## 题目描述

给定一些标记了宽度和高度的信封，宽度和高度以整数对形式 (w, h) 出现。当另一个信封的宽度和高度都比这个信封大的时候，这个信封就可以放进另一个信封里，如同俄罗斯套娃一样。

请计算最多能有多少个信封能组成一组“俄罗斯套娃”信封（即可以把一个信封放到另一个信封里面）。

说明:
不允许旋转信封。

示例:

>输入: envelopes = [[5,4],[6,4],[6,7],[2,3]]
>
>输出: 3 
>
>解释: 最多信封的个数为 3, 组合为: [2,3] => [5,4] => [6,7]。

## 分析
这是一道典型的动态规划题目，假设信封大小（w，h），因为不能旋转，所以只需w之间比较，h之间比较。若我们先按照w递增的顺序排列，再从h的序列中寻找最长上升子序列，则此序列长度就是答案。可以看出，我们将这个问题转换成为了求最长上升子序列的问题。

## 代码
```
class Solution {
public:
    static bool cmpEnvelope(vector<int> &a, vector<int> &b) {
        if(a[0] != b[0]) {
            return a[0] < b[0];
        } else if (a[1] != b[1]) {
            return a[1] > b[1];
        }
        return 0;
    }
    int maxEnvelopes(vector<vector<int>>& envelopes) {
        // 先排序
        int size = envelopes.size();
        if (size <= 1) {
            return size;
        }
        sort(envelopes.begin(), envelopes.end(), cmpEnvelope);
        vector<int> dp(size, 1);
        int maxEnv = 1;
        for (int k = 0; k < size; ++k) {
            for (int i = 0; i < k; ++i) {
                if (envelopes[k][1] > envelopes[i][1]) {
                    dp[k] = max(dp[k], dp[i] + 1);
                }
            }
            if (dp[k] > maxEnv) {
                maxEnv = dp[k];
            }
        }
        return maxEnv;
    }

};
```