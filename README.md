# Algorithms

This repository contains implementation of different algorithms:

1. Topological sort

2. Depth-First Search

3. Kruskal algorithm


# Topological Sort Algorithm Implementation (Page 613 ,fig-22.7 (a),Cormen 3rd edition)

This repository contains an implementation of Kahn's algorithm for topological sorting, demonstrated with a clothing dependency graph.
Topological sorting is a linear ordering of vertices in a directed acyclic graph (DAG) such that for every directed edge (u, v), vertex u comes before vertex v in the ordering. This algorithm is particularly useful for scheduling tasks with dependencies, course prerequisites, or determining the order to put on clothing items.

## Algorithm: Kahn's Topological Sort

Kahn's algorithm works by repeatedly removing nodes with no incoming edges and adding them to the result list. The implementation:

1. Calculates the in-degree (number of incoming edges) for each node
2. Adds all nodes with in-degree 0 to a queue
3. Processes nodes in the queue by:
   - Removing a node and adding it to the result
   - Decreasing the in-degree of all its neighbors
   - Adding any neighbors whose in-degree becomes 0 to the queue
4. Continues until the queue is empty
5. Checks if all nodes were processed (if not, the graph contains a cycle)

## Example Application: Clothing Graph

The repository includes an example of using topological sort to determine the correct order to put on clothing items. The clothing graph represents dependencies such as:
- Undershorts must be put on before pants
- Pants must be put on before shoes
- Socks must be put on before shoes
- Shirt must be put on before belt and tie
- Belt and tie must be put on before jacket

## Time Complexity

- Time Complexity: O(V + E) where V is the number of vertices and E is the number of edges
- Space Complexity: O(V)

## Usage

```python
# Define your graph as an adjacency list
graph = {
    "undershorts": ["pants"],
    "pants": ["shoes"],
    "socks": ["shoes"],
    "shirt": ["belt", "tie"],
    "belt": ["jacket"],
    "tie": ["jacket"],
    "watch": [],
    "shoes": [],
    "jacket": []
}

# Run the topological sort
sorted_order = kahns_topological_sort(graph)
print(sorted_order)
```

## Features

- ✅ Detects cycles in the graph
- ✅ Handles disconnected graphs
- ✅ Provides a valid topological ordering when possible
- ✅ Clear, commented implementation for educational purposes

# DFS Implementation (Page 613 ,fig-22.7 (b),Cormen 3rd edition)

This repository contains a Python implementation of the Depth-First Search (DFS) algorithm applied to a directed graph of clothing items. The graph represents dependencies or relationships between different clothing items, with each node having associated fraction values.

## Graph Structure
The graph is represented as follows:
- Each node is a clothing item (undershorts, pants, shirt, etc.)
- Directed edges show connections between items
- Each node has an associated fraction value (e.g., undershorts: 11/16)
  
## Implementation Details
The DFS algorithm is implemented using recursion with the following components:
1. Graph representation using an adjacency list
2. Visited node tracking to prevent cycles
3. Traversal order recording
4. Complete graph coverage handling

### Example Output
```
Starting DFS traversal of the clothing graph:
Visiting: undershorts (11/16)
Visiting: pants (12/15)
Visiting: belt (6/7)
Visiting: jacket (3/4)
Visiting: shoes (13/14)

Full DFS traversal order:
1. undershorts (11/16)
2. pants (12/15)
3. belt (6/7)
4. jacket (3/4)
5. shoes (13/14)

Checking for unvisited nodes:
Some nodes were not visited: watch, socks, tie, shirt
Running DFS from the remaining nodes:
Visiting: undershorts (11/16)
Visiting: pants (12/15)
Visiting: belt (6/7)
Visiting: jacket (3/4)
Visiting: shoes (13/14)
Visiting: socks (17/18)
Visiting: shirt (1/8)
Visiting: tie (2/5)
Visiting: watch (9/10)

Complete traversal order:
1. undershorts (11/16)
2. pants (12/15)
3. belt (6/7)
4. jacket (3/4)
5. shoes (13/14)
6. socks (17/18)
7. shirt (1/8)
8. tie (2/5)
9. watch (9/10)
```

## Graph Representation
The clothing graph is defined with the following adjacency list:
```python
graph = {
    'undershorts': ['pants', 'shoes'],
    'pants': ['belt', 'shoes'],
    'belt': ['jacket'],
    'shirt': ['belt', 'tie'],
    'tie': ['jacket'],
    'socks': ['shoes'],
    'shoes': [],
    'watch': [],
    'jacket': []
}
```

