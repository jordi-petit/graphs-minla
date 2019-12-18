# Collection of graphs

This repository provides a set of graphs originally used to benchmark the MinLA
problem. All graphs on this page are undirected, without self loops, and very
sparse. I am currently unable to trace back their original source.

Each graph has a name and several associated files. Not all graphs have the same
files. For example, the `airfoil1` graph is associated with the files
`airfoil1.gra`, `airfoil1.txt`, `airfoil1.xyz`, `airfoil1.eps`, and
`airfoil1.pdf`; but the `c1y` graph has only the `c1y.gra` and `c1y.txt` files
associated with it.

Here follows a description of the format of these files.


## Description files

The description files have the extension `.txt`. These are text files with a
brief description that describe the type of graph, its origin or
characteristics.


## Graph files

All graphs have a graph file that has the `.gra` extension. This is the only
really important file, as it contains the graph itself. The graph is
described through an adjacency list format.

These files have 5 lines, each with the following information:

1. Number of vertices
2. Number of edges
3. Degree of the vertices
4. Adjacency list
5. Indexes of the adjacency list

For example, the `small.gra` file contains:

```text
5
8
3 3 3 3 4
1 3 4 0 2 4 1 3 4 0 2 4 0 1 2 3 -1
0 3 6 9 12 16
```


The number of vertices (*n*) is given on the first line. It is an integer. In
the case of the `small` graph, there are *n* = 5 vertices. The vertices have
named 0, 1, ..., *n* - 1.

The number of edges (*m*) is given in the second line. It is an integer. In the
case of the `small` graph, there are (*m* = 8) edges.

The degree of each vertex is given in the third line, containing *n* integers.
In the case of `small` graph, vertex 0 has degree 3, vertex 1 has degree 3, vertex
2 has degree 3, vertex 3 has degree 3, and vertex 4 has degree 4.

The adjacency lists for each vertex come in the fourth line,  which contains 2 *
*m* + 1 values. This line breaks down into *n* + 1 chunks, one for each vertex,
and an extra element which is always -1. So, in
the case of the `small` graph we have 5 chunks:

```text
[1 3 4] [0 2 4] [1 3 4] [0 2 4] [0 1 2 3] -1
```

This means that vertex 0 (which had a degree 3) has neighbors  1, 3 and 4.
Vertex 1 has neighbors 0, 2 and 4... The -1 mark is usefull to stop the loops in
the implementation phase.

The indexes in the adjacency lists are also  usefull at the implementation
phase. They are not essential, as the degree of the nodes already generates this
information. In any case, this fifth contiguous line *n* + 1 integers, which
form the prefixed sum of the degrees of the vertices.

For instance, in the `small` graph, this would be the table that corresponds to
the adjacency lists:

```
0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16
1  3  4  0  2  4  1  3  4  0  2  4  0  1  2  3 -1
```

and this is the table of indexes to the adjacency lists:

```text
0  1  2  3  4  5
0  3  6  9 12 16
```

Using the indexes in the adjacency lists, one can
know that the adjacency list of vertex 1 is between positions 3 and 6-1 and
that, therefore, 1 is connected to vertices 0, 2 and 4.

From this explanation, it is clear that this is the `small` graph:

```
0-----1
|\   /|
| \ / |
|  4  |
| / \ |
|/   \|
3-----2
```


## Coordinate files

Coordinate files have the `.xyz` extension. There can be two-dimensional (x and
y) coordinates or three-dimensional (x, y and z) coordinates. The coordinates of
each vertex are in a line, containing two or three real values.


## Drawing files

Drawing files have the `.eps` and `.pdf` extensions corrresponding to
Encapsulated PostScript and PDF drawings of the graphs.
