# Data Structure Assignments  
## Assignment 2  

---

### Q1. Implement the Binary search algorithm regarded as a fast search algorithm with run-time complexity of Ο(log n) in comparison to the Linear Search.  

```cpp
#include <iostream>
using namespace std;

// Binary Search
int binarysearch(int arr[], int n, int target) {
    int left = 0, right = n - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) return mid;
        else if (arr[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}

// Linear Search
int linearsearch(int arr[], int n, int target) {
    for (int i = 0; i < n; i++)
        if (arr[i] == target) return i;
    return -1;
}

int main() {
    int arr[] = {2,4,6,8,10,12,14,16,18,20};
    int n = sizeof(arr) / sizeof(arr[0]);
    int target;
    cout << "Enter element to search: ";
    cin >> target;

    int Binresult = binarysearch(arr, n, target);
    if (Binresult != -1) cout << "Binary Search: Found at position " << Binresult+1 << endl;
    else cout << "Binary Search: Element not found\n";

    int Linresult = linearsearch(arr, n, target);
    if (Linresult != -1) cout << "Linear Search: Found at position " << Linresult+1 << endl;
    else cout << "Linear Search: Element not found\n";

    return 0;
}
```

---

### Q2. Bubble Sort is the simplest sorting algorithm that works by repeatedly swapping the adjacent elements if they are in wrong order. Code the Bubble sort with the following elements: 64 34 25 12 22 11 90

```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[] = {64,34,25,12,22,11,90};
    int n = sizeof(arr)/sizeof(arr[0]);

    cout << "Input Array: ";
    for(int i=0;i<n;i++) cout << arr[i] << " ";

    for(int i=0;i<n-1;i++) {
        for(int j=0;j<n-i-1;j++) {
            if(arr[j] > arr[j+1]) {
                int temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
            }
        }
    }

    cout << "\nSorted Array: ";
    for(int i=0;i<n;i++) cout << arr[i] << " ";
    return 0;
}
```

---

### Q3. Given an array of n-1 distinct integers in the range of 1 to n, find the missing number in it in a Sorted Array.

#### (a) Linear Time

```cpp
#include <iostream>
using namespace std;

int findMissingLinear(int arr[], int n) {
    int total = (n * (n + 1)) / 2;
    int sum = 0;
    for (int i = 0; i < n - 1; i++) sum += arr[i];
    return total - sum;
}

int main() {
    int arr[] = {1,2,3,5,6}; // missing = 4
    int n = 6;
    cout << "Missing number (Linear method): " << findMissingLinear(arr, n) << endl;
    return 0;
}
```

#### (b) Using Binary Search

```cpp
#include <iostream>
using namespace std;

int findMissingBinary(int arr[], int n, int start) {
    int left = 0, right = n - 1;
    while (left <= right) {
        int mid = (left + right) / 2;
        if (arr[mid] == start + mid) left = mid + 1;
        else right = mid - 1;
    }
    return start + left;
}

int main() {
    int arr[] = {4,5,6,8,9}; // missing = 7
    int n = 5, start = arr[0];
    cout << "Missing number (Binary method): " << findMissingBinary(arr, n, start) << endl;
    return 0;
}
```

---

### Q4. String Related Programs

#### (a) Concatenate one string to another string.

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str1, str2;
    cout << "Enter first string: ";
    getline(cin, str1);
    cout << "Enter second string: ";
    getline(cin, str2);

    str1 = str1 + str2;

    cout << "Concatenated string: " << str1 << endl;
    return 0;
}
```

#### (b) Reverse a string.

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str;
    cout << "Enter a string: ";
    getline(cin, str);

    int n = str.length();
    for (int i = 0; i < n/2; i++) {
        char temp = str[i];
        str[i] = str[n-i-1];
        str[n-i-1] = temp;
    }

    cout << "Reversed string: " << str << endl;
    return 0;
}
```

#### (c) Delete all the vowels from the string.

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str, result="";
    cout << "Enter a string: ";
    getline(cin, str);

    for (int i=0;i<str.length();i++) {
        char c = str[i];
        if (!(c=='a'||c=='e'||c=='i'||c=='o'||c=='u'||c=='A'||c=='E'||c=='I'||c=='O'||c=='U'))
            result += c;
    }

    cout << "String without vowels: " << result << endl;
    return 0;
}
```

#### (d) Sort the strings in alphabetical order.

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    int n;
    cout << "Enter number of strings: ";
    cin >> n;
    cin.ignore();
    string arr[n];
    cout << "Enter " << n << " strings:\n";
    for (int i=0;i<n;i++) getline(cin, arr[i]);

    for (int i=0;i<n-1;i++) {
        for (int j=0;j<n-i-1;j++) {
            if (arr[j] > arr[j+1]) {
                string temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
            }
        }
    }

    cout << "Sorted strings:\n";
    for (int i=0;i<n;i++) cout << arr[i] << endl;
    return 0;
}
```