## Features

- ✅ Implementation of classic Depth-First Search algorithm
- ✅ Complete traversal of potentially disconnected graph components
- ✅ Tracks and reports visited nodes in order
- ✅ Handles the specific clothing item graph shown in the project
- ✅ Includes fraction values for each clothing item node


# Kruskal's Algorithm (Page 625 ,fig-23.1,Cormen 3rd edition)

This repository contains an implementation of Kruskal's algorithm for finding the Minimum Spanning Tree (MST) of an undirected, weighted graph. The implementation includes detailed debugging output, verification steps, and visualization capabilities.


A **Minimum Spanning Tree (MST)** is a subset of edges from a connected, undirected, weighted graph that connects all vertices with the minimum possible total edge weight, without forming any cycles. Kruskal's algorithm is one of the most efficient methods for finding MSTs.


Kruskal's algorithm works by:
1. Sorting all edges in non-decreasing order of their weight
2. Keeping a set of edges in the MST, initially empty
3. Iterating through the sorted edges and adding an edge to the MST if it doesn't form a cycle
4. Using a disjoint-set data structure (Union-Find) to efficiently detect cycles

The algorithm follows a greedy approach and guarantees an optimal solution.


## Usage

```python
from kruskal import kruskal, visualize_graph

# Define your graph
vertices = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i']
edges = [
    ('a', 'b', 4), ('a', 'h', 8),
    ('b', 'h', 11), ('b', 'c', 8),
    ('c', 'd', 7), ('c', 'i', 2),
    ('c', 'f', 4), ('d', 'e', 9),
    ('d', 'f', 14), ('e', 'f', 10),
    ('f', 'g', 2), ('g', 'h', 1),
    ('g', 'i', 6), ('h', 'i', 7)
]

# Run the algorithm with debugging information
mst, total_weight = kruskal(vertices, edges, debug=True)

# Visualize the result
visualize_graph(vertices, edges, mst)

# Find a path between vertices
path = find_path(mst, 'a', 'e')
if path:
    print(f"Path from 'a' to 'e': {' -> '.join(path)}")
```

## Example Output

When running the algorithm on the test graph:

```
Running Kruskal's algorithm with detailed debugging...

Sorted edges:
1. (g, h): 1
2. (c, i): 2
3. (f, g): 2
4. (a, b): 4
5. (c, f): 4
6. (g, i): 6
7. (c, d): 7
8. (h, i): 7
9. (a, h): 8
10. (b, c): 8
11. (d, e): 9
12. (e, f): 10
13. (b, h): 11
14. (d, f): 14

Execution of Kruskal's algorithm:
Added edge #1: (g, h) with weight 1
Current MST weight: 1
Added edge #2: (c, i) with weight 2
Current MST weight: 3
Added edge #3: (f, g) with weight 2
Current MST weight: 5
Added edge #4: (a, b) with weight 4
Current MST weight: 9
Added edge #5: (c, f) with weight 4
Current MST weight: 13
Skipped edge #6: (g, i) - would create a cycle
Added edge #7: (c, d) with weight 7
Current MST weight: 20
Skipped edge #8: (h, i) - would create a cycle
Added edge #9: (a, h) with weight 8
Current MST weight: 28
Skipped edge #10: (b, c) - would create a cycle
Added edge #11: (d, e) with weight 9
Current MST weight: 37
MST is complete with V-1 edges

MST verification passed: it is connected and acyclic

Edges in the Minimum Spanning Tree (sorted by weight and node names):
g - h: 1
c - i: 2
f - g: 2
a - b: 4
c - f: 4
c - d: 7
a - h: 8
d - e: 9

Total weight of MST: 37

Path from 'a' to 'e' in MST: a -> h -> g -> f -> c -> d -> e
Total weight of path: 31
```

## Visualization

The visualization shows both the original graph and the MST:

- Gray edges represent the original graph
- Red edges represent the edges in the MST
- Edge labels show the weights

## Complexity Analysis

- **Time Complexity**: O(E log E) where E is the number of edges in the graph
  - Sorting edges takes O(E log E)
  - Union-Find operations take nearly constant time with path compression and union by rank
- **Space Complexity**: O(V + E) where V is the number of vertices and E is the number of edges


## Features

This implementation includes:

- ✅ Uses path compression and union by rank optimizations for near-constant time operations
- ✅ Shows the execution of the algorithm step by step
- ✅ Confirms that the resulting MST is connected and acyclic
- ✅ Finds paths between vertices in the MST
- ✅ Creates a graphical representation of the original graph and the MST




