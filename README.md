# ===========================================================
#              DAA LAB – IMPORTANT PYTHON PROGRAMS
#                  Created by: Reva Rao 🧡
# ===========================================================

# 1. Linear Search
def linear_search(arr, x):
    for i in range(len(arr)):
        if arr[i] == x:
            return i
    return -1

print("\n--- Linear Search ---")
arr = [5, 2, 8, 9, 3]
x = 9
result = linear_search(arr, x)
print("Found at index:", result if result != -1 else "Not Found")


# 2. Binary Search
def binary_search(arr, x):
    low = 0
    high = len(arr) - 1
    while low <= high:
        mid = (low + high) // 2
        if arr[mid] == x:
            return mid
        elif x < arr[mid]:
            high = mid - 1
        else:
            low = mid + 1
    return -1

print("\n--- Binary Search ---")
arr = [2, 3, 5, 7, 11, 13]
res = binary_search(arr, 7)
print("Found at index:", res if res != -1 else "Not Found")


# 3. Merge Sort
def merge_sort(arr):
    if len(arr) <= 1:
        return arr
    mid = len(arr)//2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    return merge(left, right)

def merge(left, right):
    result = []
    i = j = 0
    while i < len(left) and j < len(right):
        if left[i] < right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
    result.extend(left[i:])
    result.extend(right[j:])
    return result

print("\n--- Merge Sort ---")
print(merge_sort([5, 3, 8, 4, 2]))


# 4. Quick Sort
def quick_sort(arr):
    if len(arr) <= 1:
        return arr
    p = arr[0]
    left = []
    right = []
    for x in arr[1:]:
        if x < p:
            left.append(x)
        else:
            right.append(x)
    return quick_sort(left) + [p] + quick_sort(right)

print("\n--- Quick Sort ---")
print(quick_sort([8, 3, 5, 1, 6]))


# 5. Strassen Matrix Multiplication (2x2)
print("\n--- Strassen Matrix Multiplication ---")
A = [[1, 2],
     [3, 4]]
B = [[5, 6],
     [7, 8]]

p1 = A[0][0]*(B[0][1]-B[1][1])
p2 = (A[0][0]+A[0][1])*B[1][1]
p3 = (A[1][0]+A[1][1])*B[0][0]
p4 = A[1][1]*(B[1][0]-B[0][0])
p5 = (A[0][0]+A[1][1])*(B[0][0]+B[1][1])
p6 = (A[0][1]-A[1][1])*(B[1][0]+B[1][1])
p7 = (A[0][0]-A[1][0])*(B[0][0]+B[0][1])

C = [[p5+p4-p2+p6, p1+p2],
     [p3+p4, p5+p1-p3-p7]]

print(C)


# 6. Greedy Knapsack
print("\n--- Greedy Knapsack ---")
items = [(60, 10), (100, 20), (120, 30)]
capacity = 50
items.sort(reverse=True)
profit = 0

for p, w in items:
    if capacity >= w:
        profit += p
        capacity -= w

print("Max Profit:", profit)


# 7. Greedy Graph Coloring
print("\n--- Graph Coloring ---")
graph = {
  0: [1, 2],
  1: [0, 2],
  2: [0, 1]
}
colors = {}
for node in graph:
    used = []
    for n in graph[node]:
        if n in colors:
            used.append(colors[n])
    for c in ["Red", "Blue", "Green"]:
        if c not in used:
            colors[node] = c
            break

print(colors)


# 8. 8 Queens (Backtracking)
print("\n--- 8 Queens Solution ---")
board = [[0]*8 for _ in range(8)]

def safe(r, c):
    for i in range(r):
        if board[i][c] == 1:
            return False
        if c-(r-i) >= 0 and board[i][c-(r-i)] == 1:
            return False
        if c+(r-i) < 8 and board[i][c+(r-i)] == 1:
            return False
    return True

def solve(r):
    if r == 8:
        for row in board:
            print(row)
        return True
    for c in range(8):
        if safe(r, c):
            board[r][c] = 1
            if solve(r+1):
                return True
            board[r][c] = 0

solve(0)


# 9. TSP (Small Example)
print("\n--- TSP (Small Example) ---")
INF = 999
cost = [
    [0,10,15,20],
    [10,0,35,25],
    [15,35,0,30],
    [20,25,30,0]
]
vis = [0]*4
best = INF

def tsp(curr, count, total):
    global best
    if count == 4:
        best = min(best, total + cost[curr][0])
        return
    for nxt in range(4):
        if not vis[nxt]:
            vis[nxt] = 1
            tsp(nxt, count+1, total + cost[curr][nxt])
            vis[nxt] = 0

vis[0] = 1
tsp(0, 1, 0)
print("Shortest Path:", best)


# 10. Valid Parentheses
print("\n--- Valid Parentheses ---")
s = "(())()"
stack = []
valid = True

for ch in s:
    if ch == "(":
        stack.append(ch)
    else:
        if not stack:
            valid = False
            break
        stack.pop()

print("Valid" if valid and not stack else "Invalid")
