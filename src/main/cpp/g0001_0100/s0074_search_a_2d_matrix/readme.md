[![](https://img.shields.io/github/stars/LeetCode-in-Cpp/LeetCode-in-Cpp?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Cpp/LeetCode-in-Cpp)
[![](https://img.shields.io/github/forks/LeetCode-in-Cpp/LeetCode-in-Cpp?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Cpp/LeetCode-in-Cpp/fork)

## 74\. Search a 2D Matrix

Medium

Write an efficient algorithm that searches for a value in an `m x n` matrix. This matrix has the following properties:

*   Integers in each row are sorted from left to right.
*   The first integer of each row is greater than the last integer of the previous row.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/05/mat.jpg)

**Input:** matrix = \[\[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3

**Output:** true 

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/10/05/mat2.jpg)

**Input:** matrix = \[\[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13

**Output:** false 

**Constraints:**

*   `m == matrix.length`
*   `n == matrix[i].length`
*   `1 <= m, n <= 100`
*   <code>-10<sup>4</sup> <= matrix[i][j], target <= 10<sup>4</sup></code>

## Solution

```cpp
#include <vector>

class Solution {
public:
    bool searchMatrix(const std::vector<std::vector<int>>& matrix, int target) {
        int endRow = matrix.size();
        int endCol = matrix[0].size();
        int targetRow = 0;
        bool result = false;

        for (int i = 0; i < endRow; i++) {
            if (matrix[i][endCol - 1] >= target) {
                targetRow = i;
                break;
            }
        }

        for (int i = 0; i < endCol; i++) {
            if (matrix[targetRow][i] == target) {
                result = true;
                break;
            }
        }

        return result;
    }
};
```