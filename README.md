# LEETCODE-Array-1514

Let's go through a dry run of the `maxProbability` method step-by-step with an example to see how the algorithm works. 

### Method Explanation
The function `maxProbability` aims to find the maximum probability of reaching a destination node `end` from a starting node `start` in a graph where each edge has a success probability.

1. **Graph Representation**: 
   - The graph is represented as an adjacency list (`graph`) where each node points to a list of pairs `(neighbor, probability)`.

2. **Priority Queue**:
   - A max-heap (`maxHeap`) is used to always explore the path with the highest probability first. 
   - Each entry in the heap is a pair of `(probability, node)`.

3. **Dijkstra-like Algorithm**:
   - The algorithm uses a greedy approach similar to Dijkstra's but focused on maximizing the product of probabilities instead of minimizing distances.

4. **Seen Array**:
   - An array `seen` keeps track of visited nodes to avoid re-processing.

### Example Input
Consider the following input to dry run the algorithm:

- `n = 3` (number of nodes)
- `edges = [[0, 1], [1, 2], [0, 2]]` (edges between nodes)
- `succProb = [0.5, 0.5, 0.2]` (success probabilities for each edge)
- `start = 0` (starting node)
- `end = 2` (destination node)

### Step-by-Step Dry Run

1. **Initialize Structures**:
   - `graph`: [[], [], []]
   - `maxHeap`: [(1.0, 0)] (start with probability 1 at the start node)
   - `seen`: [false, false, false]

2. **Build the Graph**:
   ``` 
   graph[0] = [(1, 0.5), (2, 0.2)]
   graph[1] = [(0, 0.5), (2, 0.5)]
   graph[2] = [(1, 0.5), (0, 0.2)]
   ```
   
3. **Main Loop - Process Nodes**:

   - **Iteration 1**:
     - Pop `(1.0, 0)` from `maxHeap`
     - `u = 0`, `prob = 1.0`
     - `seen[0]` becomes `true`
     - Process neighbors of `0`:
       - For `(1, 0.5)`: Add `(1.0 * 0.5, 1)` to `maxHeap` -> `maxHeap = [(0.5, 1)]`
       - For `(2, 0.2)`: Add `(1.0 * 0.2, 2)` to `maxHeap` -> `maxHeap = [(0.5, 1), (0.2, 2)]`

   - **Iteration 2**:
     - Pop `(0.5, 1)` from `maxHeap`
     - `u = 1`, `prob = 0.5`
     - `seen[1]` becomes `true`
     - Process neighbors of `1`:
       - For `(0, 0.5)`: Node `0` already seen, continue.
       - For `(2, 0.5)`: Add `(0.5 * 0.5, 2)` to `maxHeap` -> `maxHeap = [(0.25, 2), (0.2, 2)]`

   - **Iteration 3**:
     - Pop `(0.25, 2)` from `maxHeap`
     - `u = 2`, `prob = 0.25`
     - `u == end` (2 is the destination node)
     - Return `0.25` (maximum probability to reach node `2` from `0`)

### Result
The output of the function for this input is `0.25`.

### Summary
The algorithm correctly finds the path from the starting node to the destination node with the maximum probability using a priority queue (max-heap) and a Dijkstra-like approach.
