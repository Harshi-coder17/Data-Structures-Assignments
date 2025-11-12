# Data Structures Assignment
## Assignment 9

---
### Q1. Implement Heapsort (Increasing/Decreasing order).
```cpp
#include <iostream>
using namespace std;

void maxHeapify(int arr[], int n, int i) {
    int largest = i;
    int l = 2 * i + 1;
    int r = 2 * i + 2;

    if (l < n && arr[l] > arr[largest])
        largest = l;
    if (r < n && arr[r] > arr[largest])
        largest = r;

    if (largest != i) {
        int temp = arr[i];
        arr[i] = arr[largest];
        arr[largest] = temp;
        maxHeapify(arr, n, largest);
    }
}

void heapSortAsc(int arr[], int n) {
    for (int i = n / 2 - 1; i >= 0; i--)
        maxHeapify(arr, n, i);

    for (int i = n - 1; i > 0; i--) {
        swap(arr[0], arr[i]);
        maxHeapify(arr, i, 0);
    }
}

void minHeapify(int arr[], int n, int i) {
    int smallest = i;
    int l = 2 * i + 1;
    int r = 2 * i + 2;

    if (l < n && arr[l] < arr[smallest])
        smallest = l;
    if (r < n && arr[r] < arr[smallest])
        smallest = r;

    if (smallest != i) {
        swap(arr[i], arr[smallest]);
        minHeapify(arr, n, smallest);
    }
}

void heapSortDesc(int arr[], int n) {
    for (int i = n / 2 - 1; i >= 0; i--)
        minHeapify(arr, n, i);

    for (int i = n - 1; i > 0; i--) {
        swap(arr[0], arr[i]);
        minHeapify(arr, i, 0);
    }
}

int main() {
    int arr1[] = {15, 3, 17, 8, 10, 20, 25};
    int arr2[] = {15, 3, 17, 8, 10, 20, 25};
    int n = sizeof(arr1) / sizeof(arr1[0]);

    cout << "Original Array: ";
    for (int i = 0; i < n; i++) cout << arr1[i] << " ";
    cout << "\n";

    heapSortAsc(arr1, n);
    cout << "Sorted (Ascending): ";
    for (int i = 0; i < n; i++) cout << arr1[i] << " ";
    cout << "\n";

    heapSortDesc(arr2, n);
    cout << "Sorted (Descending): ";
    for (int i = 0; i < n; i++) cout << arr2[i] << " ";
    cout << "\n";

    return 0;
}
```
---
### Q2. Implement priority queues using heaps.
```cpp
#include <iostream>
using namespace std;

class PriorityQueue {
    int arr[100];
    int size;

public:
    PriorityQueue() {
        size = 0;
    }

    void insert(int val) {
        if (size >= 100) {
            cout << "Queue Overflow!\n";
            return;
        }
        arr[size] = val;
        int i = size;
        size++;

        while (i > 0 && arr[(i - 1) / 2] < arr[i]) {
            swap(arr[i], arr[(i - 1) / 2]);
            i = (i - 1) / 2;
        }
    }

    void removeMax() {
        if (size <= 0) {
            cout << "Queue Underflow!\n";
            return;
        }
        cout << "Removed element: " << arr[0] << endl;
        arr[0] = arr[size - 1];
        size--;

        int i = 0;
        while (true) {
            int largest = i;
            int l = 2 * i + 1;
            int r = 2 * i + 2;

            if (l < size && arr[l] > arr[largest])
                largest = l;
            if (r < size && arr[r] > arr[largest])
                largest = r;

            if (largest != i) {
                swap(arr[i], arr[largest]);
                i = largest;
            } else break;
        }
    }

    int getMax() {
        if (size == 0) {
            cout << "Queue is empty!\n";
            return -1;
        }
        return arr[0];
    }

    void display() {
        if (size == 0) {
            cout << "Queue is empty!\n";
            return;
        }
        cout << "Priority Queue (Max Heap): ";
        for (int i = 0; i < size; i++)
            cout << arr[i] << " ";
        cout << "\n";
    }
};

int main() {
    PriorityQueue pq;
    int choice, val;

    do {
        cout << "\n--- PRIORITY QUEUE MENU ---\n";
        cout << "1. Insert\n2. Remove Max\n3. Get Max\n4. Display\n5. Exit\n";
        cout << "Enter choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                cout << "Enter value: ";
                cin >> val;
                pq.insert(val);
                break;
            case 2:
                pq.removeMax();
                break;
            case 3:
                cout << "Maximum element: " << pq.getMax() << endl;
                break;
            case 4:
                pq.display();
                break;
            case 5:
                cout << "Exiting...\n";
                break;
            default:
                cout << "Invalid choice.\n";
        }
    } while (choice != 5);

    return 0;
}
```
---
