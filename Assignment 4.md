# Data Structures Assignments
## Assignment 4

---

### Q1. Develop a menu driven program demonstrating the following operations on simple Queues: enqueue(), dequeue(), isEmpty(), isFull(), display(), and peek().
```cpp
#include <iostream>
using namespace std;

#define MAX 100

class Queue {
    int arr[MAX];
    int front, rear;
public:
    Queue() {
        front = -1;
        rear = -1;
    }

    bool isEmpty() {
        return front == -1;
    }

    bool isFull() {
        return rear == MAX - 1;
    }

    void enqueue(int x) {
        if (isFull()) {
            cout << "Queue is full!\n";
            return;
        }
        if (front == -1) front = 0;
        arr[++rear] = x;
    }

    void dequeue() {
        if (isEmpty()) {
            cout << "Queue is empty!\n";
            return;
        }
        cout << "Dequeued: " << arr[front] << endl;
        if (front == rear) front = rear = -1;
        else front++;
    }

    void display() {
        if (isEmpty()) {
            cout << "Queue is empty!\n";
            return;
        }
        cout << "Queue elements: ";
        for (int i = front; i <= rear; i++)
            cout << arr[i] << " ";
        cout << endl;
    }

    void peek() {
        if (isEmpty()) cout << "Queue is empty!\n";
        else cout << "Front element: " << arr[front] << endl;
    }
};

int main() {
    Queue q;
    int choice, val;
    do {
        cout << "\n--- MENU ---\n";
        cout << "1. Enqueue\n2. Dequeue\n3. isEmpty\n4. isFull\n5. Display\n6. Peek\n7. Exit\n";
        cout << "Enter choice: ";
        cin >> choice;
        switch (choice) {
            case 1: cout << "Enter value: "; cin >> val; q.enqueue(val); break;
            case 2: q.dequeue(); break;
            case 3: cout << (q.isEmpty() ? "Queue is empty\n" : "Queue is not empty\n"); break;
            case 4: cout << (q.isFull() ? "Queue is full\n" : "Queue is not full\n"); break;
            case 5: q.display(); break;
            case 6: q.peek(); break;
            case 7: cout << "Exiting...\n"; break;
            default: cout << "Invalid choice!\n";
        }
    } while (choice != 7);
}
```
### Q2. Develop a menu driven program demonstrating the following operations on Circular Queues: enqueue(), dequeue(), isEmpty(), isFull(), display(), and peek().
```cpp
#include <iostream>
using namespace std;

#define MAX 5

class CircularQueue {
    int arr[MAX];
    int front, rear;
public:
    CircularQueue() {
        front = rear = -1;
    }

    bool isEmpty() {
        return front == -1;
    }

    bool isFull() {
        return (front == 0 && rear == MAX - 1) || (rear == (front - 1) % (MAX - 1));
    }

    void enqueue(int x) {
        if (isFull()) {
            cout << "Queue is full!\n";
            return;
        }
        if (front == -1) front = rear = 0;
        else if (rear == MAX - 1 && front != 0) rear = 0;
        else rear++;
        arr[rear] = x;
    }

    void dequeue() {
        if (isEmpty()) {
            cout << "Queue is empty!\n";
            return;
        }
        cout << "Dequeued: " << arr[front] << endl;
        if (front == rear) front = rear = -1;
        else if (front == MAX - 1) front = 0;
        else front++;
    }

    void display() {
        if (isEmpty()) {
            cout << "Queue is empty!\n";
            return;
        }
        cout << "Queue elements: ";
        if (rear >= front) {
            for (int i = front; i <= rear; i++) cout << arr[i] << " ";
        } else {
            for (int i = front; i < MAX; i++) cout << arr[i] << " ";
            for (int i = 0; i <= rear; i++) cout << arr[i] << " ";
        }
        cout << endl;
    }

    void peek() {
        if (isEmpty()) cout << "Queue is empty!\n";
        else cout << "Front element: " << arr[front] << endl;
    }
};

int main() {
    CircularQueue cq;
    int choice, val;
    do {
        cout << "\n--- MENU ---\n";
        cout << "1. Enqueue\n2. Dequeue\n3. isEmpty\n4. isFull\n5. Display\n6. Peek\n7. Exit\n";
        cout << "Enter choice: ";
        cin >> choice;
        switch (choice) {
            case 1: cout << "Enter value: "; cin >> val; cq.enqueue(val); break;
            case 2: cq.dequeue(); break;
            case 3: cout << (cq.isEmpty() ? "Queue is empty\n" : "Queue is not empty\n"); break;
            case 4: cout << (cq.isFull() ? "Queue is full\n" : "Queue is not full\n"); break;
            case 5: cq.display(); break;
            case 6: cq.peek(); break;
            case 7: cout << "Exiting...\n"; break;
            default: cout << "Invalid choice!\n";
        }
    } while (choice != 7);
}
```
### Q3. Write a program interleave the first half of the queue with second half.
#### Sample Input: 4 7 11 20 5 9
#### Sample Output: 4 20 7 5 11 9
```cpp
#include <iostream>
#include <queue>
using namespace std;

void interleaveQueue(queue<int>& q) {
    int n = q.size();
    if (n % 2 != 0) {
        cout << "Queue size must be even!\n";
        return;
    }
    queue<int> firstHalf;
    for (int i = 0; i < n / 2; i++) {
        firstHalf.push(q.front());
        q.pop();
    }
    while (!firstHalf.empty()) {
        q.push(firstHalf.front());
        firstHalf.pop();
        q.push(q.front());
        q.pop();
    }
}

int main() {
    queue<int> q;
    int arr[] = {4, 7, 11, 20, 5, 9};
    for (int x : arr) q.push(x);

    cout << "Original queue: ";
    queue<int> temp = q;
    while (!temp.empty()) {
        cout << temp.front() << " ";
        temp.pop();
    }
    cout << endl;

    interleaveQueue(q);

    cout << "Interleaved queue: ";
    while (!q.empty()) {
        cout << q.front() << " ";
        q.pop();
    }
    cout << endl;
}
```
### Q4. Write a program to find first non-repeating character in a string using Queue.
#### Sample Input: a a b c
#### Sample Output: a -1 b b
```cpp
#include <iostream>
#include <queue>
#include <unordered_map>
using namespace std;

void firstNonRepeating(string str) {
    unordered_map<char, int> freq;
    queue<char> q;

    for (char ch : str) {
        freq[ch]++;
        q.push(ch);

        while (!q.empty() && freq[q.front()] > 1) {
            q.pop();
        }
        if (q.empty()) cout << -1 << " ";
        else cout << q.front() << " ";
    }
    cout << endl;
}

int main() {
    string s = "aabc";
    cout << "Input: " << s << endl;
    cout << "Output: ";
    firstNonRepeating(s);
}
```
### Q5. Write a program to implement a stack using
#### (a) Two queues
#### (b) One queue
```cpp
#include <iostream>
#include <queue>
using namespace std;

// (a) Stack using two queues
class StackTwoQueues {
    queue<int> q1, q2;
public:
    void push(int x) {
        q1.push(x);
    }
    void pop() {
        if (q1.empty()) { cout << "Stack is empty\n"; return; }
        while (q1.size() > 1) {
            q2.push(q1.front());
            q1.pop();
        }
        cout << "Popped: " << q1.front() << endl;
        q1.pop();
        swap(q1, q2);
    }
    void top() {
        if (q1.empty()) { cout << "Stack is empty\n"; return; }
        while (q1.size() > 1) {
            q2.push(q1.front());
            q1.pop();
        }
        cout << "Top: " << q1.front() << endl;
        q2.push(q1.front());
        q1.pop();
        swap(q1, q2);
    }
};

// (b) Stack using one queue
class StackOneQueue {
    queue<int> q;
public:
    void push(int x) {
        q.push(x);
        for (int i = 0; i < q.size() - 1; i++) {
            q.push(q.front());
            q.pop();
        }
    }
    void pop() {
        if (q.empty()) { cout << "Stack is empty\n"; return; }
        cout << "Popped: " << q.front() << endl;
        q.pop();
    }
    void top() {
        if (q.empty()) { cout << "Stack is empty\n"; return; }
        cout << "Top: " << q.front() << endl;
    }
};

int main() {
    cout << "--- Stack using Two Queues ---\n";
    StackTwoQueues s1;
    s1.push(10); s1.push(20); s1.push(30);
    s1.top();
    s1.pop();
    s1.top();

    cout << "\n--- Stack using One Queue ---\n";
    StackOneQueue s2;
    s2.push(5); s2.push(15); s2.push(25);
    s2.top();
    s2.pop();
    s2.top();
}
```
