---
layout: post
title: LeetCode At Hand (3sum-closest)
categories: [LeetCode,手边算法]
description: LeetCode刷题笔记
keywords: 3sum, 三数相加, Medium
---

### 1.问题描述

Given an array `nums` of *n* integers and an integer `target`, find three integers in `nums` such that the sum is closest to `target`. Return the sum of the three integers. You may assume that each input would have exactly one solution.

**Example:**

```
Given array nums = [-1, 2, 1, -4], and target = 1.

The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```

## 2.解题思路

#### 2.1 快速归类：

+ 数据结构：考察对数组知识的掌握程度；数组结构的相关问题主要考察如何高效遍历数组，需要重点关注任务的初始化条件和边界条件。
+ 任务类型：属于"遍历搜索类型”；

#### 2.2 问题抽象重建：

+ 该题可以抽象理解为:提供一种算法，使得从给定整数集合中寻找任意三个元素的非重复子集，该子集的元素的和与目标的值的欧式距离尽可能小。
+ 问题的关键点在于如何快速寻找符合要求的子集

#### 2.3 思路：

+ 暴力搜寻：对数组进行三重循环，最外层固定第一个元素，内层双重循环遍历所有的二元组组合,从而寻找所有可能的非重复子集。算法时间复杂度是$O(n^3)​$
+ 启发式搜索：暴力搜寻的高复杂度在于内层循环的$O(n^2)​$复杂度，仔细思考发现如果数组是有序(非严格递增或非严格递减)的，那么可以用双游标启发式的寻找最优解，复杂度降为$O(n)​$,那么遍历搜索任务的复杂度为$O(n^2)​$,考虑到数组排序算法的复杂度$O(n)-O(n^2)​$,那么整体的复杂度为$O(n^2)​$

#### 2.4 证明：

+ 假设数组nums是单调不减的,数组长度为n,目标值为target,此时第一个元素为nums[i];那么在一次内层循环中,建立下界游标 $l​$ 和上界游标$r​$使得,$l=nums[0]​$，$r=nums[n-1]​$,可以计算子集的和$sum=nums[i]+nums[l]+nums[r]​$
+ 此时要将$sum$和$target$进行比较,若  $\|sum-target\|_2$减少则用当前子集替换为当前最优子集，否则:
  + 当$sum<target$时,需要启发式的增加$sum$以逼近$target$,由于数组是单调不减的，若$nums[l+1]$存在,那么$nums[l+1]>=nums[l]$从而只需右移下届游标即可实现。
  + 当$sum>target​$是,同理需要减少$sum​$以逼近$target​$，通过移动上界游标$r​$
  + 上下界游标相遇时$(l>=r)​$内层循环结束,此时内层循环复杂度仅为$O(n)​$

### 3.解法

#### 3.1 排序+搜索


```java
class Solution{
public static int threeSumClosest(int[] nums, int target) {
        int res = Integer.MAX_VALUE;
        Arrays.sort(nums);
        for (int i = 0; i < nums.length - 2; i++) {
            if (i == 0 || (i > 0 && nums[i - 1] != nums[i])) {
                int l = i + 1, r = nums.length - 1;
                while (l < r) {
                    int tmp = nums[l] + nums[r] + nums[i] - target;
                    if (Math.abs(tmp) < Math.abs(res)) res = tmp;
                    if (tmp < 0) l++;
                    else r--;
                }
            }
        }
        return res + target;
    }
}
```

#### 3.2 暴力搜索

略

### 3.参考资料

+ [3sum问题的$O(n^2)$时间复杂度解法](https://leetcode.com/problems/3sum/discuss/7380/Concise-O(N2)-Java-solution)

+ [3Sum-closest问题LeetCode传送门](https://leetcode.com/problems/3sum-closest/)