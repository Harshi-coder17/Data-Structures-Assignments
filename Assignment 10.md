# Data Structures Assignment
## Assignment 10

---
### Q1. Write a program to represent a graph using adjacency matrix/list and perform basic operations like degree (in/out) of a vertex, adjacent vertices, number of edges, etc.
```cpp
#include <iostream>
using namespace std;

int main() {
    int n;
    cout << "Enter number of vertices: ";
    cin >> n;

    int adj[20][20] = {0};
    int e;
    cout << "Enter number of edges: ";
    cin >> e;

    cout << "Enter edges (u v):\n";
    for (int i = 0; i < e; i++) {
        int u, v;
        cin >> u >> v;
        adj[u][v] = 1;
        adj[v][u] = 1; // for undirected graph
    }

    cout << "\nAdjacency Matrix:\n";
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++)
            cout << adj[i][j] << " ";
        cout << "\n";
    }

    cout << "\nDegrees of vertices:\n";
    for (int i = 0; i < n; i++) {
        int deg = 0;
        for (int j = 0; j < n; j++)
            deg += adj[i][j];
        cout << "Vertex " << i << " → Degree: " << deg << endl;
    }

    cout << "\nAdjacent vertices:\n";
    for (int i = 0; i < n; i++) {
        cout << "Vertex " << i << " → ";
        for (int j = 0; j < n; j++) {
            if (adj[i][j]) cout << j << " ";
        }
        cout << endl;
    }

    cout << "\nTotal edges in graph: " << e << endl;
    return 0;
}

```
---
### Q2. Write a program to implement breadth first search algorithm.
```cpp
#include <iostream>
using namespace std;

void BFS(int adj[20][20], int n, int start) {
    int visited[20] = {0}, queue[20];
    int front = 0, rear = 0;

    visited[start] = 1;
    queue[rear++] = start;

    cout << "BFS Traversal: ";

    while (front < rear) {
        int node = queue[front++];
        cout << node << " ";

        for (int i = 0; i < n; i++) {
            if (adj[node][i] && !visited[i]) {
                visited[i] = 1;
                queue[rear++] = i;
            }
        }
    }
    cout << endl;
}

int main() {
    int n;
    cout << "Enter number of vertices: ";
    cin >> n;

    int adj[20][20];
    cout << "Enter adjacency matrix:\n";
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            cin >> adj[i][j];

    int start;
    cout << "Enter starting vertex: ";
    cin >> start;

    BFS(adj, n, start);
    return 0;
}

```
---
### Q3. Write a program to implement depth first search algorithm.
```cpp
#include <iostream>
using namespace std;

void DFS(int adj[20][20], int n, int start, int visited[]) {
    cout << start << " ";
    visited[start] = 1;

    for (int i = 0; i < n; i++) {
        if (adj[start][i] && !visited[i])
            DFS(adj, n, i, visited);
    }
}

int main() {
    int n;
    cout << "Enter number of vertices: ";
    cin >> n;

    int adj[20][20];
    cout << "Enter adjacency matrix:\n";
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            cin >> adj[i][j];

    int start;
    cout << "Enter starting vertex: ";
    cin >> start;

    int visited[20] = {0};
    cout << "DFS Traversal: ";
    DFS(adj, n, start, visited);
    cout << endl;

    return 0;
}

```
---
### Q4. Write a program to implement kruskal's minimum spanning tree algorithm.
```cpp
#include <iostream>
using namespace std;

int findParent(int parent[], int i) {
    if (parent[i] == i)
        return i;
    return findParent(parent, parent[i]);
}

void unionSet(int parent[], int x, int y) {
    int xroot = findParent(parent, x);
    int yroot = findParent(parent, y);
    parent[xroot] = yroot;
}

int main() {
    int n, e;
    cout << "Enter number of vertices and edges: ";
    cin >> n >> e;

    int u[20], v[20], w[20];
    cout << "Enter edges (u v weight):\n";
    for (int i = 0; i < e; i++)
        cin >> u[i] >> v[i] >> w[i];

    for (int i = 0; i < e - 1; i++) {
        for (int j = 0; j < e - i - 1; j++) {
            if (w[j] > w[j + 1]) {
                swap(w[j], w[j + 1]);
                swap(u[j], u[j + 1]);
                swap(v[j], v[j + 1]);
            }
        }
    }

    int parent[20];
    for (int i = 0; i < n; i++) parent[i] = i;

    int cost = 0;
    cout << "\nEdges in MST:\n";
    for (int i = 0; i < e; i++) {
        int x = findParent(parent, u[i]);
        int y = findParent(parent, v[i]);
        if (x != y) {
            cout << u[i] << " - " << v[i] << " : " << w[i] << endl;
            cost += w[i];
            unionSet(parent, x, y);
        }
    }

    cout << "Total cost of MST: " << cost << endl;
    return 0;
}

```
---
### Q5. Write a program to implement prim's minimum spanning tree algorithm.
```cpp
#include <iostream>
using namespace std;

#define INF 9999

int main() {
    int n;
    cout << "Enter number of vertices: ";
    cin >> n;

    int cost[20][20];
    cout << "Enter adjacency matrix (0 for no edge):\n";
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++) {
            cin >> cost[i][j];
            if (cost[i][j] == 0)
                cost[i][j] = INF;
        }

    int visited[20] = {0};
    visited[0] = 1;
    int edgeCount = 0, total = 0;

    cout << "\nEdges in MST:\n";
    while (edgeCount < n - 1) {
        int minCost = INF, a = -1, b = -1;
        for (int i = 0; i < n; i++) {
            if (visited[i]) {
                for (int j = 0; j < n; j++) {
                    if (!visited[j] && cost[i][j] < minCost) {
                        minCost = cost[i][j];
                        a = i;
                        b = j;
                    }
                }
            }
        }

        if (a != -1 && b != -1) {
            cout << a << " - " << b << " : " << minCost << endl;
            total += minCost;
            visited[b] = 1;
            edgeCount++;
        }
    }

    cout << "Total cost of MST: " << total << endl;
    return 0;
}

```
---
### Q6. Write a program to implement Dijkstra's shortest path algorithm.
```cpp
#include <iostream>
using namespace std;

#define INF 9999

int main() {
    int n;
    cout << "Enter number of vertices: ";
    cin >> n;

    int graph[20][20];
    cout << "Enter adjacency matrix (0 for no edge):\n";
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++) {
            cin >> graph[i][j];
            if (graph[i][j] == 0)
                graph[i][j] = INF;
        }

    int start;
    cout << "Enter source vertex: ";
    cin >> start;

    int dist[20], visited[20] = {0};
    for (int i = 0; i < n; i++)
        dist[i] = graph[start][i];

    visited[start] = 1;
    dist[start] = 0;

    for (int c = 1; c < n - 1; c++) {
        int min = INF, next = -1;
        for (int i = 0; i < n; i++) {
            if (!visited[i] && dist[i] < min) {
                min = dist[i];
                next = i;
            }
        }

        visited[next] = 1;
        for (int i = 0; i < n; i++) {
            if (!visited[i] && dist[next] + graph[next][i] < dist[i])
                dist[i] = dist[next] + graph[next][i];
        }
    }

    cout << "\nShortest Distances from vertex " << start << ":\n";
    for (int i = 0; i < n; i++)
        cout << "To " << i << " : " << dist[i] << endl;

    return 0;
}

```
---
