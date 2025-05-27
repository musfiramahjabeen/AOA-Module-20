# AOA Module-20
## Day 1 - BACKTRACKING-RAT IN MAZE PROBLEM
### Rat In A Maze Problem
You are given a maze in the form of a matrix of size n * n. Each cell is either clear or blocked denoted by 1 and 0 respectively. A rat sits at the top-left cell and there exists a block of cheese at the bottom-right cell. Both these cells are guaranteed to be clear. You need to find if the rat can get the cheese if it can move only in one of the two directions - down and right. It can’t move to blocked cells.
![image](https://github.com/user-attachments/assets/7f8ea140-0357-462f-af75-3020b5525b0c)

Provide the solution for the above problem(Consider n=4)
The output (Solution matrix) must be 4*4 matrix with value "1" which indicates the path to destination and "0" for the cell indicating the absence of the path to destination.
```py
N = 4
def printSolution(sol):
    for i in sol:
        for j in i:
            print(str(j) + " ", end ="")
        print("")
def isSafe( maze, x, y ):
    if x >= 0 and x < N and y >= 0 and y < N and maze[x][y] == 1:
        return True
    return False
def solveMaze( maze ):
    # Creating a 4 * 4 2-D list
    sol = [ [ 0 for j in range(4) ] for i in range(4) ]
    if solveMazeUtil(maze, 0, 0, sol) == False:
        print("Solution doesn't exist");
        return False
    printSolution(sol)
    return True
def solveMazeUtil(maze, x, y, sol):
    if x==N-1 and y==N-1:
        sol[x][y]=1
        return True
    if isSafe(maze,x,y)==True:
        sol[x][y]=1
        if solveMazeUtil(maze,x+1,y,sol)==True:
            return True
        if solveMazeUtil(maze,x,y+1,sol)==True:
            return True
        sol[x][y]=0
        return False
    
if __name__ == "__main__":
    # Initialising the maze
    maze = [ [1, 0, 0, 0],
             [1, 1, 0, 1],
             [0, 1, 0, 0],
             [1, 1, 1, 1] ]
    solveMaze(maze)
```
## Day 2 - BACKTRACKING-NQUEEN PROBLEM
### NQUEEN PROBLEM

You are given an integer N. For a given N x N chessboard, find a way to place 'N' queens such that no queen can attack any other queen on the chessboard.
A queen can be attacked when it lies in the same row, column, or the same diagonal as any of the other queens. You have to print one such configuration.
![image](https://github.com/user-attachments/assets/8ecbab14-5f93-4de9-a320-5262ce347645)

Note :
Get the input from the user for N . The value of N must be from 1 to 4
If solution exists Print a binary matrix as output that has 1s for the cells where queens are placed
If there is no solution to the problem  print  "Solution does not exist"
```py
global N
N = int(input())
 
def printSolution(board):
    for i in range(N):
        for j in range(N):
            print(board[i][j], end = " ")
        print()
 
def isSafe(board, row, col):
 
    # Check this row on left side
    for i in range(col):
        if board[row][i] == 1:
            return False
 
    # Check upper diagonal on left side
    for i, j in zip(range(row, -1, -1),
                    range(col, -1, -1)):
        if board[i][j] == 1:
            return False
 
    # Check lower diagonal on left side
    for i, j in zip(range(row, N, 1),
                    range(col, -1, -1)):
        if board[i][j] == 1:
            return False
 
    return True
 
def solveNQUtil(board, col):
    if col>=N:
        return True
    for i in range(N):
        if isSafe(board,i,col):
            board[i][col]=1
            if solveNQUtil(board,col+1)==True:
                return True
            board[i][col]=0
    return False
                
      
def solveNQ():
    board = [ [0, 0, 0, 0],
              [0, 0, 0, 0],
              [0, 0, 0, 0],
              [0, 0, 0, 0]]
              
    if solveNQUtil(board, 0) == False:
        print ("Solution does not exist")
        return False
 
    printSolution(board)
    return True
 
# Driver Code
solveNQ()
```
## Day 3 - BACKTRACKING-SUBSET SUM PROBLEM
### SUBSET SUM PROBLEM
We are given a list of n numbers and a number x, the task is to write a python program to find out all possible subsets of the list such that their sum is x.
Examples:
![image](https://github.com/user-attachments/assets/1504ee54-6b1f-4f99-a7e4-9367ba5a50be)

THE INPUT
1.No of numbers
2.Get the numbers
3.Sum Value
```py
from itertools import combinations
def subsetSum(n, arr, x):
    for i in range(n):
        for sub in combinations(arr,i):
            if sum(sub)==x:
                print(list(sub))

n=int(input())
arr=[]
for i in range(0,n):
    a=int(input())
    arr.append(a)
x = int(input())

subsetSum(n, arr, x)
```
## Day 4 - BACKTRACKING - GRAPH COLORING PROBLEM
### GRAPH COLORING PROBLEM 
Given an undirected graph and a number m, determine if the graph can be coloured with at most m colours such that no two adjacent vertices of the graph are colored with the same color. Here coloring of a graph means the assignment of colors to all vertices.

Input-Output format: 

Input: 
A 2D array graph[V][V] where V is the number of vertices in graph and graph[V][V] is an adjacency matrix representation of the graph. A value graph[i][j] is 1 if there is a direct edge from i to j, otherwise graph[i][j] is 0.

An integer m is the maximum number of colors that can be used.

Output:

An array color[V] that should have numbers from 1 to m. color[i] should represent the color assigned to the ith vertex.

Example: 
![image](https://github.com/user-attachments/assets/e781bc50-a6e8-40e0-9113-1ce48d9f3354)
![image](https://github.com/user-attachments/assets/f76f4603-6cf7-4513-9e07-c54e55c3fb88)
```py
class Graph():
    def __init__(self,vertices):
        self.V = vertices
        self.graph = [[0 for col in range(vertices)]for row in range(vertices)]
    def isSafe(self,v,colour,c):
        for i in range(self.V):
            if self.graph[v][i]==1 and colour[i] == c:
                return False
        return True
    def graphColourUtil(self,m,colour,v):
        if v == self.V:
            return True
        for c in range(1,m+1):
            if self.isSafe(v,colour,c):
                colour[v] = c
                if self.graphColourUtil(m,colour,v+1):
                    return True
                colour[v] = 0
        return False
    def graphColouring(self,m):
        colour = [0]*self.V
        if not self.graphColourUtil(m,colour,0):
            print("Solution does not exist ")
            return False
        print("Solution exist and Following are the assigned colours:")
        for c in colour:
            print(c,end=" ")
        print()
        return True
```







