# 🌳 Binary Tree DSA Problems (02/09/2025)

This README contains my solutions and approaches for three important binary tree problems from **LeetCode** and **GeeksforGeeks**.  
---
I solved each problem in **C++**, explained my thought process, and analyzed the time/space complexity.

---

## 🔹 LeetCode 572: Subtree of Another Tree

### Problem
Check whether `subRoot` is a subtree of another binary tree `root`.

### My Approach

- I first wrote a helper function `isIdentical` that checks if two trees are exactly the same.  
- Then, I recursively traverse the `root` and whenever I find a node with the same value as `subRoot->val`, I check if both trees match.  
- If yes, return `true`. Otherwise, continue searching in left and right subtrees.

### Code
```
class Solution {
public:
    bool isIdentical(TreeNode* root, TreeNode* subRoot) {
        if(root==NULL && subRoot==NULL) return true;
        if(root==NULL || subRoot==NULL) return false;
        if(root->val != subRoot->val) return false;

        return isIdentical(root->left, subRoot->left) &&
               isIdentical(root->right, subRoot->right);
    }

    bool isSubtree(TreeNode* root, TreeNode* subRoot) {
        if(root==NULL) return false;
        if(isIdentical(root, subRoot)) return true;

        return isSubtree(root->left, subRoot) || 
               isSubtree(root->right, subRoot);
    }
};
```
**Complexity**
Time: O(n * m) (in worst case we compare subRoot at every node of root).

**Space**: O(h) (recursion stack, where h = height of tree).

## 🔹 GFG: Top View of Binary Tree

**Problem**
**Return the top view of a binary tree (first visible nodes when viewed from above).**

## My Approach

I used BFS (level order traversal) with a queue.

Along with each node, I stored its Horizontal Distance (HD) from the root.

For each HD, I only stored the first node encountered in a map<int,int>.

Finally, I iterated over the map to get nodes in left-to-right order.

---

```
class Solution {
  public:
    map<int, int> topviewofthebinarytree(Node* root) {
        queue<pair<Node*, int>> q;
        map<int, int> m;
        
        if(root == NULL) return m;
        q.push({root, 0});
        
        while(!q.empty()) {
            auto current = q.front(); q.pop();
            Node* node = current.first;
            int hd = current.second;
            
            if(m.count(hd) == 0) {  // first time this HD
                m[hd] = node->data;
            }
            if(node->left)  q.push({node->left, hd-1});
            if(node->right) q.push({node->right, hd+1});
        }
        return m;
    }
    
    vector<int> topView(Node *root) {
        vector<int> ans;
        map<int, int> m = topviewofthebinarytree(root);
        for(auto it : m) ans.push_back(it.second);
        return ans;
    }
};

```

**Complexity**

## Time: O(n log n) (map insertions).

## Space: O(n).

👉 If I use unordered_map, insertion becomes O(1) avg, but I still need to sort by HD → overall still O(n log n).


## 🔹 GFG: Bottom View of Binary Tree

**Problem**
## Return the bottom view of a binary tree (last visible nodes when viewed from below).

## My Approach
---
Very similar to Top View, but here I overwrite the map entry for each HD with the most recent node encountered at that horizontal distance.

The last node for each HD (encountered in BFS) will represent the bottom view.

```
class Solution {
  public:
    map<int, int> bottomviewofthetree(Node* root) {
        queue<pair<Node*, int>> q;
        map<int, int> m;
        
        if(root == NULL) return m;
        q.push({root, 0});
        
        while(!q.empty()) {
            auto current = q.front(); q.pop();
            Node* node = current.first;
            int hd = current.second;
            
            m[hd] = node->data;  // overwrite
            if(node->left)  q.push({node->left, hd-1});
            if(node->right) q.push({node->right, hd+1});
        }
        return m;
    }
    
    vector<int> bottomView(Node *root) {
        vector<int> ans;
        map<int, int> m = bottomviewofthetree(root);
        for(auto it : m) ans.push_back(it.second);
        return ans;
    }
};
```

**Complexity**
## Time: O(n log n) (map insertions).

## Space: O(n).



## 🔹 Key Learnings (02/09/2025)
**Top View: take the first node at each HD.**

**Bottom View: take the last node at each HD.**

**Using map keeps order by default, but unordered_map needs extra sorting.**

**Subtree check (LC 572) → reduce to repeated tree comparison problem.**