#### (e) Convert a character from uppercase to lowercase.

```cpp
#include <iostream>
using namespace std;

int main() {
    char c;
    cout << "Enter a character: ";
    cin >> c;

    if (c >= 'A' && c <= 'Z') c = c + 32;
    cout << "Lowercase character: " << c << endl;
    return 0;
}
```

---

### Q5. Space-efficient storage for special matrices.

#### (a) Diagonal Matrix

```cpp
#include <iostream>
using namespace std;

int main() {
    int n;
    cout << "Enter order of diagonal matrix: ";
    cin >> n;

    int D[100];
    cout << "Enter diagonal elements:\n";
    for (int i=0;i<n;i++) cin >> D[i];

    cout << "Diagonal Matrix:\n";
    for (int i=0;i<n;i++) {
        for (int j=0;j<n;j++) {
            if (i==j) cout << D[i] << " ";
            else cout << 0 << " ";
        }
        cout << "\n";
    }
    return 0;
}
```

#### (b) Tri-diagonal Matrix

```cpp
#include <iostream>
using namespace std;

int main() {
    int n;
    cout << "Enter order of tri-diagonal matrix: ";
    cin >> n;

    int D[100], U[100], L[100];
    cout << "Enter main diagonal:\n";
    for (int i=0;i<n;i++) cin >> D[i];
    cout << "Enter upper diagonal:\n";
    for (int i=0;i<n-1;i++) cin >> U[i];
    cout << "Enter lower diagonal:\n";
    for (int i=0;i<n-1;i++) cin >> L[i];

    cout << "Tri-diagonal Matrix:\n";
    for (int i=0;i<n;i++) {
        for (int j=0;j<n;j++) {
            if (i==j) cout << D[i] << " ";
            else if (j==i+1) cout << U[i] << " ";
            else if (i==j+1) cout << L[j] << " ";
            else cout << 0 << " ";
        }
        cout << "\n";
    }
    return 0;
}
```

#### (c) Lower Triangular Matrix

```cpp
#include <iostream>
using namespace std;

int main() {
    int n;
    cout << "Enter order of lower triangular matrix: ";
    cin >> n;

    int A[100][100];
    cout << "Enter lower triangular elements row-wise:\n";
    for (int i=0;i<n;i++)
        for (int j=0;j<=i;j++) cin >> A[i][j];

    cout << "Lower Triangular Matrix:\n";
    for (int i=0;i<n;i++) {
        for (int j=0;j<n;j++) {
            if (j<=i) cout << A[i][j] << " ";
            else cout << 0 << " ";
        }
        cout << "\n";
    }
    return 0;
}
```

#### (d) Upper Triangular Matrix

```cpp
#include <iostream>
using namespace std;

int main() {
    int n;
    cout << "Enter order of upper triangular matrix: ";
    cin >> n;

    int A[100][100];
    cout << "Enter upper triangular elements row-wise:\n";
    for (int i=0;i<n;i++)
        for (int j=i;j<n;j++) cin >> A[i][j];

    cout << "Upper Triangular Matrix:\n";
    for (int i=0;i<n;i++) {
        for (int j=0;j<n;j++) {
            if (j>=i) cout << A[i][j] << " ";
            else cout << 0 << " ";
        }
        cout << "\n";
    }
    return 0;
}
```

#### (e) Symmetric Matrix

```cpp
#include <iostream>
using namespace std;

int main() {
    int n;
    cout << "Enter order of symmetric matrix: ";
    cin >> n;

    int A[100][100];
    cout << "Enter lower triangle (including diagonal):\n";
    for (int i=0;i<n;i++) {
        for (int j=0;j<=i;j++) {
            cin >> A[i][j];
            A[j][i] = A[i][j];
        }
    }

    cout << "Symmetric Matrix:\n";
    for (int i=0;i<n;i++) {
        for (int j=0;j<n;j++) cout << A[i][j] << " ";
        cout << "\n";
    }
    return 0;
}
```

---

### Q6. Sparse Matrix Operations (Triplet Representation)

#### (a) Transpose

