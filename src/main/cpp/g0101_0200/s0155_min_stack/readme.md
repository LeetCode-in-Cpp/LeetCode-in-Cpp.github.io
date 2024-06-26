[![](https://img.shields.io/github/stars/LeetCode-in-Cpp/LeetCode-in-Cpp?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Cpp/LeetCode-in-Cpp)
[![](https://img.shields.io/github/forks/LeetCode-in-Cpp/LeetCode-in-Cpp?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Cpp/LeetCode-in-Cpp/fork)

## 155\. Min Stack

Easy

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the `MinStack` class:

*   `MinStack()` initializes the stack object.
*   `void push(int val)` pushes the element `val` onto the stack.
*   `void pop()` removes the element on the top of the stack.
*   `int top()` gets the top element of the stack.
*   `int getMin()` retrieves the minimum element in the stack.

**Example 1:**

**Input**

    ["MinStack","push","push","push","getMin","pop","top","getMin"]
    [[],[-2],[0],[-3],[],[],[],[]]

**Output:** [null,null,null,null,-3,null,0,-2]

**Explanation:**

    MinStack minStack = new MinStack();
    minStack.push(-2);
    minStack.push(0);
    minStack.push(-3);
    minStack.getMin(); // return -3
    minStack.pop();
    minStack.top(); // return 0
    minStack.getMin(); // return -2 

**Constraints:**

*   <code>-2<sup>31</sup> <= val <= 2<sup>31</sup> - 1</code>
*   Methods `pop`, `top` and `getMin` operations will always be called on **non-empty** stacks.
*   At most <code>3 * 10<sup>4</sup></code> calls will be made to `push`, `pop`, `top`, and `getMin`.

## Solution

```cpp
#include <stack>
#include <algorithm>

class MinStack {
private:
    struct Node {
        int min;
        int data;
        Node* nextNode;
        Node* previousNode;

        Node(int min, int data, Node* previousNode, Node* nextNode)
            : min(min), data(data), previousNode(previousNode), nextNode(nextNode) {}
    };

    Node* currentNode;

public:
    MinStack() : currentNode(nullptr) {}

    void push(int val) {
        if (currentNode == nullptr) {
            currentNode = new Node(val, val, nullptr, nullptr);
        } else {
            currentNode->nextNode = new Node(std::min(currentNode->min, val), val, currentNode, nullptr);
            currentNode = currentNode->nextNode;
        }
    }

    void pop() {
        if (currentNode != nullptr) {
            currentNode = currentNode->previousNode;
        }
    }

    int top() {
        if (currentNode != nullptr) {
            return currentNode->data;
        }
        return -1;
    }

    int getMin() {
        if (currentNode != nullptr) {
            return currentNode->min;
        }
        return -1;
    }

    ~MinStack() {
        while (currentNode != nullptr) {
            Node* temp = currentNode;
            currentNode = currentNode->previousNode;
            delete temp;
        }
    }
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(val);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->getMin();
 */
```