
## Assignment Objectives:

In this assignment, you will:

* Implement some graph algorithms

NOTE: **as this assignment is about implementing data structures, you are not allowed to make use of any python libraries or use built-in python data structures and functions unless specified.  If you are not sure, please ask your professor.  Any use a built-in libraries or functions without approval will result in having to redo the assignment with a grade penalty of -50%**

## Part A: MinHeap (10 marks)

Create a class that will implement a MinHeap.  A MinHeap has the following member functions:

```python
def __init__(self, arr = [])
```
When a MinHeap is instantiated, it is passed a python list that may be empty.  You may assume that any values in the list are comparable using comparison operators such as <, <=, >=, >, == and !=.   This initializer will initialize a heap using this array.


***

```python
def insert(self, element)
```
This function adds element to the MinHeap

***

```python
def get_min(self)
```
This function returns smallest value in the MinHeap without altering the data structure

***
```python
def extract_min(self)
```

This function removes the smallest value from the MinHeap and returns that value

***

```python
def is_empty(self):
```
This function returns True if the MinHeap does not have any values in the heap, False otherwise

```python
def __len__(self):
```
This function returns number of values stored in the heap


## Part B: Minimum Spanning Tree (10 marks)

Write a function that will find the minimum spanning tree of a graph using either Kruskal's or Prim's algorithm.  You can find the description of Kruskal's and Prim's algorithm here.  Which one you choose is up to you.  if you use Kruskal's algorithm you will need to make use of the disjoint set from A1, if you use a Prims, you will need the MinHeap from part B:

https://seneca-ictoer.github.io/data-structures-and-algorithms/G-Graphs/mst

Write the following function:

```python
def minimum_spanning_tree(graph)
```

This function returns a list of edges that represents a minimum spanning tree.  Each element in the list of edges is made up of a tuple of two vertices

For example, suppose you were given this graph:

![Graph](https://user-images.githubusercontent.com/1699186/229127403-21643bca-ff75-42a8-b3ae-3df9f4d1b29f.png)


You function would return a list with the following edges:

[(2, 3), (5, 6), (0, 1), (3, 4), (0, 2), (4, 5)] which represents the MST in this picture

![MST of Graph](https://user-images.githubusercontent.com/1699186/229127426-eadace3e-11c3-4575-9f35-2c7acda82846.png)



## Part C: Maze Generation (10 marks)


In this last part of A3, you will use what you have created in this assignment and previous assignments to:

* generate a new maze of a given size
* run your mazerunner function from A1 on your new maze



### Update import statement in a1_partd.py

Please alter the import statement for importing the maze to:
```python
from a3_maze import Maze
```
it use to import from the file named maze.py but we need to update this to support alteration to data format.  This object is essentially the same as the old maze and only differs on how the maze is loaded

### Write the generat_maze function

Write the following function:

```python
def generate_maze(number_of_rows, number_of_columns)
```

This function is given the size of the maze in terms of number of rows and columns.  It will return a python list of tuples representing the walls for this maze.

Recall that a maze was defined by a set of walls that separated each cell.  If you were given a 3 X 4 maze, you would have 12 cells that were numbered as follows:

```
  0 |  1 |  2 |  3 
--------------------  
  4 |  5 |  6 |  7
--------------------
  8 |  9 | 10 | 11
```

To create a maze, start by creating a list of all walls.  Each wall can be represented as a tuple.  For example in the above maze we would represent all walls as follows:

[(0,1),(1,2),(2,3), (4,5),(5,6),(6,7), (8,9),(9,10),(10,11),(0,4),(4,8), (1,5),(5,9),(2,6),(6,10),(3,7),(7,11)]


Once you have the list of walls, use it to create a graph.  Each cell in the maze is represented as a vertex.  Thus the number of vertices in the graph is equal to the total number of cells.  For each of the walls in your list of walls:

* each wall is made up a tuple of 2 numbers (cell_1,cell_2).  These numbers represent the cells on either side of the wall.
* generate a small random number between 1 and 50
* create an edge from cell_1 to cell_2 with the random weight
* create another edge from cell_2 to cell_1 one with the same random weight

The reason you need two edges is because your graph is undirected



Thus, for a 3X4 maze above, we would end up with a graph that looks something like the following (note weights are random, yours will not have same weight, but the existance of the edges will be the same):


![Blank diagram(1)](https://user-images.githubusercontent.com/1699186/229268945-45ccbc4c-63a6-4e9c-ad46-09904a94e5fc.png)

The reason we wish to add this random edge weight is to allow an easy way to randomize the maze generation.


Once you have create the graph, a minimum spanning tree of this graph would represent a "hallway" that allows every cell to be reacheable by every other cell.

Use your function for finding a minimum spanning tree from part C to create a list of walls to remove.

Remove each of the walls in the MST from your original wall list.

This will create the list of walls that form your maze.


If your test passes for part C, four files will get generated.  You will use these to generate a visual output for your maze as part of your submission.

The following files are the mazes:

* a3_maze1.txt
* a3_maze2.txt

The following files are runs for the corresponding mazes:

* a3_run1.txt
* a3_run2.txt


Go to this url:

https://seneca-dsa456.github.io/dsa456-s23/a3.html


* Load each maze
* Load each mazerunner

Take a screenshot of each the two maze with maze runs add it to a3.md

* NOTE: due to the random nature of how you generate the maze, each test run will produce different mazes even without changing the code.  This is to be expected. 
