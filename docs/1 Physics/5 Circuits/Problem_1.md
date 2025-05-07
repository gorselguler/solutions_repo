# Problem 1

# Equivalent Resistance Using Graph Theory
 
Motivation:
Calculating the equivalent resistance in an electrical circuit is a fundamental task in electrical engineering and physics. While traditional methods involve step-by-step application of series and parallel resistor rules, graph theory offers a more systematic approach for handling complex resistor networks. By representing the circuit as a graph, where nodes are junctions and edges represent resistors, we can simplify the process of finding the equivalent resistance, especially in circuits with complex or nested configurations.

Algorithm Overview:
The algorithm calculates the equivalent resistance in a circuit by reducing the graph iteratively. The key steps involve:

Identifying Series Connections: Resistors connected end-to-end (in series) can be replaced by a single equivalent resistor, where the total resistance is the sum of individual resistances.

Identifying Parallel Connections: Resistors connected in parallel can be replaced by an equivalent resistor using the parallel resistance formula:

𝑅
eq
=
(
∑
1
𝑅
𝑖
)
−
1
R 
eq
​
 =(∑ 
R 
i
​
 
1
​
 ) 
−1
 
Iterative Reduction: The algorithm simplifies the graph by detecting and combining series and parallel resistors until only one edge (the equivalent resistance) remains.

Algorithm Steps:
Input: A graph representing the circuit, where each node is a junction and each edge is a resistor with a resistance value.

Series and Parallel Reduction:

For series resistors, combine their resistances by adding them.

```python
def series_circuit(*resistances):
    """
    Calculate the equivalent resistance for resistors in series.
    :param resistances: List of resistor values in series.
    :return: Equivalent resistance
    """
    return sum(resistances)

# Example for A-B-C in series
resistance_series = series_circuit(5, 10)  # A–B: 5Ω, B–C: 10Ω
print(f"Equivalent resistance for series circuit: {resistance_series} Ω")
```
Equivalent resistance for series circuit: 15 Ω


For parallel resistors, use the parallel formula to compute the equivalent resistance.

```python
def parallel_circuit(*resistances):
    """
    Calculate the equivalent resistance for resistors in parallel.
    :param resistances: List of resistor values in parallel.
    :return: Equivalent resistance
    """
    inverse_sum = sum(1 / r for r in resistances)
    return 1 / inverse_sum

# Example for triangle circuit: A–B = 6Ω, A–C = 6Ω, B–C = 3Ω
resistance_parallel = parallel_circuit(6, 6, 3)  # Resistors in parallel
print(f"Equivalent resistance for parallel circuit: {resistance_parallel:.2f} Ω")
```
Equivalent resistance for parallel circuit: 1.50 Ω

Graph Update:

After combining resistors, update the graph by replacing the combined resistors with their equivalent resistance, removing the individual resistors.

Repeat: Continue reducing the graph until there is only one remaining edge, which represents the equivalent resistance of the entire circuit.

Output: The equivalent resistance of the circuit.

Pseudocode for Equivalent Resistance Calculation:
plaintext
Kopyala
Düzenle
function calculate_equivalent_resistance(graph):
    while graph has more than one resistor:
        // Step 1: Identify and combine series resistors
        for each pair of nodes u and v connected by resistors:
            if u and v are in series:
                R_series = sum of resistances of connected resistors
                replace u-v connection with R_series in the graph

        // Step 2: Identify and combine parallel resistors
        for each pair of nodes u and v connected by resistors:
            if u and v are in parallel:
                R_parallel = 1 / (1/R1 + 1/R2 + ...)
                replace u-v connection with R_parallel in the graph
        
        // Repeat until only one resistor remains in the graph

    return the final equivalent resistance
Explanation:
Series Connection: Resistors in series share a single path, so their total resistance is the sum of the individual resistances:

𝑅
eq
=
𝑅
1
+
𝑅
2
+
⋯
R 
eq
​
 =R 
1
​
 +R 
2
​
 +⋯
Parallel Connection: Resistors in parallel share two nodes and can be reduced using the formula:

1
𝑅
eq
=
1
𝑅
1
+
1
𝑅
2
+
⋯
R 
eq
​
 
1
​
 = 
R 
1
​
 
