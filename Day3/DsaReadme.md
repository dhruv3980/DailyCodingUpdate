# 📘 Day 3 - DSA Notes

## ✅ Problems Solved
1. **LeetCode 84: Largest Rectangle in Histogram**
2. **LeetCode 155: Min Stack**

---

## 🔹 LeetCode 84: Largest Rectangle in Histogram

### Problem:
Given an array representing heights of bars in a histogram, find the area of the largest rectangle that can be formed.

---

### Approach:
- Use a **monotonic increasing stack**:
  - Traverse the array from both left → right and right → left.
  - For each index, find the nearest smaller element on the left and on the right.
  - Width = `rightSmaller[i] - leftSmaller[i] - 1`
  - Area = `heights[i] * width`
- Time Complexity: **O(n)**








---

### Code:
```cpp
class Solution {
public:
  int largestRectangleArea(vector<int>& heights) {
      int n = heights.size();
      vector<int> rightsmaller(n), leftsmaller(n);
      stack<int> s;

      // Right smaller
      for (int i = n - 1; i >= 0; i--) {
          while (!s.empty() && heights[s.top()] >= heights[i]) s.pop();
          rightsmaller[i] = s.empty() ? n : s.top();
          s.push(i);
      }

      while (!s.empty()) s.pop();

      // Left smaller
      for (int i = 0; i < n; i++) {
          while (!s.empty() && heights[s.top()] >= heights[i]) s.pop();
          leftsmaller[i] = s.empty() ? -1 : s.top();
          s.push(i);
      }

      // Calculate max area
      int area = 0;
      for (int i = 0; i < n; i++) {
          int width = rightsmaller[i] - leftsmaller[i] - 1;
          area = max(area, heights[i] * width);
      }

      return area;
  }
};

```
---
---
🔹 LeetCode 155: Min Stack
Problem:
Design a stack that supports push, pop, top, and retrieving the minimum element in O(1).

Approach:
Use a stack of pairs: {value, min_so_far}.

On push:

If stack empty → {val, val}

Else → {val, min(val, s.top().second)}

On pop → remove top element.

top() → returns s.top().first

getMin() → returns s.top().second


Code:

class MinStack {
public:
    stack<pair<int,int>> s;

    MinStack() {}

    void push(int val) {
        if (s.empty()) {
            s.push({val, val});
        } else {
            s.push({val, min(val, s.top().second)});
        }
    }

    void pop() {
        s.pop();
    }

    int top() {
        return s.top().first;
    }

    int getMin() {
        return s.top().second;
    }
};
```
✨ Takeaways:
Monotonic stacks help solve nearest smaller/greater problems in O(n).

Min Stack shows how storing min_so_far with each value keeps operations efficient.

Dry runs help visualize stack changes and understand the logic step by step.