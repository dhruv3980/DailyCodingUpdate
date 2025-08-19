# 🚀 Day 2 – DSA Problem Solving Notes

Today I practiced stack-based problems that focus on finding **Next Greater Element** and **Previous Smaller Element**.  
These problems helped me understand how **monotonic stacks** can reduce time complexity from O(n²) to O(n).

---

## 📝 Problems Solved

### 1️⃣ Previous Smaller Element
**Problem:** For each element in the array, find the closest smaller element on the left. If none exists, return `-1`.

**Approach:**
- Use a stack to keep track of elements.
- Pop from the stack until a smaller element is found.
- If stack is empty → no smaller element, assign `-1`.

**Code:**
```cpp
vector<int> previoussmaller(vector<int>& arr) {
    vector<int> ans(arr.size(), 0);
    stack<int> s;

    for (int i = 0; i < arr.size(); i++) {
        while (!s.empty() && s.top() >= arr[i]) {
            s.pop();
        }
        ans[i] = s.empty() ? -1 : s.top();
        s.push(arr[i]);
    }
    return ans;
}

```

2️⃣ Next Greater Element (Single Array – GFG Style)
Problem: For each element in the array, find the closest greater element on the right. If none exists, return -1.

Approach:

Traverse from right → left.

Maintain stack of candidates.

Assign -1 if stack is empty, otherwise assign top of stack.

Code:

```cpp
vector<int> nextLargerElement(vector<int>& arr) {
    vector<int> ans(arr.size(), 0);
    stack<int> s;
    
    for (int i = arr.size()-1; i >= 0; i--) {
        while (!s.empty() && s.top() <= arr[i]) {
            s.pop();
        }
        ans[i] = s.empty() ? -1 : s.top();
        s.push(arr[i]);
    }
    return ans;
}

```

3️⃣ Next Greater Element (LeetCode – Two Arrays)
Problem:
Given two arrays nums1 and nums2, find the next greater element for each element of nums1 as it appears in nums2.

Approach:

Use a map to store next greater elements for all values in nums2.

Iterate from right → left over nums2 while maintaining a stack.

Lookup results for nums1 in O(1).

Code:

```cpp

vector<int> nextGreaterElement(vector<int>& nums1, vector<int>& nums2) {
    stack<int> s;
    unordered_map<int, int> m;
    vector<int> ans;

    for (int i = nums2.size()-1; i >= 0; i--) {
        while (!s.empty() && s.top() < nums2[i]) {
            s.pop();
        }
        m[nums2[i]] = s.empty() ? -1 : s.top();
        s.push(nums2[i]);
    }

    for (int num : nums1) {
        ans.push_back(m[num]);
    }
    return ans;
}
```

🔑 Key Takeaways
Monotonic Stacks are powerful for "next/previous greater/smaller element" problems.

Direction of traversal matters:

Left → Right for previous problems.

Right → Left for next problems.

HashMaps help when dealing with subsets (LeetCode version).

📌 Day 2 complete. Feeling more confident with stack-based problems!


#DSA #C++ #ProblemSolving #100DaysOfCode