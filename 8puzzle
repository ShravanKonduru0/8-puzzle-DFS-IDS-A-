import copy
import sys
import os


def checkgoal(start, goal):  # checks if goal is reached
    for i in range(3):
        for j in range(3):
            if start[i][j] != goal[i][j]:
                return False
    return True


def move(current):  # returns array with possible moves of 0/empty tile
    x, y = 0, 0
    for i in range(3):
        for j in range(3):
            if current[i][j] == 0:
                x, y = i, j
    movelist = [[x, y, x + 1, y], [x, y, x - 1, y], [x, y, x, y + 1], [x, y, x, y - 1]]
    return movelist


def fscore1(current, goal, level):  # heuristic 1, calculates number of wrong tiles
    fscore, g, h = 0, 0, 0
    g = 10 - level
    for i in range(3):
        for j in range(3):
            if current[i][j] != goal[i][j]:
                h += 1
    fscore = g + h
    return fscore


def manhattanhelper(current, goal, element):
    a, b, x, y = 3, 3, 3, 3
    for i in range(3):
        for j in range(3):
            if current[i][j] == element:
                a, b = i, j
    for i in range(3):
        for j in range(3):
            if goal[i][j] == element:
                x, y = i, j
    return abs(a - x) + abs(b - y)


def fscoremanhattan(current, goal, level):  # heuristic 2, manhattan calculates distance from goal of wrong tiles
    fscore, g, h = 0, 0, 0
    g = 10 - level
    for i in range(8):
        h += manhattanhelper(current, goal, i + 1)
    fscore = g + h
    return fscore


def dfs(current, level):  # dfs method goes through all possible moves until one is found
    if level <= 0:
        return False
    visited.append(current)
    global states
    states += 1
    if checkgoal(current, goalarr):
        resultarr.append(current)
        return True
    movelist = move(current)
    for i in movelist:
        temp = copy.deepcopy(current)
        if 0 <= i[2] < 3 and 0 <= i[3] < 3:
            temp[i[2]][i[3]] = current[i[0]][i[1]]
            temp[i[0]][i[1]] = current[i[2]][i[3]]
        if temp in visited:
            continue
        if dfs(temp, level - 1):
            resultarr.append(current)
            return True
    visited.remove(current)
    return False


def ids(start):  # iterative deep search goes through dfs one depth at a time to ensure the simplest solution is found
    i = 1
    while i <= 11:
        visited.clear()
        if dfs(start, i):
            return True
        i += 1
    return False


def astar(current, level):  # astar helper which computes fscore of children and child with smallest f score recurse
    if level <= 0:
        return False
    visited.append(current)
    global states
    states += 1
    if checkgoal(current, goalarr):
        resultarr.append(current)
        return True
    movelist = move(current)
    f0, f1, f2, f3 = sys.maxsize, sys.maxsize, sys.maxsize, sys.maxsize
    temp0 = copy.deepcopy(current)
    if 0 <= movelist[0][2] < 3 and 0 <= movelist[0][3] < 3:
        temp0[movelist[0][2]][movelist[0][3]] = current[movelist[0][0]][movelist[0][1]]
        temp0[movelist[0][0]][movelist[0][1]] = current[movelist[0][2]][movelist[0][3]]
        f0 = fscore1(temp0, goalarr, level - 1)
    temp1 = copy.deepcopy(current)
    if 0 <= movelist[1][2] < 3 and 0 <= movelist[1][3] < 3:
        temp1[movelist[1][2]][movelist[1][3]] = current[movelist[1][0]][movelist[1][1]]
        temp1[movelist[1][0]][movelist[1][1]] = current[movelist[1][2]][movelist[1][3]]
        f1 = fscore1(temp1, goalarr, level - 1)
    temp2 = copy.deepcopy(current)
    if 0 <= movelist[2][2] < 3 and 0 <= movelist[2][3] < 3:
        temp2[movelist[2][2]][movelist[2][3]] = current[movelist[2][0]][movelist[2][1]]
        temp2[movelist[2][0]][movelist[2][1]] = current[movelist[2][2]][movelist[2][3]]
        f2 = fscore1(temp2, goalarr, level - 1)
    temp3 = copy.deepcopy(current)
    if 0 <= movelist[3][2] < 3 and 0 <= movelist[3][3] < 3:
        temp3[movelist[3][2]][movelist[3][3]] = current[movelist[3][0]][movelist[3][1]]
        temp3[movelist[3][0]][movelist[3][1]] = current[movelist[3][2]][movelist[3][3]]
        f3 = fscore1(temp3, goalarr, level - 1)
    temparr = [temp0, temp1, temp2, temp3]
    tempf = [f0, f1, f2, f3]
    childlist = [x for _, x in sorted(zip(tempf, temparr))]
    for i in childlist:
        if i in visited:
            continue
        if astar(i, level - 1):
            resultarr.append(current)
            return True
    visited.remove(current)
    return False


