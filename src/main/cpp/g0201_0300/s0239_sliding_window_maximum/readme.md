[![](https://img.shields.io/github/stars/LeetCode-in-Cpp/LeetCode-in-Cpp?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Cpp/LeetCode-in-Cpp)
[![](https://img.shields.io/github/forks/LeetCode-in-Cpp/LeetCode-in-Cpp?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Cpp/LeetCode-in-Cpp/fork)

## 239\. Sliding Window Maximum

Hard

You are given an array of integers `nums`, there is a sliding window of size `k` which is moving from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position.

Return _the max sliding window_.

**Example 1:**

**Input:** nums = [1,3,-1,-3,5,3,6,7], k = 3

**Output:** [3,3,5,5,6,7]

**Explanation:**

    Window position        Max
    ---------------       -----
    [1 3 -1] -3 5 3 6 7     3
    1 [3 -1 -3] 5 3 6 7     3
    1 3 [-1 -3 5] 3 6 7     5
    1 3 -1 [-3 5 3] 6 7     5
    1 3 -1 -3 [5 3 6] 7     6
    1 3 -1 -3 5 [3 6 7]     7 

**Example 2:**

**Input:** nums = [1], k = 1

**Output:** [1] 

**Example 3:**

**Input:** nums = [1,-1], k = 1

**Output:** [1,-1] 

**Example 4:**

**Input:** nums = [9,11], k = 2

**Output:** [11] 

**Example 5:**

**Input:** nums = [4,-2], k = 2

**Output:** [4] 

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>5</sup></code>
*   <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>
*   `1 <= k <= nums.length`

## Solution

```cpp
#include <vector>
#include <deque>

class Solution {
public:
    std::vector<int> maxSlidingWindow(std::vector<int>& nums, int k) {
        int n = nums.size();
        std::vector<int> res(n - k + 1);
        int x = 0;
        std::deque<int> dq;
        int i = 0;
        int j = 0;
        while (j < nums.size()) {
            while (!dq.empty() && dq.back() < nums[j]) {
                dq.pop_back();
            }
            dq.push_back(nums[j]);
            if (j - i + 1 == k) {
                res[x] = dq.front();
                ++x;
                if (dq.front() == nums[i]) {
                    dq.pop_front();
                }
                ++i;
            }
            ++j;
        }
        return res;
    }
};
```