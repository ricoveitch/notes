# Data structures and algorithms

## Kadane's Algorithm

Finds maximum sub array. Its dp but also sliding window.

keep expanding the right pointer. If the current total < 0 then keep moving the left pointer to the right.

https://leetcode.com/problems/maximum-subarray/description/

## Deque

https://leetcode.com/problems/sliding-window-maximum/description/

## Binary search

https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/description/

## Dynamic Programming

### Use Cases

Usually one of:

- finding an optimal solution
- counting the total number of solutions for a problem

### Process

Usually solve by representing search space as tree, and (recursively) brute forcing it by using some tree search like `DFS`.

This will take the original problem and break it down into sub problems. Then recognize that you are repeating searches for the same trees.

### Top down

You take the same process as above but just cache the results.

https://www.youtube.com/watch?v=Hdr64lKQ3e4&t=669s

https://leetcode.com/problems/combination-sum-iv/ (easier to do than bottom up)

### Bottom up

When you break the original problem down in to sub problems, bottom up will start at the leaf nodes and go up (reverse order).

e.g. Instead of solving fibonacci(7) you start with fibonacci(1) then fibonacci(2) and so on. It needs to done in topological order.

This is `Iterative`.

`Climbing stairs`:
https://leetcode.com/problems/climbing-stairs/description/
https://www.youtube.com/watch?v=Y0lT9Fck7qI

`Coin change`:
https://leetcode.com/problems/coin-change/description/
https://www.youtube.com/watch?v=H9bfqozjoqs (good explanation)

## Heaps

## Graphs

### DFS

stack.pop()

### BFS

stack.remove(0)

## Two sum
