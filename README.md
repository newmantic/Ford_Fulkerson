# Ford_Fulkerson


The Ford-Fulkerson method is an algorithm used to compute the maximum flow in a flow network. The method repeatedly finds augmenting paths from a source node s to a sink node t and increases the flow along these paths until no more augmenting paths can be found. The key idea is to keep adjusting the flow in the network until the maximum possible flow is achieved.


Flow Network:
A flow network is a directed graph G = (V, E) where:
V is the set of vertices (nodes).
E is the set of edges.
Each edge (u, v) has a capacity c(u, v), which is the maximum amount of flow that can pass through the edge.
The flow f(u, v) on each edge must satisfy:
0 <= f(u, v) <= c(u, v)

Flow Conservation:
For every vertex v in the graph except the source s and sink t, the sum of the flow into v equals the sum of the flow out of v:
sum(f(u, v) for u in pred(v)) = sum(f(v, w) for w in succ(v))
This ensures that flow is conserved at each vertex.


The residual graph G_f represents the available capacity for sending additional flow. It is constructed from the original flow network by adjusting capacities:
For each edge (u, v), the residual capacity is c_f(u, v) = c(u, v) - f(u, v).
Additionally, a reverse edge (v, u) is included in the residual graph with a capacity of f(u, v) to allow for flow reversal if necessary.

An augmenting path is a path from s to t in the residual graph G_f where every edge on the path has a positive residual capacity:
c_f(u, v) > 0  for every edge (u, v) in the path

The bottleneck capacity of an augmenting path is the minimum residual capacity along the path:
bottleneck(P) = min(c_f(u, v) for (u, v) in P)

Increase the flow along the augmenting path by the bottleneck capacity. Adjust the residual capacities in the residual graph accordingly.


Step 1:
Initialize the flow on all edges to 0:
f(u, v) = 0  for all (u, v) in E

Step 2:
Construct the residual graph G_f based on the current flow.

Step 3:
While there exists an augmenting path P from s to t in the residual graph G_f:
Find the bottleneck capacity of the path P:
bottleneck(P) = min(c_f(u, v) for (u, v) in P)

Increase the flow along the path P by the bottleneck capacity:
f(u, v) += bottleneck(P)  for all (u, v) in P
Update the residual graph G_f by adjusting the capacities.

Step 4:
The algorithm terminates when no more augmenting paths can be found. The value of the maximum flow is the sum of the flow on edges going out of the source s:
max_flow = sum(f(s, v) for v in succ(s))
