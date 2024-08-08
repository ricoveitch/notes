# Data structures and algorithms

## Kadane's Algorithm

Finds maximum sub array. Its dp but also sliding window.

keep expanding the right pointer. If the current total < 0 then keep moving the left pointer to the right.

https://leetcode.com/problems/maximum-subarray/description/

## Deque

https://leetcode.com/problems/sliding-window-maximum/description/

## Heaps

A 'compact' binary tree where each child is less than its parent (in a min heap).

O(logn) for push, pop and remove
O(n) to init an array
O(1) to get min (in min heap)

https://yuminlee2.medium.com/golang-heap-data-structure-45760f9562dc#e3f4

https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/description/

### Priority Queue

## Graphs

https://leetcode.com/problems/number-of-islands/

Need to build a `adjacency list` or `adjacency matrix`.

### Adjacency List

If you have (1) -> (2)

Then list would look like:

```js
{
    1: [2]
}
```

### DFS

`Time`: O(|V| + |E|)

Where where |V| is the number of vertices and |E| .the number of edges

Using a stack, push to front when can keep going, and stack.pop() when can't

```
def dfs_recursive(row, col):
    if !inbounds(row, col):
        return

    if visited[row][col]:
        return

    visited[row][col] = true

    for edge in curr:
        dfs_recursive(edge[0], edge[1])
```

```
def dfs(row, col):
    stack = [start]
    while stack.len:
        curr = stack.pop()
        if visited:
            continue

        visited = true

        for edge in curr:
            stack.push(edge)

```

E.g. https://leetcode.com/problems/word-search/description/ (modified so visited only hold the current path)

### BFS

`Time`: O(|V| + |E|)

```
queue = [edge]
while queue:
    curr = queue.popLeft()
    for edge in curr:
        if !visited(edge):
            queue.push(edge)
```

### Topological sort

`Time`: O(N)
`Space`: O(N)

```
adj_list := makeAdjList(nodes)
visited := [nodes.length]
in_curr_path := [nodes.length]
stack = []

for n in nodes {
    visit(n)
}
print(stack)

func visit(n) {
    if n in in_curr_path:
        stop // there is a cycle
    if n in visited:
        return

    in_curr_path[n] = true
    visited[n] = true

    for node m in adj_list[n]:
        visit(m)

    in_curr_path[n] = false
    stack.push(n)
}
```

E.g. https://leetcode.com/problems/course-schedule/description/

## Trees

### Inorder

```
if not root:
    return

inorder(root.left)
print(root)
inorder(root.right)
```

https://leetcode.com/problems/binary-tree-inorder-traversal/

### Preorder

```
if not root:
    return

print(root)
preorder(root.left)
preorder(root.right)
```

https://leetcode.com/problems/binary-tree-preorder-traversal/

### Postorder

```
if not root:
    return

preorder(root.left)
preorder(root.right)
print(root)
```

https://leetcode.com/problems/binary-tree-postorder-traversal/

### Iterative

Maintain a stack, and a curr pointer. When you go left or right push curr on the stack, and then set curr to left or right.

## Trie

For storing words.

O(n) for search, insert and delete
