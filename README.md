# 8-puzzle-DFS-IDS-A-
8 puzzle with 4 solutions, depth first search, iterative deep search, a star with simple and Manhattan heuristics

Shravan Konduru README file

How to run the code:

python 8puzzle.py <Algorithm name> <File name>

Make sure that the algorithm name is valid and the file name is valid

algorithm name:

dfs		-for depth first search
ids		-for iterative deep search
astar1	-for a* algorithm with heuristic 1, simple
astar2	-for a* algorithm with heuristic 2, manhattan

file name:
Path of file, make sure folders are separated with forward slashes /
Make sure file has space separated integers with 0 representing empty tile. For example:

6 7 1 8 2 0 5 4 3

Sample dfs input and output, with input file containing same input as above:

python 8puzzle.py dfs C:/Users/shrak/PycharmProjects/8puzzle/inputfile
Input: 

6 7 1
8 2 0
5 4 3

Output:

6 7 1
8 2 0
5 4 3

6 7 1
8 0 2
5 4 3

6 0 1
8 7 2
5 4 3

0 6 1
8 7 2
5 4 3

8 6 1
0 7 2
5 4 3

8 6 1
7 0 2
5 4 3

8 0 1
7 6 2
5 4 3

0 8 1
7 6 2
5 4 3

7 8 1
0 6 2
5 4 3

7 8 1
6 0 2
5 4 3

Number of moves = 9
Number of states visited = 474


Sample astar2 input and output, with the input file containing same input as above:

python 8puzzle.py astar2 C:/Users/shrak/PycharmProjects/8puzzle/inputfile
Input: 

6 7 1
8 2 0
5 4 3

Output:

6 7 1
8 2 0
5 4 3

6 7 1
8 0 2
5 4 3

6 7 1
0 8 2
5 4 3

0 7 1
6 8 2
5 4 3

7 0 1
6 8 2
5 4 3

7 8 1
6 0 2
5 4 3

Number of moves = 5
Number of states visited = 5
