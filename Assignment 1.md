# Data Structure Assignments
## Assignment 1

---

### Q1. Write a menu-driven program to perform the following operations on an array: create, display, insert, delete and linear search.

```cpp
#include <iostream>
using namespace std;

#define MAX 100

int arr[MAX];
int n = 0;

void create() {
    cout << "Enter number of elements: ";
    cin >> n;
    cin.ignore();
    cout << "Enter " << n << " elements:\n";
    for(int i = 0; i < n; i++)
        cin >> arr[i];
}

void display() {
    if(n == 0) {
        cout << "Array is empty.\n";
        return;
    }
    cout << "Array elements: ";
    for(int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;
}

void insertElement() {
    if(n == MAX) {
        cout << "Array is full.\n";
        return;
    }
    int pos, val;
    cout << "Enter position (0-" << n << "): ";
    cin >> pos;
    cout << "Enter value: ";
    cin >> val;
    for(int i = n; i > pos; i--)
        arr[i] = arr[i - 1];
    arr[pos] = val;
    n++;
}

void deleteElement() {
    if(n == 0) {
        cout << "Array is empty.\n";
        return;
    }
    int pos;
    cout << "Enter position (0-" << n-1 << "): ";
    cin >> pos;
    for(int i = pos; i < n - 1; i++)
        arr[i] = arr[i + 1];
    n--;
}

void linearSearch() {
    int key;
    cout << "Enter value to search: ";
    cin >> key;
    for(int i = 0; i < n; i++) {
        if(arr[i] == key) {
            cout << "Element found at position " << i << endl;
            return;
        }
    }
    cout << "Element not found.\n";
}

int main() {
    int choice;
    do{
        cout << "\n--- MENU ---\n";
        cout << "1. CREATE\n";
        cout << "2. DISPLAY\n";
        cout << "3. INSERT\n";
        cout << "4. DELETE\n";
        cout << "5. LINEAR SEARCH\n";
        cout << "6. EXIT\n";
        cout << "Enter choice: ";
        cin >> choice;
        cin.ignore();

        switch(choice) {
            case 1: create(); break;
            case 2: display(); break;
            case 3: insertElement(); break;
            case 4: deleteElement(); break;
            case 5: linearSearch(); break;
            case 6: cout<<"Exiting Program..\n";
                break;
            default: cout << "Invalid choice. Try Again..\n";
        }
    }while(choice !=6);
}
```

---

### Q2. Write a program to remove duplicate elements from an array.

```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[100], n;
    cout << "Enter number of elements: ";
    cin >> n;

    cout << "Enter " << n << " elements:\n";
    for(int i = 0; i < n; i++)
        cin >> arr[i];

    for(int i = 0; i < n; i++) {
        for(int j = i + 1; j < n; j++) {
            if(arr[i] == arr[j]) {
                for(int k = j; k < n - 1; k++)
                    arr[k] = arr[k + 1];
                n--;
                j--;
            }
        }
    }

    cout << "Array after removing duplicates: ";
    for(int i = 0; i < n; i++)
        cout << arr[i] << " ";
}
```

---

### Q3. What is the output of the following code?

```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[5] = {1};
    for (int i = 0; i < 5; i++)
        cout << arr[i];
    return 0;
}
// Output: 10000
```

---

### Q4a. Write a program to reverse an array.

```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[100], n;
    cout << "Enter number of elements: ";
    cin >> n;
    cout << "Enter " << n << " elements:\n";
    for(int i = 0; i < n; i++)
        cin >> arr[i];

    for(int i = 0; i < n / 2; i++) {
        int temp = arr[i];
        arr[i] = arr[n - i - 1];
        arr[n - i - 1] = temp;
    }

    cout << "Reversed array: ";
    for(int i = 0; i < n; i++)
        cout << arr[i] << " ";
}
```

---

### Q4b. Write a program for matrix multiplication.

```cpp
#include <iostream>
using namespace std;

int main() {
    int a[10][10], b[10][10], c[10][10];
    int n, m, p, q;

    cout << "Enter rows and coloumns of first matrix: ";
    cin >> n >> m;
    cout << "Enter rows and coloumns of second matrix: ";
    cin >> p >> q;

    if(m != p) {
        cout << "Matrix multiplication not possible.\n";
        return 0;
    }

    cout << "Enter first matrix:\n";
    for(int i = 0; i < n; i++)
        for(int j = 0; j < m; j++)
            cin >> a[i][j];

    cout << "Enter second matrix:\n";
    for(int i = 0; i < p; i++)
        for(int j = 0; j < q; j++)
            cin >> b[i][j];

    for(int i = 0; i < n; i++)
        for(int j = 0; j < q; j++) {
            c[i][j] = 0;
            for(int k = 0; k < m; k++)
                c[i][j] += a[i][k] * b[k][j];
        }

    cout << "1st matrix:\n";
    for(int i = 0; i < n; i++) {
        for(int j = 0; j < m; j++)
            cout << a[i][j] << " ";
        cout << endl;
    }

    cout << "2nd matrix:\n";
    for(int i = 0; i < p; i++) {
        for(int j = 0; j < q; j++)
            cout << b[i][j] << " ";
        cout << endl;
    }

    cout << "Resultant matrix:\n";
    for(int i = 0; i < n; i++) {
        for(int j = 0; j < q; j++)
            cout << c[i][j] << " ";
        cout << endl;
    }
}
```

---

### Q4c. Write a program to find transpose of a matrix.

```cpp
#include <iostream>
using namespace std;

int main() {
    int a[10][10], trans[10][10], r, c;
    cout << "Enter rows and coloumns: ";
    cin >> r >> c;

    cout << "Enter matrix:\n";
    for(int i = 0; i < r; i++)
        for(int j = 0; j < c; j++)
            cin >> a[i][j];

    for(int i = 0; i < r; i++)
        for(int j = 0; j < c; j++)
            trans[j][i] = a[i][j];

    cout << "Entered Matrix:\n";
    for(int i = 0; i < r; i++) {
        for(int j = 0; j < c; j++)
            cout << a[i][j] << " ";
        cout << endl;
    }

    cout << "Transpose:\n";
    for(int i = 0; i < c; i++) {
        for(int j = 0; j < r; j++)
            cout << trans[i][j] << " ";
        cout << endl;
    }
}
```

---

### Q5. Write a program to find the sum of each row and column of a matrix.

```cpp
#include <iostream>
using namespace std;

int main() {
    int a[10][10], r, c;
    cout << "Enter rows and coloumns: ";
    cin >> r >> c;

    cout << "Enter matrix:\n";
    for(int i = 0; i < r; i++)
        for(int j = 0; j < c; j++)
            cin >> a[i][j];

    for(int i = 0; i < r; i++) {
        int sum = 0;
        for(int j = 0; j < c; j++)
            sum += a[i][j];
        cout << "Sum of row " << i+1 << " = " << sum << endl;
    }

    for(int j = 0; j < c; j++) {
        int sum = 0;
        for(int i = 0; i < r; i++)
            sum += a[i][j];
        cout << "Sum of column " << j+1 << " = " << sum << endl;
    }
}
```

