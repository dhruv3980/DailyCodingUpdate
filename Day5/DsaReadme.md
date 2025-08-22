# 🚀 Day 5 – DSA Progress  

## ✅ Problems Solved Today
- **Celebrity Problem (GeeksforGeeks)**

---

## 📘 Problem: Celebrity Problem  
In a party of *n* people, a **celebrity** is defined as:  
- A person who **knows no one**  
- But is **known by everyone**  

We are given an `n x n` matrix `mat`, where:  
- `mat[i][j] = 1` → person `i` knows person `j`  
- `mat[i][j] = 0` → person `i` does not know person `j`  

The task is to determine whether a celebrity exists, and if yes, return their index. Otherwise, return `-1`.

---

## 💡 Approach
1. Push all people (0…n-1) into a **stack**.  
2. Compare two people at a time:  
   - If `i` knows `j`, then `i` cannot be celebrity → keep `j`.  
   - Else, `j` cannot be celebrity → keep `i`.  
3. Continue until one candidate remains.  
4. Verify the candidate by checking:  
   - Everyone knows them.  
   - They know no one.  

---

## 🧑‍💻 Code (C++ Implementation)
```cpp
class Solution {
  public:
    int celebrity(vector<vector<int>>& mat) {
        stack<int> s;
        int n = mat.size();

        // Step 1: Push all people into stack
        for (int i = 0; i < n; i++) s.push(i);

        // Step 2: Eliminate non-celebrities
        while (s.size() > 1) {
            int i = s.top(); s.pop();
            int j = s.top(); s.pop();

            if (mat[i][j] == 1) s.push(j); // i knows j → i not celebrity
            else s.push(i);                // i doesn't know j → j not celebrity
        }

        int ans = s.top();

        // Step 3: Verify candidate
        for (int i = 0; i < n; i++) {
            if (i != ans && (mat[i][ans] == 0 || mat[ans][i] == 1)) {
                return -1;
            }
        }
        return ans;
    }
};
```
---
---
⏱️ Complexity Analysis
Time Complexity: O(n)

Space Complexity: O(n)

---
✨ Key Takeaway
This problem was a great refresher on stack-based elimination and matrix validation.
It shows how clever use of data structures can optimize an otherwise brute-force O(n²) solution into an efficient O(n) approach.
---
📌 Continuing my journey to strengthen problem-solving skills with daily practice!