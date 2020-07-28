---
title: Leetcode#143 环状链表II
date: 2020-02-13 12:15:42
cover_img: https://res.cloudinary.com/dmqrfncz7/image/upload/v1579533135/timg_1_o6pkuf.jpg
categories: leetcode
description: leetcode
keywords: leetcode 链表 指针
tags: leetcode
---

# 143 环状链表II

## 题目描述

给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。

为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。

说明：不允许修改给定的链表。

示例1:

>输入：head = [3,2,0,-4], pos = 1
>
>输出：tail connects to node index 1
>
>解释：链表中有一个环，其尾部连接到第二个节点。

![avatar](./1.jpg)

示例 2：

>输入：head = [1,2], pos = 0
>
>输出：tail connects to node index 0
>
>解释：链表中有一个环，其尾部连接到第一个节点。

![avatar](./2.jpg)

示例 3：

>输入：head = [1], pos = -1
>
>输出：no cycle
>
>解释：链表中没有环。

![avatar](./3.jpg)


## 分析

利用快慢指针来解这道题，快指针的速度为2，慢指针的速度为1.

在示例1中，快慢指针第一次在-4点相遇，快指针走的路径6是慢指针3的二倍，即长度3->2->0->-4->2->0->-4是长度3-2-0->-4的二倍，也就是说-4->2->0->-4的长度（即一圈的长度）等于3-2-0->-4的长度，将两个长度同时减掉2-0->-4，则-4->2的长度等于3->2的长度。

所以在第一次相遇后，我们只需要将慢指针的起点指定为head的起点，快指针的位置不变(-4)，并且将快慢指针的速度都设置为1，那么下次相遇的点就是圆环的起点（2）。

## 代码
```
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode* slow=head,*fast=head;
        while(fast&&fast->next)
        {
            slow=slow->next;
            fast=fast->next->next;
            if(slow==fast) break;
        }
        if(!fast||!fast->next) return NULL;
        slow=head;
        while(fast!=slow)
        {
            slow=slow->next;
            fast=fast->next;
        }
        return slow;
    }
};
```