```cpp
#include <iostream>
using namespace std;

struct Term {
    int row, col, val;
};

int main() {
    int r, c, n;
    cout << "Enter rows, cols and non-zero count: ";
    cin >> r >> c >> n;

    Term A[100], T[100];
    cout << "Enter triplets (row col value):\n";
    for (int i = 0; i < n; i++) cin >> A[i].row >> A[i].col >> A[i].val;

    for (int i = 0; i < n; i++) {
        T[i].row = A[i].col;
        T[i].col = A[i].row;
        T[i].val = A[i].val;
    }

    cout << "Transpose triplets:\n";
    for (int i = 0; i < n; i++)
        cout << T[i].row << " " << T[i].col << " " << T[i].val << "\n";

    return 0;
}
```

#### (b) Addition

```cpp
#include <iostream>
using namespace std;

struct Term { int row, col, val; };

int main() {
    int n1, n2;
    cout << "Enter number of non-zero terms in A: ";
    cin >> n1;
    Term A[100];
    cout << "Enter triplets of A:\n";
    for (int i = 0; i < n1; i++) cin >> A[i].row >> A[i].col >> A[i].val;

    cout << "Enter number of non-zero terms in B: ";
    cin >> n2;
    Term B[100];
    cout << "Enter triplets of B:\n";
    for (int i = 0; i < n2; i++) cin >> B[i].row >> B[i].col >> B[i].val;

    Term C[200];
    int k = 0;
    int i = 0, j = 0;
    while (i < n1 && j < n2) {
        if (A[i].row == B[j].row && A[i].col == B[j].col) {
            C[k].row = A[i].row;
            C[k].col = A[i].col;
            C[k].val = A[i].val + B[j].val;
            i++; j++; k++;
        } else if (A[i].row < B[j].row || (A[i].row == B[j].row && A[i].col < B[j].col)) {
            C[k++] = A[i++];
        } else {
            C[k++] = B[j++];
        }
    }
    while (i < n1) C[k++] = A[i++];
    while (j < n2) C[k++] = B[j++];

    cout << "Addition result triplets:\n";
    for (int x = 0; x < k; x++)
        cout << C[x].row << " " << C[x].col << " " << C[x].val << "\n";

    return 0;
}
```

#### (c) Multiplication

```cpp
#include <iostream>
using namespace std;

struct Term { int row, col, val; };

int main() {
    int n1, n2;
    cout << "Enter number of non-zero terms in A: ";
    cin >> n1;
    Term A[100];
    cout << "Enter triplets of A:\n";
    for (int i = 0; i < n1; i++) cin >> A[i].row >> A[i].col >> A[i].val;

    cout << "Enter number of non-zero terms in B: ";
    cin >> n2;
    Term B[100];
    cout << "Enter triplets of B:\n";
    for (int i = 0; i < n2; i++) cin >> B[i].row >> B[i].col >> B[i].val;

    Term C[200];
    int k = 0;
    for (int i = 0; i < n1; i++) {
        for (int j = 0; j < n2; j++) {
            if (A[i].col == B[j].row) {
                int found = -1;
                for (int x = 0; x < k; x++) {
                    if (C[x].row == A[i].row && C[x].col == B[j].col) {
                        found = x; break;
                    }
                }
                if (found != -1) {
                    C[found].val += A[i].val * B[j].val;
                } else {
                    C[k].row = A[i].row;
                    C[k].col = B[j].col;
                    C[k].val = A[i].val * B[j].val;
                    k++;
                }
            }
        }
    }

    cout << "Multiplication result triplets:\n";
    for (int x = 0; x < k; x++)
        cout << C[x].row << " " << C[x].col << " " << C[x].val << "\n";

    return 0;
}
```

---

### Q7. Count number of inversions in an array.

```cpp
#include <iostream>
using namespace std;

int main() {
    int n;
    cout << "Enter size of array: ";
    cin >> n;
    int A[100];
    cout << "Enter elements:\n";
    for (int i = 0; i < n; i++) cin >> A[i];

    int count = 0;
    for (int i = 0; i < n; i++) {
        for (int j = i+1; j < n; j++) {
            if (A[i] > A[j]) count++;
        }
    }
    cout << "Number of inversions = " << count << "\n";
    return 0;
}
```

---

### Q8. Count the total number of distinct elements in an array of length n.

```cpp
#include <iostream>
using namespace std;

int main() {
    int n;
    cout << "Enter size of array: ";
    cin >> n;
    int A[100];
    cout << "Enter elements:\n";
    for (int i = 0; i < n; i++) cin >> A[i];

    int count = 0;
    for (int i = 0; i < n; i++) {
        bool seen = false;
        for (int j = 0; j < i; j++) {
            if (A[i] == A[j]) {
                seen = true; break;
            }
        }
        if (!seen) count++;
    }
    cout << "Number of distinct elements = " << count << "\n";
    return 0;
}
```

---
