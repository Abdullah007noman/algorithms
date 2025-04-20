# Algorithms

This repository contains implementation of different algorithms:

1. Topological sort

2. Depth-First Search

3. Kruskal algorithm


# Topological Sort Algorithm Implementation (Page 613 ,fig-2,Cormen 3rd edition)

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

# DFS Implementation (Page 613 ,fig-1,Cormen 3rd edition)

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








