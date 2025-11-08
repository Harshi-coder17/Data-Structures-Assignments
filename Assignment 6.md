# Data Structures Assignment
## Assignment 6

---
### Q1. Develop a menu-driven program for the following operations on a Circular as well as a Doubly Linked List:
#### (a) Insertion anywhere (first, last, before/after a specific node)
#### (b) Deletion of a specific node
#### (c) Search for a node

```cpp
#include <iostream>
using namespace std;

// Doubly Linked List Node
struct Node {
    int data;
    Node* prev;
    Node* next;
};

Node* head = NULL;

// Insert at beginning
void insertAtBeginning(int val) {
    Node* newNode = new Node();
    newNode->data = val;
    newNode->prev = NULL;
    newNode->next = head;
    if (head != NULL)
        head->prev = newNode;
    head = newNode;
}

// Insert at end
void insertAtEnd(int val) {
    Node* newNode = new Node();
    newNode->data = val;
    newNode->next = NULL;
    if (head == NULL) {
        newNode->prev = NULL;
        head = newNode;
        return;
    }
    Node* temp = head;
    while (temp->next != NULL)
        temp = temp->next;
    temp->next = newNode;
    newNode->prev = temp;
}

// Insert after specific value
void insertAfter(int key, int val) {
    Node* temp = head;
    while (temp != NULL && temp->data != key)
        temp = temp->next;
    if (temp == NULL) {
        cout << "Node not found!\n";
        return;
    }
    Node* newNode = new Node();
    newNode->data = val;
    newNode->next = temp->next;
    newNode->prev = temp;
    if (temp->next != NULL)
        temp->next->prev = newNode;
    temp->next = newNode;
}

// Delete node by value
void deleteNode(int key) {
    Node* temp = head;
    while (temp != NULL && temp->data != key)
        temp = temp->next;
    if (temp == NULL) {
        cout << "Node not found!\n";
        return;
    }
    if (temp->prev != NULL)
        temp->prev->next = temp->next;
    else
        head = temp->next;
    if (temp->next != NULL)
        temp->next->prev = temp->prev;
    delete temp;
    cout << "Node deleted.\n";
}

// Search a node
void search(int key) {
    Node* temp = head;
    int pos = 1;
    while (temp != NULL) {
        if (temp->data == key) {
            cout << "Node " << key << " found at position " << pos << endl;
            return;
        }
        temp = temp->next;
        pos++;
    }
    cout << "Node not found!\n";
}

// Display list
void display() {
    Node* temp = head;
    cout << "List: ";
    while (temp != NULL) {
        cout << temp->data << " <-> ";
        temp = temp->next;
    }
    cout << "NULL\n";
}

int main() {
    int choice, val, key;
    do {
        cout << "\n--- DOUBLY LINKED LIST MENU ---\n";
        cout << "1. Insert at Beginning\n2. Insert at End\n3. Insert After Node\n";
        cout << "4. Delete Node\n5. Search Node\n6. Display\n7. Exit\n";
        cout << "Enter choice: ";
        cin >> choice;

        switch (choice) {
            case 1: cout << "Enter value: "; cin >> val; insertAtBeginning(val); break;
            case 2: cout << "Enter value: "; cin >> val; insertAtEnd(val); break;
            case 3: cout << "Enter key and value: "; cin >> key >> val; insertAfter(key, val); break;
            case 4: cout << "Enter value to delete: "; cin >> val; deleteNode(val); break;
            case 5: cout << "Enter value to search: "; cin >> val; search(val); break;
            case 6: display(); break;
            case 7: cout << "Exiting...\n"; break;
            default: cout << "Invalid choice!\n";
        }
    } while (choice != 7);
}
```

---
### Q2. Display all node values in a circular linked list, repeating the head node at the end.
#### Example: For 20 → 100 → 40 → 80 → 60, output should be 20 100 40 80 60 20.

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
};

