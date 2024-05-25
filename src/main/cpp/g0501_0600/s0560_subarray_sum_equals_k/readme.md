[![](https://img.shields.io/github/stars/LeetCode-in-Cpp/LeetCode-in-Cpp?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Cpp/LeetCode-in-Cpp)
[![](https://img.shields.io/github/forks/LeetCode-in-Cpp/LeetCode-in-Cpp?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Cpp/LeetCode-in-Cpp/fork)

## 560\. Subarray Sum Equals K

Medium

Given an array of integers `nums` and an integer `k`, return _the total number of continuous subarrays whose sum equals to `k`_.

**Example 1:**

**Input:** nums = [1,1,1], k = 2

**Output:** 2 

**Example 2:**

**Input:** nums = [1,2,3], k = 3

**Output:** 2 

**Constraints:**

*   <code>1 <= nums.length <= 2 * 10<sup>4</sup></code>
*   `-1000 <= nums[i] <= 1000`
*   <code>-10<sup>7</sup> <= k <= 10<sup>7</sup></code>

## Solution

```cpp
#include <vector>
#include <unordered_map>

class Solution {
public:
    int subarraySum(std::vector<int>& nums, int k) {
        int tempSum = 0;
        int ret = 0;
        std::unordered_map<int, int> sumCount;
        sumCount[0] = 1;
        
        for (int num : nums) {
            tempSum += num;
            if (sumCount.find(tempSum - k) != sumCount.end()) {
                ret += sumCount[tempSum - k];
            }
            if (sumCount.find(tempSum) != sumCount.end()) {
                sumCount[tempSum]++;
            } else {
                sumCount[tempSum] = 1;
            }
        }
        return ret;
    }
};
```