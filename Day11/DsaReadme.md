# 🌳 Binary Tree Traversal in C++

## 🚀 Day 11

---

## 📌 Features

- Build a binary tree using **preorder input**.
- Implemented **DFS Traversals**:
  - Preorder Traversal
  - Inorder Traversal
  - Postorder Traversal
- Implemented **BFS Traversals**:
  - Simple Level Order Traversal
  - Modified Level Order Traversal (prints nodes level by level)

---

## 🛠️ Code Overview

### 1. **Node Class**
```
class Node {
public:
    int data;
    Node* left;
    Node* right;

    Node(int data) {
        this->data = data;
        this->left = NULL;
        this->right = NULL;
    }
};
```
---
**2. Build Tree (Recursive)**

```
int idx = -1;
Node* buildTree(vector<int>& node) {
    idx++;
    if (node[idx] == -1) {
        return NULL;
    }

    Node* currentNode = new Node(node[idx]);
    currentNode->left = buildTree(node);
    currentNode->right = buildTree(node);

    return currentNode;
}
```
---


**3 DFS Traversals**
```
// Preorder (Root → Left → Right)
void preOrderTraversal(Node* head) {
    if (head == NULL) return;
    cout << head->data << " ";
    preOrderTraversal(head->left);
    preOrderTraversal(head->right);
}

// Inorder (Left → Root → Right)
void inOrderTraversal(Node* head) {
    if (head == NULL) return;
    inOrderTraversal(head->left);
    cout << head->data << " ";
    inOrderTraversal(head->right);
}

// Postorder (Left → Right → Root)
void postOrderTraversal(Node* head) {
    if (head == NULL) return;
    postOrderTraversal(head->left);
    postOrderTraversal(head->right);
    cout << head->data << " ";
}
```
---

**4. BFS Traversals**
```
// Simple Level Order Traversal
void levelOrderTraversal(Node* head) {
    if (head == NULL) return;

    queue<Node*> q;
    q.push(head);

    while (!q.empty()) {
        Node* current = q.front();
        q.pop();

        cout << current->data << " ";

        if (current->left != NULL) q.push(current->left);
        if (current->right != NULL) q.push(current->right);
    }
}
```
---

**// Modified Level Order Traversal (prints line by line)**
```
void modifyLevelOrderTraversal(Node* head) {
    if (head == NULL) return;

    queue<Node*> q;
    q.push(head);
    q.push(NULL);

    while (!q.empty()) {
        Node* current = q.front();
        q.pop();

        if (current == NULL) {
            cout << endl;
            if (!q.empty()) {
                q.push(NULL);
            }
        } else {
            cout << current->data << " ";
            if (current->left != NULL) q.push(current->left);
            if (current->right != NULL) q.push(current->right);
        }
    }
}
```
---

**5. Main Function**
```
int main() {
    vector<int> node {1,2,4,-1,-1,5,-1,-1,3,-1,6,-1,-1};

    Node* head = buildTree(node);

    cout << "The current head value is " << head->data << endl;

    cout << "Print Preorder Traversal" << endl;
    preOrderTraversal(head);

    cout << endl << "Print Inorder Traversal" << endl;
    inOrderTraversal(head);

    cout << endl << "Print Postorder Traversal" << endl;
    postOrderTraversal(head);

    cout << endl << "Printing Level Order Traversal" << endl;
    levelOrderTraversal(head);

    cout << endl << "Printing Modified Level Order Traversal" << endl;
    modifyLevelOrderTraversal(head);

    return 0;
}

```
---

**🌲 Example Input**

## Preorder vector:


vector<int> node {1, 2, 4, -1, -1, 5, -1, -1, 3, -1, 6, -1, -1};
This represents the tree:

markdown

        1
       / \
      2   3
     / \    \
    4   5    6

📤 Example Output


The current head value is 1

Print Preorder Traversal
1 2 4 5 3 6 

Print Inorder Traversal
4 2 5 1 3 6 

Print Postorder Traversal
4 5 2 6 3 1 

Printing Level Order Traversal
1 2 3 4 5 6 

Printing Modified Level Order Traversal
1 
2 3 
4 5 6 