1
​
 + 
R 
2
​
 
1
​
 +⋯
For two resistors in parallel:

𝑅
eq
=
𝑅
1
⋅
𝑅
2
𝑅
1
+
𝑅
2
R 
eq
​
 = 
R 
1
​
 +R 
2
​
 
R 
1
​
 ⋅R 
2
​
 
​
 
Iterative Reduction:

At each iteration, identify series or parallel connections and replace them with their equivalent resistances.

The graph is updated to reflect the new resistor configuration after each reduction.

This process continues until only one equivalent resistor remains.

Handling Nested Configurations:

Nested series and parallel configurations are handled by detecting combinations of series and parallel connections that can be simplified. After reducing one combination, the graph is re-evaluated to check if new series or parallel combinations appear due to the simplification.

Complex Circuits:

For circuits with multiple cycles and branches, the algorithm systematically reduces the graph while maintaining the relationships between resistors. Even in complex circuits, the algorithm ensures that each reduction step brings the graph closer to a single equivalent resistor.

Example Inputs:
Example 1: Simple Series Circuit
Given a simple series circuit:

css
Kopyala
Düzenle
A -- 2Ω -- B -- 3Ω -- C
The algorithm detects that resistors between A and B, and B and C, are in series.

The equivalent resistance between A and C is:

𝑅
eq
=
2
Ω
+
3
Ω
=
5
Ω
R 
eq
​
 =2Ω+3Ω=5Ω
Example 2: Simple Parallel Circuit
Given a simple parallel circuit:

less
Kopyala
Düzenle
A -- 2Ω --+-- C
          |
          3Ω
          |
          B
The algorithm detects that resistors between A and C, and C and B, are in parallel.

The equivalent resistance is:

𝑅
eq
=
2
Ω
×
3
Ω
2
Ω
+
3
Ω
=
1.2
Ω
R 
eq
​
 = 
2Ω+3Ω
2Ω×3Ω
​
 =1.2Ω
Example 3: Nested Series and Parallel
Given a nested circuit:

less
Kopyala
Düzenle
A -- 2Ω --+-- B -- 4Ω --+-- C
          |              |
          3Ω             6Ω
          |              |
          +--------------+
First, combine the resistors between B and C (which are in parallel):

𝑅
BC
=
4
Ω
×
6
Ω
4
Ω
+
6
Ω
=
2.4
Ω
R 
BC
​
 = 
4Ω+6Ω
4Ω×6Ω
​
 =2.4Ω
Now, combine the resistors between A and B (in series with 3Ω and 2.4Ω):

𝑅
AB
=
3
Ω
+
2.4
Ω
=
5.4
Ω
R 
AB
​
 =3Ω+2.4Ω=5.4Ω
Finally, combine the remaining series resistors A to C:

𝑅
eq
=
2
Ω
+
5.4
Ω
=
7.4
Ω
R 
eq
​
 =2Ω+5.4Ω=7.4Ω
Algorithm Efficiency:
Time Complexity:

The algorithm processes each edge of the graph multiple times. Each iteration reduces the number of resistors by merging series or parallel connections.

In the worst case, the complexity can be 
𝑂
(
𝐸
)
O(E), where 
𝐸
E is the number of edges (resistors) in the graph.

Space Complexity:

The space complexity is 
𝑂
(
𝑉
+
𝐸
)
O(V+E), where 
𝑉
V is the number of nodes (junctions) and 
𝐸
E is the number of edges (resistors). The graph's adjacency list is stored in memory.

Potential Improvements:

Optimized Parallelism: In circuits with many parallel paths, additional optimizations can be applied to detect and combine parallel resistors more efficiently.

Graph Traversal: Depth-First Search (DFS) or Breadth-First Search (BFS) could be used to identify cycles and more complex subgraphs that might offer faster reduction.

Caching Subgraphs: Caching intermediate results for subgraphs could improve efficiency for circuits with repeated substructures.

Conclusion:
Using graph theory to calculate equivalent resistance provides a structured, algorithmic way to analyze circuits. This approach can handle complex configurations, including nested series and parallel resistors, making it ideal for circuit analysis and simulation. The iterative graph simplification process ensures that the algorithm is scalable and efficient, even for large circuits.


