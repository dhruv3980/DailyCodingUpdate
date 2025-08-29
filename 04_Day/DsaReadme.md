📘 Day 4 – DSA Progress
---
✅ Problems Solved Today:
---
Trapping Rain Water (Leetcode 42)

Next Greater Element II (Leetcode 503)

🏗️ Problem 1: Trapping Rain Water (Leetcode 42)
🔹 Method 1 – Prefix/Suffix Arrays (Space O(n))

Idea:

For each index i, the trapped water depends on the minimum of the tallest bar to the left and the tallest bar to the right.

Precompute:

leftMax[i] = maximum height from 0 → i.

rightMax[i] = maximum height from i → n-1.

Water trapped at index i = min(leftMax[i], rightMax[i]) - height[i] (if positive).

Steps:

Build leftMax[] from left to right.

Build rightMax[] from right to left.

Loop over each index and calculate trapped water.
---
Time Complexity: O(n)
Space Complexity: O(n)
---

Code:
```

class Solution {
public:
    int trap(vector<int>& height) {
        int n = height.size();
        if (n == 0) return 0;

        vector<int> leftMax(n), rightMax(n);
        leftMax[0] = height[0];
        for (int i = 1; i < n; i++) {
            leftMax[i] = max(leftMax[i - 1], height[i]);
        }

        rightMax[n - 1] = height[n - 1];
        for (int i = n - 2; i >= 0; i--) {
            rightMax[i] = max(rightMax[i + 1], height[i]);
        }

        int ans = 0;
        for (int i = 0; i < n; i++) {
            ans += min(leftMax[i], rightMax[i]) - height[i];
        }
        return ans;
    }
};

```
---
🔹 Method 2 – Two Pointers (Optimized)

Keep two pointers left, right.

Maintain leftMax, rightMax.

Move the pointer that has the smaller max boundary inward.

Add trapped water as leftMax - height[left] or rightMax - height[right].
---
Time Complexity: O(n)
Space Complexity: O(1)
---

Code:
```
class Solution {
public:
    int trap(vector<int>& height) {
        int n = height.size();
        int left = 0, right = n - 1;
        int leftMax = height[left], rightMax = height[right];
        int ans = 0;

        while (left < right) {
            if (leftMax < rightMax) {
                left++;
                leftMax = max(leftMax, height[left]);
                ans += leftMax - height[left];
            } else {
                right--;
                rightMax = max(rightMax, height[right]);
                ans += rightMax - height[right];
            }
        }
        return ans;
    }
};

```


---

🏗️ Problem 2: Next Greater Element II (Leetcode 503)
🔹 Approach – Monotonic Stack + Circular Array

Traverse array 2*n times (2*n - 1 → 0) to simulate circular behavior.

Use a monotonic decreasing stack:

Pop smaller elements.

If stack not empty → top is next greater.

Push current element.

Time Complexity: O(n)
Space Complexity: O(n)



Code:
```
class Solution {
public:
    vector<int> nextGreaterElements(vector<int>& nums) {
        int n = nums.size();
        vector<int> ans(n, -1);
        stack<int> s;

        for (int i = 2*n - 1; i >= 0; i--) {
            while (!s.empty() && s.top() <= nums[i % n]) {
                s.pop();
            }
            if (i < n) ans[i] = s.empty() ? -1 : s.top();
            s.push(nums[i % n]);
        }
        return ans;
    }
};
```
---
📝 Learnings Today:

Trapping Rain Water:

Prefix/Suffix arrays (space O(n) → easier to think).

Two Pointers (space O(1) → optimized).

Monotonic Stack is a powerful tool for problems like Next Greater Element.

Circular arrays can be handled by iterating 2*n times with modulo indexing.
---
✨ Day 4 Complete!

Solved 2 problems.

Strengthened concepts in two pointers, prefix/suffix arrays, and monotonic stacks.