# 📘 DSA Notes – 10 Sept 2025  

**Today I solved 3 important tree-based problems in C++ 🚀**

---

## ✅ Problem 1: Build a Balanced BST from a Sorted Array  

- **Idea:**  
  - Use the middle element as the root.  
  - Recursively build left and right subtrees from left/right halves.  
- **Why it works:**  
  - Middle ensures balance (O(log n) height).  

### Code Snippet:
```cpp
Node* buildBST(int arr[], int start, int end){
    if(start > end) return NULL;
    int mid = start + (end - start) / 2;
    Node* current = new Node(arr[mid]);
    current->left = buildBST(arr, start, mid - 1);
    current->right = buildBST(arr, mid + 1, end);
    return current;
}
```

### ✅ Problem 2: Convert Skewed BST to Balanced BST

**Steps:**

**Store inorder traversal in a vector (sorted order).**

**Rebuild balanced BST from that sorted vector.**

#### Why it works:

**Inorder of BST = sorted array.**

**Balanced construction same as Problem 1.**

```
void storeInorder(Node* root, vector<int>& arr){
    if(root==NULL) return;
    storeInorder(root->left, arr);
    arr.push_back(root->data);
    storeInorder(root->right, arr);
}

Node* buildBalanced(vector<int>& arr, int start, int end){
    if(start > end) return NULL;
    int mid = start + (end - start) / 2;
    Node* node = new Node(arr[mid]);
    node->left = buildBalanced(arr, start, mid - 1);
    node->right = buildBalanced(arr, mid + 1, end);
    return node;
}
```

### ✅ Problem 3: Largest BST in a Binary Tree (LeetCode #333)

**Idea:**

#### For each node, compute:

**min, max, isBST, size of its subtree.**

**If both children are BSTs and conditions hold → current subtree is BST.**

**Track max size in a global variable.**

**Key Condition:**

```
root->data > left.max && root->data < right.min
```

```
info* largestBST(Node* root){
    if(root==NULL) return new info(INT_MAX, INT_MIN, true, 0);

    info* left = largestBST(root->left);
    info* right = largestBST(root->right);

    int currentMin = min(root->data, min(left->min, right->min));
    int currentMax = max(root->data, max(left->max, right->max));
    int currentSize = left->size + right->size + 1;

    if(left->isBst && right->isBst &&
       root->data > left->max && root->data < right->min){
        maxvalue = max(maxvalue, currentSize);
        return new info(currentMin, currentMax, true, currentSize);
    }

    return new info(currentMin, currentMax, false, currentSize);
}
```

---
**📌 Learnings from Today**

**Balanced BSTs can be built using divide & conquer (take mid as root).**

**Any skewed BST can be restructured into balanced by inorder → rebuild.**

**Largest BST in a binary tree requires bottom-up information passing (min, max, isBST, size).**

**Always handle edge cases carefully (INT_MIN, INT_MAX as boundaries).**