Node* head = NULL;

// Create circular linked list
void insertEnd(int val) {
    Node* newNode = new Node();
    newNode->data = val;
    if (head == NULL) {
        head = newNode;
        newNode->next = head;
        return;
    }
    Node* temp = head;
    while (temp->next != head)
        temp = temp->next;
    temp->next = newNode;
    newNode->next = head;
}

void displayCircular() {
    if (head == NULL) {
        cout << "List is empty!\n";
        return;
    }
    Node* temp = head;
    do {
        cout << temp->data << " ";
        temp = temp->next;
    } while (temp != head);
    cout << head->data << endl; // repeat head value at end
}

int main() {
    insertEnd(20); insertEnd(100); insertEnd(40); insertEnd(80); insertEnd(60);
    cout << "Circular Linked List: ";
    displayCircular();
}
```

---
### Q3. Write a program to find the size of
#### (i) Doubly Linked List
#### (ii) Circular Linked List

```cpp
#include <iostream>
using namespace std;

struct DNode {
    int data;
    DNode* next;
    DNode* prev;
};
struct CNode {
    int data;
    CNode* next;
};

DNode* headD = NULL;
CNode* headC = NULL;

void insertD(int val) {
    DNode* n = new DNode();
    n->data = val;
    n->next = headD;
    n->prev = NULL;
    if (headD != NULL) headD->prev = n;
    headD = n;
}

void insertC(int val) {
    CNode* n = new CNode();
    n->data = val;
    if (headC == NULL) {
        headC = n;
        n->next = headC;
        return;
    }
    CNode* temp = headC;
    while (temp->next != headC) temp = temp->next;
    temp->next = n;
    n->next = headC;
}

int sizeD() {
    int count = 0;
    DNode* temp = headD;
    while (temp != NULL) {
        count++;
        temp = temp->next;
    }
    return count;
}

int sizeC() {
    if (headC == NULL) return 0;
    int count = 0;
    CNode* temp = headC;
    do {
        count++;
        temp = temp->next;
    } while (temp != headC);
    return count;
}

int main() {
    insertD(1); insertD(2); insertD(3);
    insertC(10); insertC(20); insertC(30);
    cout << "Size of Doubly Linked List: " << sizeD() << endl;
    cout << "Size of Circular Linked List: " << sizeC() << endl;
}
```

---
### Q4. Write a program to check if a doubly linked list of characters is palindrome or not.

```cpp
#include <iostream>
using namespace std;

struct Node {
    char data;
    Node* next;
    Node* prev;
};

Node* head = NULL;

void insert(char ch) {
    Node* n = new Node();
    n->data = ch;
    n->next = head;
    n->prev = NULL;
    if (head != NULL)
        head->prev = n;
    head = n;
}

bool isPalindrome() {
    if (head == NULL) return true;
    Node* left = head;
    Node* right = head;
    while (right->next != NULL)
        right = right->next;

    while (left != right && right->next != left) {
        if (left->data != right->data)
            return false;
        left = left->next;
        right = right->prev;
    }
    return true;
}

int main() {
    string s = "MADAM";
    for (char c : s) insert(c);
    if (isPalindrome()) cout << "Palindrome\n";
    else cout << "Not Palindrome\n";
}
```

---
### Q5. Write a program to check if a linked list is Circular Linked List or not.

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
};

bool isCircular(Node* head) {
    if (head == NULL) return false;
    Node* temp = head->next;
    while (temp != NULL && temp != head)
        temp = temp->next;
    return (temp == head);
}

int main() {
    Node* head = new Node();
    Node* second = new Node();
    Node* third = new Node();

    head->data = 1;
    second->data = 2;
    third->data = 3;

    head->next = second;
    second->next = third;
    third->next = head; // make it circular

    if (isCircular(head))
        cout << "Linked list is circular.\n";
    else
        cout << "Linked list is not circular.\n";
}
```
---
