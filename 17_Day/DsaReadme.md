# DSA Learning Log - Binary Trees

📅 **Date:** 4th September 2025

This is my daily learning log where I solve and note down DSA problems, focusing on **binary trees** today.

---

## 🥇 Problem 1: Kth Ancestor of a Node

**📝 Problem:**
Given a binary tree and a node, find its kth ancestor.

**💡 Approach:**

* Use recursion to traverse the tree.
* If current node is NULL → return -1.
* If current node is the target → return 0.
* Recursively check left and right subtrees.
* If either subtree returns a valid value, increment it by 1.
* If incremented value equals k → print current node as kth ancestor.

**💻 Solution (C++):**

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
        this->left=NULL;
        this->right=NULL;
    }
};

int idx=-1;
Node* generateTree(vector<int>& arr){
    idx++;
    if(arr[idx]==-1) return NULL;
    Node* head = new Node(arr[idx]);
    head->left = generateTree(arr);
    head->right = generateTree(arr);
    return head;
}

int kthancestor(Node* head, int node, int k){
    if(head==NULL) return -1;
    if(head->data==node) return 0;

    int leftans = kthancestor(head->left, node, k);
    int rightans = kthancestor(head->right, node, k);

    if(leftans==-1 && rightans==-1) return -1;

    int val = leftans==-1 ? rightans : leftans;
    if(val+1==k) cout << "kth ancestor is " << head->data << endl;
    return val+1;
}

int main(){
    vector<int> arr = {1,2,4,-1,-1,5,-1,6,-1,7,-1,-1,3,-1,-1};
    Node* root = generateTree(arr);
    kthancestor(root, 5, 2);
}
```

---

## 🔹 Problem 2: Lowest Common Ancestor (LCA)

**📝 Problem:**
Given a binary tree and two nodes, find their lowest common ancestor.

**💡 Approach:**

* Traverse the tree recursively.
* If current node is NULL → return NULL.
* If current node matches either target → return current node.
* Recursively find LCA in left and right subtrees.
* If both sides return non-NULL → current node is LCA.
* Else → return whichever side is non-NULL.

**💻 Solution (C++):**

```cpp
Node* LCA(Node* root, int n1, int n2){
    if(root==NULL) return NULL;
    if(root->data==n1 || root->data==n2) return root;

    Node* left = LCA(root->left, n1, n2);
    Node* right = LCA(root->right, n1, n2);

    if(left!=NULL && right!=NULL) return root;
    return left ? left : right;
}

int main(){
    vector<int> arr = {1,2,4,-1,-1,5,-1,-1,3,-1,6,-1,-1};
    Node* root = generateTree(arr);
    Node* ancestor = LCA(root, 5, 3);
    if(ancestor) cout << "LCA is: " << ancestor->data << endl;
}
```

---

## 🔹 Problem 3: Distance Between Two Nodes

**📝 Problem:**
Find the distance between two nodes in a binary tree.

**💡 Approach:**

* Find LCA of the two nodes.
* Calculate distance from LCA to each node.
* Sum the distances.

**💻 Solution (C++):**

```cpp
int minimumdistance(Node* root, int data){
    if(root==NULL) return -1;
    if(root->data==data) return 0;

    int left = minimumdistance(root->left, data);
    if(left!=-1) return left+1;

    int right = minimumdistance(root->right, data);
    if(right!=-1) return right+1;

    return -1;
}

int main(){
    vector<int> arr = {1,2,4,-1,-1,5,-1,-1,3,-1,6,-1,-1};
    Node* root = generateTree(arr);
    Node* ancestor = LCA(root, 5, 3);

    int dist1 = minimumdistance(ancestor, 5);
    int dist2 = minimumdistance(ancestor, 3);

    cout << "Distance between 5 and 3: " << dist1 + dist2 << endl;
}
```

---

**Takeaways:**

**Practiced binary tree traversal and recursion.**
---
**Solved problems like kth ancestor, LCA, and distance between nodes.**
---
**Enhanced problem-solving skills in tree-based DSA problems.**
