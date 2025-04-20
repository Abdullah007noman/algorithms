# Algorithms

This repository contains implementation of different algorithms:

1. Topological sort

2. Depth-First Search

3. Kruskal algorithm


# Topological Sort Algorithm Implementation

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

## Example Output

```
Topological Sort Result: ['watch', 'socks', 'shirt', 'undershorts', 'tie', 'belt', 'pants', 'jacket', 'shoes']

Dressing sequence:
Put on watch
Put on socks
Put on shirt
Put on undershorts
Put on tie
Put on belt
Put on pants
Put on jacket
Put on shoes
```

## License

MIT License

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
