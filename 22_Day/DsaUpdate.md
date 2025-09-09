# 📘 Daily DSA Notes – 09 Sept 2025



## 📝 Problem 1: Root-to-Leaf Paths in a BST

### Question
**Print all paths from root to leaf in a Binary Search Tree (BST).**

### Code
```cpp
void roottoleaf(Node* root, vector<int> &arr) {
    if (root == NULL) return;

    arr.push_back(root->data);
    if (root->left == NULL && root->right == NULL) {
        for (int val : arr) cout << val << " ";
        cout << endl;
        arr.pop_back();
        return;
    }

    roottoleaf(root->left, arr);
    roottoleaf(root->right, arr);
    arr.pop_back();
}
```
**Approach**

Perform DFS traversal while maintaining a path vector.

When reaching a leaf, print the current path.

Use backtracking to explore all possible paths.

---

### 📝 Problem 2: Print Nodes in a Given Range in BST
**Question**

**Given a BST and a range [start, end], print all elements that lie within this range.**

```
void printinrange(Node* root, int start, int end) {
    if (root == NULL) return;

    if (start <= root->data && root->data <= end) {
        printinrange(root->left, start, end);
        cout << root->data << " ";
        printinrange(root->right, start, end);
    } 
    else if (root->data < start) {
        printinrange(root->right, start, end);
    } 
    else {
        printinrange(root->left, start, end);
    }
}
```
---
**Approach**

Traverse BST recursively.

If node value lies in range → print it and explore both subtrees.

If node < start → only explore right subtree.

If node > end → only explore left subtree.

### 📝 Problem 3: LeetCode 98 – Validate Binary Search Tree

**Question**
Check if a binary tree is a valid BST.

```
class Solution {
public:
    bool helper(TreeNode* root, TreeNode* min, TreeNode* max) {
        if (root == NULL) return true;
        if (min != NULL && root->val <= min->val) return false;
        if (max != NULL && root->val >= max->val) return false;
        return helper(root->left, min, root) && helper(root->right, root, max);
    }

    bool isValidBST(TreeNode* root) {
        return helper(root, NULL, NULL);
    }
};
```


**Approach**

**Use recursion with min and max boundaries.**

For each node:

Left child must be < root

Right child must be > root

If any violation occurs, return false.

---

**✅ Today’s Work:**

### Printed all root-to-leaf paths in BST

### Printed nodes within a range in BST

### Validated BST structure (LeetCode 98)