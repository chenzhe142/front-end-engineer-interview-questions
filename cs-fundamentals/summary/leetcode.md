# leetcode

## [Kadane's algorithm](https://en.wikipedia.org/wiki/Maximum_subarray_problem)
1. maximum subarray
2. best time to buy & sell stocks (I, II, III, IV)
  - [I](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/): the logic is to calculate the difference ``(maxCur += prices[i] - prices[i-1])`` of the original array, and find a contiguous subarray giving maximum profit. If the difference falls below 0, reset it to zero.
  - [III](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/#/description): dynamic programming `dp[k][prices.length]`


## Depth first search

## Bucket sort: sort in linear time. usually the data range is known.
1. [H-index](https://leetcode.com/problems/h-index/#/description)
