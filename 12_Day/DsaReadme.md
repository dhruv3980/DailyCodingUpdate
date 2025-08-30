## DSA Update - 30/08/2025




# Today, I worked on the following topics related to Binary Trees:

**Calculating the height of a binary tree.**

**Counting the number of nodes in the tree.**

**Calculating the sum of all nodes in the tree.**
---

**Topics Covered**
**1. Height of the Tree**

To calculate the height of the tree, I implemented a recursive function. The height is the length of the longest path from the root node to any leaf node.

**2. Count of Nodes**

A function was created to count the total number of nodes in the tree. This was done recursively by adding the nodes in the left and right subtrees.

**3. Sum of Nodes**

I implemented a recursive function to calculate the sum of all nodes in the tree.

## Code Snipet

**1. Height of the Tree**
```
int returnHeightOfTree(Node* head) {
    if(head == NULL) return 0;

    int leftHeight = returnHeightOfTree(head->left);
    int rightHeight = returnHeightOfTree(head->right);

    return max(leftHeight, rightHeight) + 1;
}

```

**2. Count of Nodes**
```
int countNumberOfNodes(Node* head) {
    if(head == NULL) return 0;

    return 1 + countNumberOfNodes(head->left) + countNumberOfNodes(head->right);
}
```

**3. Sum of Nodes**
```
int sumOfNodes(Node* head) {
    if(head == NULL) return 0;

    return head->data + sumOfNodes(head->left) + sumOfNodes(head->right);
}
```

## Example Usage

```
Node* root = generateTree({1, 2, 4, -1, -1, 5, -1, 6, -1, 7, -1, -1, 3, -1, -1});

cout << "Height of Tree: " << returnHeightOfTree(root) << endl;
cout << "Number of Nodes: " << countNumberOfNodes(root) << endl;
cout << "Sum of Nodes: " << sumOfNodes(root) << endl;
```
---

Example Output

Height of Tree: 4

Number of Nodes: 7

Sum of Nodes: 28

---


**This marks today's progress in understanding and implementing basic Binary Tree operations.**