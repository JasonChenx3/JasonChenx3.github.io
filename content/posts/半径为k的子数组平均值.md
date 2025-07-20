+++
date = '2025-07-20T17:23:12+08:00'
title = '半径为k的子数组平均值'
tags = ["定长滑动窗口"]
categories = ["算法"]
+++

原题链接：[半径为k的子数组平均值](https://leetcode.cn/problems/k-radius-subarray-averages/description/)

先将 $ans$ 数组全部赋值为 $-1$ ，然后再根据滑动窗口求出平均值。

```cpp
typedef long long LL;
class Solution {
public:
    vector<int> getAverages(vector<int>& nums, int k) {
        int n = nums.size();
        vector<int> ans(n, -1);  // 提前赋值
        LL sum = 0;
        int m = 2 * k + 1;  // 窗口大小
        for (int i = 0; i < n; i ++ ) {
            sum += nums[i];
            if (i < m - 1) {
                continue;
            }
            ans[i - k] = sum / m;
            sum -= nums[i - m + 1];
        }
        return ans;
    }
};
```
