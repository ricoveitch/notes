# Algorithms

## Sliding Window

Use a left and right pointer. Objective is to shrink the window.

- https://leetcode.com/problems/container-with-most-water/description/
- https://leetcode.com/problems/minimum-size-subarray-sum/description/

### In a sorted array

```javascript
left = 0;
right = nums.length - 1;

while (left < right) {
  if (nums[left] + nums[right] > target) {
    // need to decrease total
    right -= 1;
  } else {
    // need to increase total
    left += 1;
  }
}
```

https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/

## Binary search

to find mid:

```javascript
// no overflow
mid = left + Math.floor((right - left) / 2);

// don't care
mid = Math.floor((right + left) / 2);
```

https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/description/
https://leetcode.com/problems/h-index-ii/description/

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

## Palindromes

Better to expand the window rather than shrinking it.

Will need to handle even and odd palindromes like so (will find all palindromes in O(n^2)).

```golang
for i := 0; i < len(s); i++ {
    expandRange(i, i)
    expandRange(i, i+1)
}
```

## Time intervals

If you have an interval and a newInterval, and need to determine overlap info.

newInterval comes after interval if `newInterval.start > interval.end`
newInterval comes before interval if `newInterval.end < interval.start`
else `overlaps` (`newInterval.end > interval.start || newInterval.start < interval.end`).

## The Two Pass

Make sure the condition holds for everything less then i (by going left to right)

Then make sure the condition holds for everything greater than i (by going right to left)

https://leetcode.com/problems/product-of-array-except-self/description/
https://leetcode.com/problems/candy/description/
