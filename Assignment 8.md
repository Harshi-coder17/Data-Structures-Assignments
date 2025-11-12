# Data Structures Assignment
## Assignment 8

---
### Q1. Write program using functions for binary tree traversals: Pre-order, In-order and Post-order using recursive approach.
```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
};

Node* createNode(int val) {
    Node* newNode = new Node();
    newNode->data = val;
    newNode->left = newNode->right = NULL;
    return newNode;
}

// Recursive traversals
void inorder(Node* root) {
    if (root == NULL) return;
    inorder(root->left);
    cout << root->data << " ";
    inorder(root->right);
}

void preorder(Node* root) {
    if (root == NULL) return;
    cout << root->data << " ";
    preorder(root->left);
    preorder(root->right);
}

void postorder(Node* root) {
    if (root == NULL) return;
    postorder(root->left);
    postorder(root->right);
    cout << root->data << " ";
}

int main() {
    Node* root = createNode(1);
    root->left = createNode(2);
    root->right = createNode(3);
    root->left->left = createNode(4);
    root->left->right = createNode(5);

    cout << "In-order Traversal: ";
    inorder(root);
    cout << "\nPre-order Traversal: ";
    preorder(root);
    cout << "\nPost-order Traversal: ";
    postorder(root);
    cout << endl;

    return 0;
}
```
---
### Q2. Implement following functions for Binary Search Trees
#### (a) Search a given item (Recursive & Non-Recursive)
```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
};

Node* createNode(int val) {
    Node* newNode = new Node();
    newNode->data = val;
    newNode->left = newNode->right = NULL;
    return newNode;
}

Node* insert(Node* root, int val) {
    if (root == NULL) return createNode(val);
    if (val < root->data)
        root->left = insert(root->left, val);
    else if (val > root->data)
        root->right = insert(root->right, val);
    return root;
}

// Recursive Search
Node* searchRecursive(Node* root, int key) {
    if (root == NULL || root->data == key)
        return root;
    if (key < root->data)
        return searchRecursive(root->left, key);
    return searchRecursive(root->right, key);
}

// Non-Recursive Search
Node* searchIterative(Node* root, int key) {
    while (root != NULL) {
        if (root->data == key)
            return root;
        else if (key < root->data)
            root = root->left;
        else
            root = root->right;
    }
    return NULL;
}

int main() {
    Node* root = NULL;
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 70);
    insert(root, 20);
    insert(root, 40);
    insert(root, 60);
    insert(root, 80);

    int key = 60;
    Node* found = searchRecursive(root, key);
    cout << "Recursive Search: ";
    cout << (found ? "Element Found\n" : "Not Found\n");

    found = searchIterative(root, key);
    cout << "Iterative Search: ";
    cout << (found ? "Element Found\n" : "Not Found\n");

    return 0;
}
```
---
#### (b) Maximum element of the BST
```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
};

Node* insert(Node* root, int val) {
    if (root == NULL) {
        Node* newNode = new Node();
        newNode->data = val;
        newNode->left = newNode->right = NULL;
        return newNode;
    }
    if (val < root->data)
        root->left = insert(root->left, val);
    else
        root->right = insert(root->right, val);
    return root;
}

int findMax(Node* root) {
    if (root == NULL) return -1;
    while (root->right != NULL)
        root = root->right;
    return root->data;
}

int main() {
    Node* root = NULL;
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 70);
    insert(root, 20);
    insert(root, 80);

    cout << "Maximum element in BST: " << findMax(root) << endl;
    return 0;
}
```
---
#### (c) Minimum element of the BST
```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
};

Node* insert(Node* root, int val) {
    if (root == NULL) {
        Node* n = new Node();
        n->data = val;
        n->left = n->right = NULL;
        return n;
    }
    if (val < root->data)
        root->left = insert(root->left, val);
    else
        root->right = insert(root->right, val);
    return root;
}

int findMin(Node* root) {
    if (root == NULL) return -1;
    while (root->left != NULL)
        root = root->left;
    return root->data;
}

int main() {
    Node* root = NULL;
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 70);
    insert(root, 20);
    insert(root, 80);

    cout << "Minimum element in BST: " << findMin(root) << endl;
    return 0;
}
```
---
#### (d) In-order successor of a given node the BST
```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
};

Node* insert(Node* root, int val) {
    if (root == NULL) {
        Node* n = new Node();
        n->data = val;
        n->left = n->right = NULL;
        return n;
    }
    if (val < root->data)
        root->left = insert(root->left, val);
    else
        root->right = insert(root->right, val);
    return root;
}

Node* findMin(Node* node) {
    while (node->left != NULL)
        node = node->left;
    return node;
}

Node* inorderSuccessor(Node* root, Node* target) {
    Node* successor = NULL;
    while (root != NULL) {
        if (target->data < root->data) {
            successor = root;
            root = root->left;
        } else if (target->data > root->data)
            root = root->right;
        else
            break;
    }
    if (target->right != NULL)
        return findMin(target->right);
    return successor;
}

int main() {
    Node* root = NULL;
    root = insert(root, 20);
    insert(root, 8);
    insert(root, 22);
    insert(root, 4);
    insert(root, 12);
    insert(root, 10);
    insert(root, 14);

    Node* target = root->left->right; // Node with value 12
    Node* succ = inorderSuccessor(root, target);
    if (succ)
        cout << "Inorder Successor of " << target->data << " is " << succ->data << endl;
    else
        cout << "No Successor Found" << endl;

    return 0;
}
```
---
#### (e) In-order predecessor of a given node the BST
```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
};

Node* insert(Node* root, int val) {
    if (root == NULL) {
        Node* n = new Node();
        n->data = val;
        n->left = n->right = NULL;
        return n;
    }
    if (val < root->data)
        root->left = insert(root->left, val);
    else
        root->right = insert(root->right, val);
    return root;
}

Node* findMax(Node* node) {
    while (node->right != NULL)
        node = node->right;
    return node;
}

Node* inorderPredecessor(Node* root, Node* target) {
    Node* predecessor = NULL;
    while (root != NULL) {
        if (target->data > root->data) {
            predecessor = root;
            root = root->right;
        } else if (target->data < root->data)
            root = root->left;
        else
            break;
    }
    if (target->left != NULL)
        return findMax(target->left);
    return predecessor;
}

int main() {
    Node* root = NULL;
    root = insert(root, 20);
    insert(root, 8);
    insert(root, 22);
    insert(root, 4);
    insert(root, 12);
    insert(root, 10);
    insert(root, 14);

    Node* target = root->left->right; // Node with value 12
    Node* pred = inorderPredecessor(root, target);
    if (pred)
        cout << "Inorder Predecessor of " << target->data << " is " << pred->data << endl;
    else
        cout << "No Predecessor Found" << endl;

    return 0;
}
```
---
### Q3. Write a program for binary search tree (BST) having functions for the following operations:
#### (a) Insert an element (no duplicates are allowed),
#### (b) Delete an existing element,
#### (c) Maximum depth of BST
#### (d) Minimum depth of
```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
};

Node* insert(Node* root, int val) {
    if (root == NULL) {
        Node* n = new Node();
        n->data = val;
        n->left = n->right = NULL;
        return n;
    }
    if (val < root->data)
        root->left = insert(root->left, val);
    else if (val > root->data)
        root->right = insert(root->right, val);
    return root;
}

Node* findMin(Node* node) {
    while (node->left != NULL)
        node = node->left;
    return node;
}

Node* deleteNode(Node* root, int key) {
    if (root == NULL) return root;
    if (key < root->data)
        root->left = deleteNode(root->left, key);
    else if (key > root->data)
        root->right = deleteNode(root->right, key);
    else {
        if (root->left == NULL) {
            Node* temp = root->right;
            delete root;
            return temp;
        }
        else if (root->right == NULL) {
            Node* temp = root->left;
            delete root;
            return temp;
        }
        Node* temp = findMin(root->right);
        root->data = temp->data;
        root->right = deleteNode(root->right, temp->data);
    }
    return root;
}

int maxDepth(Node* root) {
    if (root == NULL) return 0;
    int left = maxDepth(root->left);
    int right = maxDepth(root->right);
    return (left > right ? left : right) + 1;
}

int minDepth(Node* root) {
    if (root == NULL) return 0;
    int left = minDepth(root->left);
    int right = minDepth(root->right);
    return (left < right ? left : right) + 1;
}

void inorder(Node* root) {
    if (root != NULL) {
        inorder(root->left);
        cout << root->data << " ";
        inorder(root->right);
    }
}

int main() {
    Node* root = NULL;
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 70);
    insert(root, 20);
    insert(root, 40);
    insert(root, 60);
    insert(root, 80);

    cout << "In-order before deletion: ";
    inorder(root);
    cout << endl;

    root = deleteNode(root, 70);

    cout << "In-order after deletion: ";
    inorder(root);
    cout << endl;

    cout << "Maximum Depth of BST: " << maxDepth(root) << endl;
    cout << "Minimum Depth of BST: " << minDepth(root) << endl;

    return 0;
}
```
---
### Q4. Write a program to determine whether a given binary tree is a BST or not.
```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
};

Node* newNode(int val) {
    Node* n = new Node();
    n->data = val;
    n->left = n->right = NULL;
    return n;
}

bool isBSTUtil(Node* root, int min, int max) {
    if (root == NULL)
        return true;
    if (root->data < min || root->data > max)
        return false;
    return isBSTUtil(root->left, min, root->data - 1) &&
           isBSTUtil(root->right, root->data + 1, max);
}

bool isBST(Node* root) {
    return isBSTUtil(root, -99999, 99999);
}

int main() {
    Node* root = newNode(4);
    root->left = newNode(2);
    root->right = newNode(5);
    root->left->left = newNode(1);
    root->left->right = newNode(3);

    if (isBST(root))
        cout << "Given tree is a BST." << endl;
    else
        cout << "Given tree is NOT a BST." << endl;

    return 0;
}
```
---
