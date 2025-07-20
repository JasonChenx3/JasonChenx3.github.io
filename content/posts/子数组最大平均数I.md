+++
date = '2025-07-20T15:56:01+08:00'
title = '子数组最大平均数I'
tags = ["定长滑动窗口"]
categories = ["算法"]
+++

原题链接：[子数组最大平均数I](https://leetcode.cn/problems/maximum-average-subarray-i/description/)

滑动窗口维护序列和。

```cpp
class Solution {
public:
    double findMaxAverage(vector<int>& nums, int k) {
       double mx_sum = -1e18, sum = 0;
       int n = nums.size();
       for (int i = 0; i < n; i ++ ) {
        sum += nums[i];
        if (i < k - 1) {
            continue;
        }
        mx_sum = max(mx_sum, sum);
        sum -= nums[i - k + 1];
       }
       return mx_sum / k;
    }
};
```
