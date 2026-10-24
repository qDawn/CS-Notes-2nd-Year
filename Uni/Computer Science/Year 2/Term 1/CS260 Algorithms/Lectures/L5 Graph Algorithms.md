## This topic is already well known to the author and in such respects he cannot be bothered to write up much detailed notes instead he wrote a quick recap summary.


# Testing Bipartiteness

An undirected graph is bipartite if the graph is 2 colourable. Nodes can be coloured red or blue such that no two same colours match.

If a graph is bipartite it cannot contain an odd length cycle
# Prim's MST Algorithm

- Choose a random starting node and add it to a Set.
- Look at all edges connected to the node in the Set
- Choose the edge with the smallest weight which doesn't create a cycle
- Add that new node to the set
# Kruskal's MST Algorithm

- Sort edges in ascending order
- Choose edges in that order 
- Use Disjoint Set Union / Union find data structure to detect if forms a cycle
- If no cycle formed add to list 
- If cycle then discard
# Dijkstra's Shortest Path Algorithm

![[Pasted image 20261024195326.png]]

From D1 FM