# Data Structure Assignments  
## Assignment 3  

---

### Q1. Develop a menu driven program demonstrating the following operations on a Stack using array:  
(i) push(), (ii) pop(), (iii) isEmpty(), (iv) isFull(), (v) display(), and (vi) peek().  

```cpp
#include <iostream>
using namespace std;
#define MAX 100

class Stack {
    int arr[MAX];
    int top;
public:
    Stack() { top = -1; }
    bool isEmpty() { return top == -1; }
    bool isFull() { return top == MAX - 1; }
    void push(int x) {
        if (isFull()) cout << "Stack Overflow\n";
        else arr[++top] = x;
    }
    void pop() {
        if (isEmpty()) cout << "Stack Underflow\n";
        else cout << "Popped: " << arr[top--] << endl;
    }
    void peek() {
        if (isEmpty()) cout << "Stack is empty\n";
        else cout << "Top element: " << arr[top] << endl;
    }
    void display() {
        if (isEmpty()) cout << "Stack is empty\n";
        else {
            cout << "Stack elements: ";
            for (int i = top; i >= 0; i--)
                cout << arr[i] << " ";
            cout << endl;
        }
    }
};

int main() {
    Stack st;
    int choice, val;
    do {
        cout << "\n--- MENU ---\n";
        cout << "1. Push\n2. Pop\n3. Peek\n4. isEmpty\n5. isFull\n6. Display\n7. Exit\n";
        cout << "Enter choice: ";
        cin >> choice;
        switch(choice) {
            case 1: cout << "Enter value: "; cin >> val; st.push(val); break;
            case 2: st.pop(); break;
            case 3: st.peek(); break;
            case 4: cout << (st.isEmpty() ? "Stack is empty\n" : "Stack not empty\n"); break;
            case 5: cout << (st.isFull() ? "Stack is full\n" : "Stack not full\n"); break;
            case 6: st.display(); break;
            case 7: cout << "Exiting...\n"; break;
            default: cout << "Invalid choice\n";
        }
    } while(choice != 7);
}

---

### Q2. Given a string, reverse it using STACK. For example “DataStructure” should be output as “erutcurtSataD.”
