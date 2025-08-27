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
```
---

### Q2. Given a string, reverse it using STACK. For example “DataStructure” should be output as “erutcurtSataD.”

```cpp
#include <iostream>
#include <stack>
#include <string>
using namespace std;

int main() {
    string str;
    cout << "Enter a string: ";
    getline(cin, str);

    stack<char> s;
    for(char c : str) s.push(c);

    cout << "Reversed string: ";
    while(!s.empty()) {
        cout << s.top();
        s.pop();
    }
    cout << endl;
    return 0;
}
```

---

### Q3. Write a program that checks if an expression has balanced parentheses.

```cpp
#include <iostream>
#include <stack>
using namespace std;

bool isBalanced(string expr) {
    stack<char> s;
    for(char c : expr) {
        if(c == '(' || c == '{' || c == '[') s.push(c);
        else if(c == ')' || c == '}' || c == ']') {
            if(s.empty()) return false;
            char top = s.top(); s.pop();
            if((c == ')' && top != '(') ||
               (c == '}' && top != '{') ||
               (c == ']' && top != '['))
                return false;
        }
    }
    return s.empty();
}

int main() {
    string expr;
    cout << "Enter expression: ";
    cin >> expr;
    if(isBalanced(expr)) cout << "Balanced\n";
    else cout << "Not Balanced\n";
}
```

---

### Q4. Write a program to convert an Infix expression into a Postfix expression.

```cpp
#include <iostream>
#include <stack>
#include <cctype>
using namespace std;

int prec(char c) {
    if(c == '^') return 3;
    else if(c == '*' || c == '/') return 2;
    else if(c == '+' || c == '-') return 1;
    else return -1;
}

string infixToPostfix(string s) {
    stack<char> st;
    string result = "";
    for(char c : s) {
        if(isalnum(c)) result += c;
        else if(c == '(') st.push(c);
        else if(c == ')') {
            while(!st.empty() && st.top() != '(') {
                result += st.top(); st.pop();
            }
            st.pop();
        } else {
            while(!st.empty() && prec(st.top()) >= prec(c)) {
                result += st.top(); st.pop();
            }
            st.push(c);
        }
    }
    while(!st.empty()) {
        result += st.top(); st.pop();
    }
    return result;
}

int main() {
    string exp;
    cout << "Enter infix expression: ";
    cin >> exp;
    cout << "Postfix: " << infixToPostfix(exp) << endl;
}
```

---

### Q5. Write a program for the evaluation of a Postfix expression.

```cpp
#include <iostream>
#include <stack>
#include <cctype>
using namespace std;

int evaluatePostfix(string exp) {
    stack<int> st;
    for(char c : exp) {
        if(isdigit(c)) st.push(c - '0');
        else {
            int val2 = st.top(); st.pop();
            int val1 = st.top(); st.pop();
            switch(c) {
                case '+': st.push(val1 + val2); break;
                case '-': st.push(val1 - val2); break;
                case '*': st.push(val1 * val2); break;
                case '/': st.push(val1 / val2); break;
            }
        }
    }
    return st.top();
}

int main() {
    string exp;
    cout << "Enter postfix expression: ";
    cin >> exp;
    cout << "Evaluation: " << evaluatePostfix(exp) << endl;
}
```
---
