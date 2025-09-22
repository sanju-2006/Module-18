# Ex. No: 18B - Kruskal's Minimum Spanning Tree (MST) Algorithm

## AIM:
To write a Python program for **Kruskal's algorithm** to find the Minimum Spanning Tree (MST) of a given connected, undirected, and weighted graph.

## ALGORITHM:

**Step 1**: Sort all the edges of the graph in non-decreasing order of their weights.

**Step 2**: Initialize the `parent[]` and `rank[]` arrays for each vertex to keep track of the disjoint sets.

**Step 3**: Iterate through the sorted edges and pick the smallest edge. Check whether including this edge will form a cycle using the union-find method:
- If the vertices of the edge belong to different sets, include it in the MST.
- Perform a union of these two sets.

**Step 4**: Repeat Step 3 until the MST contains exactly `V-1` edges.

**Step 5**: Print the edges included in the MST and the total minimum cost.

## PYTHON PROGRAM

```
from collections import defaultdict

class Graph:

	def __init__(self, vertices):
		self.V = vertices  # No. of vertices
		self.graph = []    # List to store graph edges

	def addEdge(self, u, v, w):
		self.graph.append([u, v, w])

	def find(self, parent, i):
		if parent[i] == i:
			return i
		parent[i] = self.find(parent, parent[i])
		return parent[i]

	def union(self, parent, rank, x, y):
		xroot = self.find(parent, x)
		yroot = self.find(parent, y)

		if rank[xroot] < rank[yroot]:
			parent[xroot] = yroot
		elif rank[xroot] > rank[yroot]:
			parent[yroot] = xroot
		else:
			parent[yroot] = xroot
			rank[xroot] += 1

	def KruskalMST(self):

		result = []  # This will store the resultant MST

		self.graph = sorted(self.graph, key=lambda item: item[2])

		parent = []
		rank = []

		for node in range(self.V):
			parent.append(node)
			rank.append(0)

		e = 0  # Count of edges in MST
		i = 0  # Index for sorted edges

		while e < self.V - 1:

			u, v, w = self.graph[i]
			i += 1
			x = self.find(parent, u)
			y = self.find(parent, v)

			if x != y:
				e += 1
				result.append([u, v, w])
				self.union(parent, rank, x, y)

		print("Edges in the constructed MST")
		minCost = 0
		for u, v, weight in result:
			print(f"{u} -- {v} == {weight}")
			minCost += weight
		print(f"Minimum Spanning Tree {minCost}")

g = Graph(4)
g.addEdge(0, 1, 10)
g.addEdge(0, 2, 6)
g.addEdge(0, 3, 5)
g.addEdge(1, 3, 15)
g.addEdge(2, 3, 4)

# Function call
g.KruskalMST()```

`````

## OUTPUT

Edges in the constructed MST
2 -- 3 == 4
0 -- 3 == 5
0 -- 1 == 10
Minimum Spanning Tree 19


## RESULT

<img width="702" height="261" alt="image" src="https://github.com/user-attachments/assets/b0bb2f58-bf11-46ea-ab36-7bd062b9087e" />

