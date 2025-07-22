+++
date = '2025-07-22T23:21:44+08:00'
title = '最少交换次数来组合所有的1II'
tags = ["定长滑动窗口"]
categories = ["算法"]
+++

枚举所有连续 $1$ 可能出现的区间，转换为定长滑动窗口问题，窗口大小为 $nums$ 中 $1$ 的数量。

需要特判当 $1$ 的数量为 $0$ 时，答案为 $0$ 。

```cpp
class Solution {
public:
    int minSwaps(vector<int>& nums) {
        // 只有 0 和 1 可以求一下和得到 1 的数量
        int k = accumulate(nums.begin(), nums.end(), 0);  
        int n = nums.size();
        int ans = 1e9;
        int sum = 0;
        if (k == 0) {
            return 0;
        }
        for (int i = 0; i < 2 * n; i ++ ) {
            int in = i % n;
            sum += (nums[in] == 0);
            if (i < k - 1) {
                continue;
            }
            ans = min(ans, sum);
            int out = (i - k + 1) % n;
            sum -= (nums[out] == 0);
        }
        return ans;
    }
};
```
