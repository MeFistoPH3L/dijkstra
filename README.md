# Dijkstra
Finding the shortest paths from a given vertex to all other vertices by Dijkstra's algorithm

# The problem statement
Given a directed or undirected weighted graph with n vertices and m edges. The weights of all edges are non-negative. Given a certain starting vertex s. You are required to find the lengths of shortest paths from vertex s to all other vertices and also to provide a way to output the shortest paths themselves.

# Algorithm
Construct an array d[] to store the current length d[v] of the shortest path from s to v for each vertex v. Initially d[s]=0, and for all other vertices this length equals infinity (for computer implementation usually just big enough number, obviously larger than possible path length): d[v] = infty, v != s

Besides, for each vertex v we will store whether it is marked yet or not, i.e. we will introduce a Boolean array u[]. Initially all the vertices are unlabeled, i.e. u[v] = false

Dijkstra's algorithm itself consists of n iterations. At the next iteration the vertex v with the lowest value d[v] among those not marked yet d[v] = min d[p] will be chosen At the first iteration the starting vertex s

The vertex v thus chosen is marked as marked. Then, at the current iteration, relaxations are performed from vertex v: all edges (v,to) coming from vertex v are looked through, and for each such vertex to, the algorithm tries to improve the value of d[to]. Let the length of the current edge be \rm len, then in code form the relaxation looks like:

d[to] = min(d[to], d[v] + len)

At this point the current iteration ends, the algorithm moves on to the next iteration (again the vertex with the smallest value of d is chosen, the relaxations are performed from it, etc.). Finally, after n iterations all vertices of the graph become marked, and the algorithm finishes its work. It is said that the found values d[v] are the shortest paths from s to v.

Note that if not all vertices of the graph are reachable from vertex s, then values of d[v] for them will remain infinite. It is clear that the last few iterations of the algorithm will just select these vertices, but these iterations will not produce any useful work (because infinite distance cannot relax other, even infinite distances too). Therefore, the algorithm can immediately stop as soon as a vertex with infinite distance is taken as the selected vertex.

Reconstruct paths. Of course, we usually need to know not only the lengths of the shortest paths, but also to get the paths themselves. Let us show how to store information sufficient to later reconstruct the shortest path from s to any vertex. To do this, the so-called ancestor array is sufficient: the array p[], which for each vertex v \ne s stores the number of vertex p[v], which is the penultimate vertex in the shortest path to vertex v. Here we use the fact that if we take the shortest path to some vertex v and then remove the last vertex from this path, we get a path ending at some vertex p[v], and this path is the shortest path for vertex p[v]. So, if we have this array of ancestors, we can reconstruct the shortest path by simply taking an ancestor from the current vertex each time until we arrive at the starting vertex s - so we get the shortest path, but written in reverse order. At each successful relaxation, i.e. when there is a distance improvement from the chosen vertex v to some vertex to, we write that the ancestor of the vertex to is the vertex v: p[to] = v
