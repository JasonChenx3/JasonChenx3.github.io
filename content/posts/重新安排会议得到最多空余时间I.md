+++
date = '2025-07-22T22:36:42+08:00'
title = '重新安排会议得到最多空余时间I'
tags = ["定长滑动窗口"]
categories = ["算法"]
+++

一、计算出所有空余时间段

空余时间段可以为 $0$ 。

中间有 $n - 1$ 个空余时间段，最左边和最右边各有一个空余时间段。

空余时间段总数为 $n + 1$ 。

二、等效操作

移动会议的操作等价于合并相邻的空余时间段，移动 $i$ 次，等价于合并 $i + 1$ 个空余时间段。

问题转化为定长滑动窗口问题，窗口大小为 $k + 1$ 。

证明：假设我们已经找到了最优的移动方式，并且获得了最大的空闲区间 $I$ 。如果存在某次移动与剩余 $k - 1$ 次移动的会议并不连续，那么这次移动并不会对 $I$ 有任何贡献；此时，我们可以将这次移动更换为移动与剩余 $k - 1$ 次移动相邻的会议，那么更换后的移动一定会让 $I$ 增大，这与我们一开始的最优假设矛盾。所以一定是连续移动 $k$ 个会议最优。

```cpp
class Solution {
public:
    int maxFreeTime(int eventTime, int k, vector<int>& startTime, vector<int>& endTime) {
        vector<int> nums;
        int n = startTime.size();
        int ans = 0;
        int sum = 0;
        nums.push_back(startTime[0]);
        for (int i = 1; i < n; i ++ ) {
            nums.push_back(startTime[i] - endTime[i - 1]);
        }
        nums.push_back(eventTime - endTime[n - 1]);
        int m = nums.size();
        k ++ ;
        for (int i = 0; i < m; i ++ ) {
            sum += nums[i];
            if (i < k - 1) {
                continue;
            }
            ans = max(sum, ans);
            sum -= nums[i - k + 1];
        }
        return ans;
    }
};
```
