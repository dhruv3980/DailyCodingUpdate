# 📘 My DSA Learning Notes  

## 📅 Date: 18th August 2025  
Today I solved **two stack-based problems**.  
This README is my **learning log + notes for revision**.  

---

## 🥇 First Question: Stock Span Problem (GeeksforGeeks)

### 📝 Problem  
For each day’s stock price, calculate how many consecutive days before it had prices **less than or equal** to today’s price.  

---

### 💡 Approach  
- Use a **monotonic decreasing stack** (store indices).  
- While current price ≥ top of stack → pop.  
- If stack becomes empty → span = i + 1.  
- Else → span = i – index of last greater element.  

---

### 💻 Solution (C++)  
```cpp
class Solution {
  public:
    vector<int> calculateSpan(vector<int>& arr) {
        vector<int> ans(arr.size(), 0);
        stack<int> s;

        for (int i = 0; i < arr.size(); i++) {
            while (!s.empty() && arr[s.top()] <= arr[i]) {
                s.pop();
            }

            if (s.empty()) {
                ans[i] = i + 1;
            } else {
                ans[i] = i - s.top();
            }

            s.push(i);
        }
        return ans;
    }
};

```


# 🔹 Valid Parentheses (LeetCode)

## 📝 Problem  
Given a string containing only characters `()[]{}`, determine if the input string is a **valid parentheses sequence**.  
A string is valid if:  
1. Open brackets are closed by the same type of brackets.  
2. Open brackets are closed in the correct order.  

---

## 💡 Approach  
- Use a **stack** to keep track of opening brackets.  
- Traverse the string:  
  - If current char is an **opening bracket** → push to stack.  
  - If it is a **closing bracket** →  
    - Check if stack is empty → ❌ invalid.  
    - Otherwise, check if it matches the top of the stack → if yes, pop.  
    - If not matching → ❌ invalid.  
- At the end, string is valid if and only if the stack is empty.  

---

## 💻 Solution (C++)  
```cpp
class Solution {
public:
    bool isValid(string s) {
        stack<int> ans;
        for (int i = 0; i < s.size(); i++) {
            if (s[i] == '(' || s[i] == '{' || s[i] == '[') {
                ans.push(s[i]);
            } else {
                if (ans.empty()) {
                    return false;
                }

                if ((ans.top() == '(' && s[i] == ')') ||
                    (ans.top() == '{' && s[i] == '}') ||
                    (ans.top() == '[' && s[i] == ']')) {
                    ans.pop();
                } else {
                    return false;
                }
            }
        }
        return ans.empty();
    }
};