def astarmanhattan(current, level):  # astar with heuristic 2, very efficient
    if level <= 0:
        return False
    visited.append(current)
    global states
    states += 1
    if checkgoal(current, goalarr):
        resultarr.append(current)
        return True
    movelist = move(current)
    f0, f1, f2, f3 = sys.maxsize, sys.maxsize, sys.maxsize, sys.maxsize
    temp0 = copy.deepcopy(current)
    if 0 <= movelist[0][2] < 3 and 0 <= movelist[0][3] < 3:
        temp0[movelist[0][2]][movelist[0][3]] = current[movelist[0][0]][movelist[0][1]]
        temp0[movelist[0][0]][movelist[0][1]] = current[movelist[0][2]][movelist[0][3]]
        f0 = fscoremanhattan(temp0, goalarr, level - 1)
    temp1 = copy.deepcopy(current)
    if 0 <= movelist[1][2] < 3 and 0 <= movelist[1][3] < 3:
        temp1[movelist[1][2]][movelist[1][3]] = current[movelist[1][0]][movelist[1][1]]
        temp1[movelist[1][0]][movelist[1][1]] = current[movelist[1][2]][movelist[1][3]]
        f1 = fscoremanhattan(temp1, goalarr, level - 1)
    temp2 = copy.deepcopy(current)
    if 0 <= movelist[2][2] < 3 and 0 <= movelist[2][3] < 3:
        temp2[movelist[2][2]][movelist[2][3]] = current[movelist[2][0]][movelist[2][1]]
        temp2[movelist[2][0]][movelist[2][1]] = current[movelist[2][2]][movelist[2][3]]
        f2 = fscoremanhattan(temp2, goalarr, level - 1)
    temp3 = copy.deepcopy(current)
    if 0 <= movelist[3][2] < 3 and 0 <= movelist[3][3] < 3:
        temp3[movelist[3][2]][movelist[3][3]] = current[movelist[3][0]][movelist[3][1]]
        temp3[movelist[3][0]][movelist[3][1]] = current[movelist[3][2]][movelist[3][3]]
        f3 = fscoremanhattan(temp3, goalarr, level - 1)
    temparr = [temp0, temp1, temp2, temp3]
    tempf = [f0, f1, f2, f3]
    childlist = [x for _, x in sorted(zip(tempf, temparr))]
    for i in childlist:
        if i in visited:
            continue
        if astarmanhattan(i, level - 1):
            resultarr.append(current)
            return True
    visited.remove(current)
    return False


def printpuzzle(arr):  # helper function to print 3 by 3 puzzle
    print("\n" + str(arr[0][0]) + " " + str(arr[0][1]) + " " + str(arr[0][2]) + "\n" + str(arr[1][0]) + " " +
          str(arr[1][1]) + " " + str(arr[1][2]) + "\n" + str(arr[2][0]) + " " + str(arr[2][1]) + " " + str(
        arr[2][2]))


if os.path.isfile(sys.argv[2]):
    f = open(sys.argv[2], "r")  # input file, change this to replace file
else:
    print('The file does not exist.')
    sys.exit()

inputs = f.readline().split(" ")
startarr = [[int(inputs[0]), int(inputs[1]), int(inputs[2])], [int(inputs[3]), int(inputs[4]), int(inputs[5])],
            [int(inputs[6]), int(inputs[7]), int(inputs[8])]]
resultarr = []
goalarr = [[7, 8, 1], [6, 0, 2], [5, 4, 3]]
visited, states = [], 0

print("Input: ")
printpuzzle(startarr)
algo = sys.argv[1]
# Select number for the algorithm wanted
if algo == "dfs":  # dfs
    if dfs(startarr, 11):
        print("\nOutput: ")
        for i in reversed(resultarr):
            printpuzzle(i)
        print("\nNumber of moves = " + str(len(resultarr) - 1))
        print("Number of states visited = " + str(states - 1))
    else:
        print("Failure, could not find a valid solution within depth 10")
elif algo == "ids":  # ids
    if ids(startarr):
        print("\nOutput: ")
        for i in reversed(resultarr):
            printpuzzle(i)
        print("\nNumber of moves = " + str(len(resultarr) - 1))
        print("Number of states visited = " + str(states - 1))
    else:
        print("Failure, could not find a valid solution within depth 10")
elif algo == "astar1":  # a* heuristic 1
    if astar(startarr, 11):
        print("\nOutput: ")
        for i in reversed(resultarr):
            printpuzzle(i)
        print("\nNumber of moves = " + str(len(resultarr) - 1))
        print("Number of states visited = " + str(states - 1))
    else:
        print("Failure, could not find a valid solution within depth 10")
elif algo == "astar2":  # a* heuristic 2 manhattan
    if astarmanhattan(startarr, 11):
        print("\nOutput: ")
        for i in reversed(resultarr):
            printpuzzle(i)
        print("\nNumber of moves = " + str(len(resultarr) - 1))
        print("Number of states visited = " + str(states - 1))
    else:
        print("Failure, could not find a valid solution within depth 10")
else:
    print("Error - Not a valid algorithm")
