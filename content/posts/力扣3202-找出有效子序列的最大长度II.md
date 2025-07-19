+++
date = '2025-07-18T09:01:43+08:00'
title = '找出有效子序列的最大长度II'
tags = ["动态规划"]
categories = ["算法"]
+++
观察发现，`sub` 数组的奇数位置的数字模 `k` 同余，偶数位置的数字模 `k` 同余。

`dp[i][j]` 表示 `sub` 数组中以 `i` 和 `j` 结尾的最大数组长度。

假设当前遍历到 `num` ，此时 `dp[pre][num] = dp[num][pre] + 1`，`pre` 是模 `k` 的所有余数，通过遍历获取。

```cpp
class Solution {
public:
    int maximumLength(vector<int>& nums, int k) {
        vector<vector<int>> dp(k, vector<int>(k, 0));
        int ans = 0;
        for (int num : nums) {
            num %= k;
            for (int pre = 0; pre < k; pre ++ ) {
                dp[pre][num] = dp[num][pre] + 1;
                ans = max(ans, dp[pre][num]);
            }
        }
        return ans;
    }
};
```
