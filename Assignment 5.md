# Data Structures Assignment
## Assignment 5

---

### Q1. Develop a menu driven program for the following operations on a Singly Linked List:
#### (a) Insertion at the beginning
#### (b) Insertion at the end
#### (c) Insertion in between (before or after a node with specific value)
#### (d) Deletion from the beginning
#### (e) Deletion from the end
#### (f) Deletion of a specific node
#### (g) Search for a node and display its position
#### (h) Display all node values

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
};

Node* head = NULL;

void insertAtBeginning(int val) {
    Node* newNode = new Node();
    newNode->data = val;
    newNode->next = head;
    head = newNode;
}

void insertAtEnd(int val) {
    Node* newNode = new Node();
    newNode->data = val;
    newNode->next = NULL;
    if (head == NULL) {
        head = newNode;
        return;
    }
    Node* temp = head;
    while (temp->next != NULL) temp = temp->next;
    temp->next = newNode;
}

void insertBeforeValue(int val, int beforeVal) {
    if (head == NULL) return;
    if (head->data == beforeVal) {
        insertAtBeginning(val);
        return;
    }
    Node* temp = head;
    while (temp->next != NULL && temp->next->data != beforeVal)
        temp = temp->next;
    if (temp->next == NULL) {
        cout << "Value not found!\n";
        return;
    }
    Node* newNode = new Node();
    newNode->data = val;
    newNode->next = temp->next;
    temp->next = newNode;
}

void insertAfterValue(int val, int afterVal) {
    Node* temp = head;
    while (temp != NULL && temp->data != afterVal)
        temp = temp->next;
    if (temp == NULL) {
        cout << "Value not found!\n";
        return;
    }
    Node* newNode = new Node();
    newNode->data = val;
    newNode->next = temp->next;
    temp->next = newNode;
}

void deleteFromBeginning() {
    if (head == NULL) return;
    Node* temp = head;
    head = head->next;
    delete temp;
}

void deleteFromEnd() {
    if (head == NULL) return;
    if (head->next == NULL) {
        delete head;
        head = NULL;
        return;
    }
    Node* temp = head;
    while (temp->next->next != NULL) temp = temp->next;
    delete temp->next;
    temp->next = NULL;
}

void deleteValue(int val) {
    if (head == NULL) return;
    if (head->data == val) {
        Node* temp = head;
        head = head->next;
        delete temp;
        return;
    }
    Node* temp = head;
    while (temp->next != NULL && temp->next->data != val)
        temp = temp->next;
    if (temp->next == NULL) {
        cout << "Value not found!\n";
        return;
    }
    Node* toDelete = temp->next;
    temp->next = temp->next->next;
    delete toDelete;
}

void searchNode(int val) {
    Node* temp = head;
    int pos = 1;
    while (temp != NULL) {
        if (temp->data == val) {
            cout << "Node " << val << " found at position " << pos << endl;
            return;
        }
        temp = temp->next;
        pos++;
    }
    cout << "Value not found!\n";
}

void display() {
    Node* temp = head;
    if (temp == NULL) {
        cout << "List is empty!\n";
        return;
    }
    cout << "Linked List: ";
    while (temp != NULL) {
        cout << temp->data << " -> ";
        temp = temp->next;
    }
    cout << "NULL\n";
}

int main() {
    int choice, val, key;
    do {
        cout << "\n--- MENU ---\n";
        cout << "1. Insert at beginning\n2. Insert at end\n3. Insert before value\n4. Insert after value\n";
        cout << "5. Delete from beginning\n6. Delete from end\n7. Delete a specific node\n";
        cout << "8. Search for a node\n9. Display\n10. Exit\n";
        cout << "Enter choice: ";
        cin >> choice;
        switch (choice) {
            case 1: cout << "Enter value: "; cin >> val; insertAtBeginning(val); break;
            case 2: cout << "Enter value: "; cin >> val; insertAtEnd(val); break;
            case 3: cout << "Enter value and before which value: "; cin >> val >> key; insertBeforeValue(val, key); break;
            case 4: cout << "Enter value and after which value: "; cin >> val >> key; insertAfterValue(val, key); break;
            case 5: deleteFromBeginning(); break;
            case 6: deleteFromEnd(); break;
            case 7: cout << "Enter value to delete: "; cin >> val; deleteValue(val); break;
            case 8: cout << "Enter value to search: "; cin >> val; searchNode(val); break;
            case 9: display(); break;
            case 10: cout << "Exiting...\n"; break;
            default: cout << "Invalid choice!\n";
        }
    } while (choice != 10);
}
```

---

### Q2. Write a program to count the number of occurrences of a given key in a singly linked list and then delete all the occurrences. For example, if given linked list is 1->2->1->2->1->3->1 and given key is 1, then output should be 4. After deletion of all the occurrences of 1, the linked list is 2->2->3.

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
};
Node* head = NULL;

void insert(int val) {
    Node* newNode = new Node();
    newNode->data = val;
    newNode->next = head;
    head = newNode;
}

int countAndDeleteOccurrences(int key) {
    int count = 0;
    while (head != NULL && head->data == key) {
        Node* temp = head;
        head = head->next;
        delete temp;
        count++;
    }
    Node* curr = head;
    while (curr != NULL && curr->next != NULL) {
        if (curr->next->data == key) {
            Node* temp = curr->next;
            curr->next = curr->next->next;
            delete temp;
            count++;
        } else {
            curr = curr->next;
        }
    }
    return count;
}

void display() {
    Node* temp = head;
    while (temp != NULL) {
        cout << temp->data << " -> ";
        temp = temp->next;
    }
    cout << "NULL\n";
}

int main() {
    insert(1); insert(3); insert(1); insert(2); insert(1); insert(2); insert(1);
    cout << "Original list: "; display();
    int key = 1;
    int count = countAndDeleteOccurrences(key);
    cout << "Key " << key << " occurred " << count << " times.\n";
    cout << "Updated list: "; display();
}

```
---

### Q3. Write a program to find the middle of a linked list.
#### Input: 1->2->3->4->5
#### Output- 3

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
};
Node* head = NULL;

void insert(int val) {
    Node* newNode = new Node();
    newNode->data = val;
    newNode->next = head;
    head = newNode;
}

void findMiddle() {
    if (head == NULL) return;
    Node* slow = head;
    Node* fast = head;
    while (fast != NULL && fast->next != NULL) {
        slow = slow->next;
        fast = fast->next->next;
    }
    cout << "Middle node: " << slow->data << endl;
}

int main() {
    insert(5); insert(4); insert(3); insert(2); insert(1);
    cout << "Linked List: 1->2->3->4->5\n";
    findMiddle();
}

```
---

### Q4. Write a program to reverse a linked list.
#### Input: 1->2->3->4->NULL
#### Output: 4->3->2->1->NULL

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
};
Node* head = NULL;

void insert(int val) {
    Node* newNode = new Node();
    newNode->data = val;
    newNode->next = head;
    head = newNode;
}

void reverseList() {
    Node* prev = NULL;
    Node* curr = head;
    Node* next = NULL;
    while (curr != NULL) {
        next = curr->next;
        curr->next = prev;
        prev = curr;
        curr = next;
    }
    head = prev;
}

void display() {
    Node* temp = head;
    while (temp != NULL) {
        cout << temp->data << " -> ";
        temp = temp->next;
    }
    cout << "NULL\n";
}

int main() {
    insert(4); insert(3); insert(2); insert(1);
    cout << "Original list: "; display();
    reverseList();
    cout << "Reversed list: "; display();
}

```
---
