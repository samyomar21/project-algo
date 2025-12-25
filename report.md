==================================================

1. # Problem Description

We have (n) buildings and a list of possible
connections between the buildings.

Goal:
Construct a Minimum Spanning Tree (MST)

Conditions:
1 - Connect all buildings
2 - Minimize total cost
3 - Avoid cycles

# ==================================================

2. # Illustrative Input – Output Examples

---

## Algorithm 1: Naive MST (DFS Cycle Detection)

Example 1
Input : 50
Output : 0.001039

Example 2
Input : 100
Output : 0.003822

Example 3
Input : 300
Output : 0.021743

---

## Algorithm 2: Optimized MST (Union-Find / Kruskal)

Example 1
Input : 50
Output : 0.000000

Example 2
Input : 100
Output : 0.001445

Example 3
Input : 300
Output : 0.017499

# ==================================================

3. # Algorithms, Pseudocode, and Description

---

## Algorithm 1: Naive MST (DFS Cycle Detection)

Description:
This approach explicitly checks for cycles by
searching the current graph every time an edge
is considered. While simple and intuitive, it
becomes inefficient as the graph grows.

Pseudocode:

NAIVE_MST(n):

    buildings ← generate n random points

    edges ← empty list

    for i ← 0 to n − 1:
        for j ← i + 1 to n − 1:
            w ← distance between building i and building j
            add (i, j, w) to edges

    sort edges by weight in ascending order

    mst_edges ← empty list
    mst_cost ← 0

    create adjacency list adj for n nodes
    count ← 0

    for each (u, v, w) in edges:

        if count = n − 1:
            break

        visited ← empty set

        if HAS_PATH_DFS(adj, u, v, visited) = false:

            add (u, v, w) to mst_edges
            mst_cost ← mst_cost + w

            add v to adj[u]
            add u to adj[v]

            count ← count + 1

    return mst_edges, mst_cost

HAS_PATH_DFS(adj, current, target, visited):

    if current = target:
        return true

    add current to visited

    for each neighbor in adj[current]:
        if neighbor not in visited:
            if HAS_PATH_DFS(adj, neighbor, target, visited) = true:
                return true

    return false

---

## Algorithm 2: Optimized MST (Union-Find / Kruskal)

Description:
Union-Find efficiently tracks connected components
using path compression and union by rank, making
cycle detection nearly constant time.

Pseudocode:

MAKE_UNION_FIND(n):

    parent[i] ← i       for each i = 0 … n−1
    rank[i] ← 0         for each i = 0 … n−1

    return (parent, rank)

FIND(uf, x):

    if parent[x] ≠ x:
        parent[x] ← FIND(uf, parent[x])

    return parent[x]

UNION(uf, x, y):

    rootX ← FIND(uf, x)
    rootY ← FIND(uf, y)

    if rootX = rootY:
        return false   // cycle detected

    if rank[rootX] > rank[rootY]:
        parent[rootY] ← rootX
    else if rank[rootX] < rank[rootY]:
        parent[rootX] ← rootY
    else:
        parent[rootY] ← rootX
        rank[rootX] ← rank[rootX] + 1

    return true

OPTIMIZED_MST(n):

    buildings ← generate n random points

    edges ← empty list

    for i ← 0 to n − 1:
        for j ← i + 1 to n − 1:
            w ← distance between building i and building j
            add (i, j, w) to edges

    sort edges by weight in ascending order

    mst_edges ← empty list
    mst_cost ← 0

    uf ← MAKE_UNION_FIND(n)
    count ← 0

    for each (u, v, w) in edges:

        if count = n − 1:
            break

        if UNION(uf, u, v) = true:
            add (u, v, w) to mst_edges
            mst_cost ← mst_cost + w
            count ← count + 1

    return mst_edges, mst_cost

# ==================================================

4.  # Complexity Analysis

---

| ---Algorithm------ | ----Time-------- | ---Space------ |
| ------------------ | ---------------- | -------------- |
| ---Naive MST------ | ---- O(n³)------ | ---O(n²)------ |
| ------------------ | ---------------- | -------------- |
| --Optimized MST--- | ---O(n² log n)-- | ---O(n²)------ |

---

# ==================================================

5. # Empirical Results

## Nodes Naive Time Optimized Time

---

| -----Nodes---- | ------Naive------ | ----Optimized---- |
| -------------- | ----------------- | ----------------- |
| -----100------ | ------Slow------- | -------Fast------ |
| -------------- | ----------------- | ----------------- |
| -----1000----- | ----very Slow---- | -------Fast------ |
| -------------- | ----------------- | ----------------- |
| ----10,000---- | ---Impractical--- | ----Acceptable--- |

---

# ==================================================

6.  # Comparison Discussion

---

| -----Aspect---- | ------Naive------ | ----Optimized---- |
| --------------- | ----------------- | ----------------- |
| --Simplicity--- | ---Very Simple--- | ---More Complex-- |
| --------------- | ----------------- | ----------------- |
| --Performance-- | ------ Poor------ | -----Excellent--- |
| --------------- | ----------------- | ----------------- |
| --Scalability-- | ----No Scaling--- | ---Scales Well--- |

---

# ==================================================

7. # Final Verdict

Naive MST:

- Good for learning purposes
- Suitable only for very small graphs

Optimized MST:

- The correct choice for real-world problems
- Efficient for large-scale graphs
