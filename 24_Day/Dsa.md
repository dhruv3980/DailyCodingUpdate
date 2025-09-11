# 🧑‍💻 Binary Search Tree (BST) Problems in C++

 **Binary Search Tree (BST)** problems implemented in **C++**.

---

## 🚀 Problem 1: Merge Two BSTs

### Approach
1. Perform **inorder traversal** on both BSTs → gives two sorted arrays.
2. Merge the two sorted arrays into a single sorted array.
3. Build a **balanced BST** from the merged array using the middle element as root.

### Code
```cpp
#include<iostream>
#include<vector>
using namespace std;

class Node{
public:
    int data;
    Node* left;
    Node* right;
    Node(int data){
        this->data=data;
        left=right=NULL;
    }
};

void inorder(Node* root, vector<int>& arr){
    if(root==NULL) return;
    inorder(root->left, arr);
    arr.push_back(root->data);
    inorder(root->right, arr);
}

Node* buildTree(vector<int>& arr, int start, int end){
    if(start>end) return NULL;
    int mid = start+(end-start)/2;
    Node* root = new Node(arr[mid]);
    root->left=buildTree(arr, start, mid-1);
    root->right = buildTree(arr, mid+1, end);
    return root;
}

Node* mergeBst(Node* root1, Node* root2){
    vector<int> arr1, arr2;
    inorder(root1, arr1);
    inorder(root2, arr2);

    // merge sorted arrays
    vector<int> finalarr;
    int i=0, j=0;
    while(i<arr1.size() && j<arr2.size()){
        if(arr1[i]<arr2[j]) finalarr.push_back(arr1[i++]);
        else finalarr.push_back(arr2[j++]);
    }
    while(i<arr1.size()) finalarr.push_back(arr1[i++]);
    while(j<arr2.size()) finalarr.push_back(arr2[j++]);

    return buildTree(finalarr,0, finalarr.size()-1);
}

void print(Node* root){
    if(root==NULL) return;
    print(root->left);
    cout<<root->data<<" ";
    print(root->right);
}

int main(){
    Node* root1= new Node(2);
    root1->left = new Node(1);
    root1->right = new Node(4);

    Node* root2 = new Node(9);
    root2->left=new Node(3);
    root2->right = new Node(12);

    Node* root = mergeBst(root1, root2);
    print(root);  // Output: 1 2 3 4 9 12
}

```
# 🚀 Problem 2: Kth Smallest Element in a BST

## 📌 Problem
Given the root of a **Binary Search Tree (BST)** and an integer `k`, return the **k-th smallest value** (1-indexed) in the tree.

---

## 💡 Approach
- Perform an **inorder traversal** on the BST, since it visits nodes in **sorted order**.  
- Maintain a counter `k` while traversing.  
- Decrement `k` each time a node is visited.  
- When `k == 0`, the current node is the **k-th smallest element**.  

This ensures an **O(N)** time complexity in the worst case, with **O(H)** recursion depth (where `H` = tree height).

---

## 🧑‍💻 Code (C++)
```cpp

class Solution {
public:
    int getans(TreeNode* root, int& k){
        if(root == NULL) return -1;

        int leftans = getans(root->left, k);
        if(leftans != -1) return leftans;

        k--;
        if(k == 0) return root->val;

        return getans(root->right, k);
    }

    int kthSmallest(TreeNode* root, int k) {
        return getans(root, k);
    }
};
```

# 🚀 Problem 3: Minimum Absolute Difference in BST

## 📌 Problem
Given the root of a **Binary Search Tree (BST)**, return the **minimum absolute difference** between the values of any two different nodes.

---

## 💡 Approach
- Perform an **inorder traversal**, since it produces a **sorted sequence** of BST values.  
- Keep track of the **previous node value** while traversing.  
- At each step, compute the difference between the **current node** and the **previous node**.  
- Maintain the **minimum difference** across all nodes.  

This works because in a sorted sequence, the **smallest absolute difference** must occur between **consecutive elements**.

---

## 🧑‍💻 Code (C++)
```cpp

class Solution {
public:
    int ans = INT_MAX;
    int prev = -1;

    void getans(TreeNode* root){
        if(root == NULL) return;

        getans(root->left);

        if(prev != -1){
            ans = min(ans, root->val - prev);
        }
        prev = root->val;

        getans(root->right);
    }

    int getMinimumDifference(TreeNode* root) {
        getans(root);
        return ans;
    }
};
```

**📚 Learnings**

### Inorder traversal of a BST directly maps to sorted order.

### Passing variables by reference is crucial in recursion.

### The smallest implementation detail (like prev being int vs TreeNode*) can break logic.

