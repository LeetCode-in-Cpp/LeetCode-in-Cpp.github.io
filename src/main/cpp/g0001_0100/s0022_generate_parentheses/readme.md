[![](https://img.shields.io/github/stars/LeetCode-in-Cpp/LeetCode-in-Cpp?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Cpp/LeetCode-in-Cpp)
[![](https://img.shields.io/github/forks/LeetCode-in-Cpp/LeetCode-in-Cpp?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Cpp/LeetCode-in-Cpp/fork)

## 22\. Generate Parentheses

Medium

Given `n` pairs of parentheses, write a function to _generate all combinations of well-formed parentheses_.

**Example 1:**

**Input:** n = 3

**Output:** ["((()))","(()())","(())()","()(())","()()()"] 

**Example 2:**

**Input:** n = 1

**Output:** ["()"] 

**Constraints:**

*   `1 <= n <= 8`



## Solution

```cpp
#include <vector>
#include <string>

using namespace std;

class Solution {
public:
    vector<string> generateParenthesis(int n) {
        vector<string> ans;
        string current;
        generate(current, ans, n, n);
        return ans;
    }

private:
    void generate(string& current, vector<string>& ans, int open, int close) {
        if (open == 0 && close == 0) {
            ans.push_back(current);
            return;
        }
        if (open > 0) {
            current.push_back('(');
            generate(current, ans, open - 1, close);
            current.pop_back();
        }
        if (close > 0 && open < close) {
            current.push_back(')');
            generate(current, ans, open, close - 1);
            current.pop_back();
        }
    }
};
```