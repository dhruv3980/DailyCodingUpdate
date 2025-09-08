## 📘 DSA Update – 8/9/2025
#### Topic: Binary Search Tree (BST) – Insertion, Search, Traversal, Deletion



🔑 Concepts Covered
Binary Search Tree (BST)


A BST is a binary tree where:

Left child < Node

Right child > Node

---

Used for efficient searching, insertion, and deletion.

---

**Insertion in BST**

Recursively find the correct position based on value.

**Time Complexity:**

Average: O(log n)

**Worst case** (skewed tree): O(n)

```
Node* insert(Node* root, int val){
    if(root == NULL) return new Node(val);
    if(val < root->val) root->left = insert(root->left, val);
    else root->right = insert(root->right, val);
    return root;
}
```

**Generate BST from Array**

Insert all array elements into the BST.

Time Complexity: O(n log n) on average.

```
Node* generateBst(int arr[], int n){
    Node* root = NULL;
    for(int i=0; i<n; i++){
        root = insert(root, arr[i]);
    }
    return root;
}
```

**Inorder Traversal**

Left → Root → Right

Gives sorted order for BST.

Time Complexity: O(n)

```
void inorder(Node* root){
    if(root == NULL) return;
    inorder(root->left);
    cout << root->val << " ";
    inorder(root->right);
}
```


**Search in BST**

Recursively compare the key with root.

Time Complexity:

Average: O(log n)

Worst case: O(n)
```

bool search(Node* root, int key){
    if(root == NULL) return false;
    if(root->val == key) return true;
    if(key < root->val) return search(root->left, key);
    return search(root->right, key);
}
```

**Deletion in BST**

Three Cases:

Leaf Node → Delete directly.

One Child → Replace node with child.

Two Children → Find Inorder Successor, replace value, and delete successor.

Time Complexity: O(log n) average, O(n) worst case.

```
Node* findInorderSuccessor(Node* root){
    while(root->left != NULL){
        root = root->left;
    }
    return root;
}

Node* deleteInBst(Node* root, int key){
    if(root == NULL) return NULL;

    if(key < root->val) root->left = deleteInBst(root->left, key);
    else if(key > root->val) root->right = deleteInBst(root->right, key);
    else {
        if(root->left == NULL && root->right == NULL){
            delete root;
            return NULL;
        }
        if(root->left == NULL || root->right == NULL){
            Node* child = root->left ? root->left : root->right;
            delete root;
            return child;
        }
        Node* succ = findInorderSuccessor(root->right);
        root->val = succ->val;
        root->right = deleteInBst(root->right, succ->val);
    }
    return root;
}
```

⚡ Example Run
```
int main(){
    int arr[]={8,5,10,3,6,1,4,11,14};
    int n = 9;

    Node* root = generateBst(arr, n);

    cout << "Inorder Traversal: ";
    inorder(root); // prints sorted values
    cout << endl;

    cout << "Search 15: " << search(root, 15) << endl;

    root = deleteInBst(root, 8);
    cout << "After deleting 8: ";
    inorder(root);
}
```



