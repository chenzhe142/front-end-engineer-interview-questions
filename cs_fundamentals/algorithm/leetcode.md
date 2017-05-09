# leetcode

## [Kadane's algorithm](https://en.wikipedia.org/wiki/Maximum_subarray_problem)
1. maximum subarray
2. best time to buy & sell stocks (I, II, III, IV)
  - [I](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/): the logic is to calculate the difference ``(maxCur += prices[i] - prices[i-1])`` of the original array, and find a contiguous subarray giving maximum profit. If the difference falls below 0, reset it to zero.
  - [III](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/#/description): dynamic programming `dp[k][prices.length]`

## Maximun `blah blah blah` subarray
1. [contiguous array](https://leetcode.com/problems/contiguous-array)
for finding subarray containing equal amount of elements, use `minus plus`. Do `minus` for A element, and do `plus` for B element. They will create two points with same Y-axis value (which means they eliminates the differences between them)
2. [Maximum Size Subarray Sum Equals k](https://leetcode.com/problems/maximum-size-subarray-sum-equals-k)


## Depth first search

## Bucket sort: sort in linear time. usually the data range is known.
1. [H-index](https://leetcode.com/problems/h-index/#/description)

## Substring search & match
1. [Implement strStr()](https://leetcode.com/problems/implement-strstr/#/description): use KMP algorithm (read [this post](http://blog.csdn.net/v_july_v/article/details/7041827))

## Sliding windows:
1. find a valid window, update result (with hashmap's help)
2. make window invalid,
3. and repeat

## Breadth first search (one-end, two-end, or multiple-end search)
1. one-end: tree
2. two-end: know `start` and `end`, such as `Word Laddar`

## Graph
1. check cycle: union find
  1. initialize array with `val = -1`
  2. if `find(a)` equals to `find(b)`, it means `a` and `b` are connected
2. find order: [topological sort - Kahn's algorithm](https://en.wikipedia.org/wiki/Topological_sorting#Kahn.27s_algorithm)
  1. find start node with no incoming edges, and add them to a set
  2. start search from the set, check each of its neighbors.
  3. for each neighbor, remove the edge between itself and parent.
  4. if it has no incoming edges, add it to result set
