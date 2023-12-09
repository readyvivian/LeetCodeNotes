# Array

## 1. Two Sum

> Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
>
> You may assume that each input would have exactly one solution, and you may not use the same element twice.
>
> You can return the answer in any order.
>
> Example 1:
>
> Input: nums = [2,7,11,15], target = 9
> Output: [0,1]
> Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
>
> Example 2:
>
> Input: nums = [3,2,4], target = 6
> Output: [1,2]

### Approach

We can reduce the lookup time from $O(n)$ to $O(1)$ by trading space for speed.

A hash table supports fast lookup in near constant time ($O(1)$).

We add each element's value as a key and its index as a value to the hash table, because we look for complement value and need to get its index.

### Complexity

- Time complexity: $O(n)$.
- Space complexity: $O(n)$.

### Code

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            if (map.containsKey(complement)) {
                return new int[] { map.get(complement), i };
            }
            map.put(nums[i], i);
        }
        return null;
    }
}
```

## 121. Best Time to Buy and Sell Stock

> You are given an array `prices` where `prices[i]` is the price of a given stock on the ith day.
>
> You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.
>
> Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.
>
> Example 1:
>
> Input: prices = [7,1,5,3,6,4]
> Output: 5
> Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
> Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.
>
> Example 2:
>
> Input: prices = [7,6,4,3,1]
> Output: 0
> Explanation: In this case, no transactions are done and the max profit = 0.

### Approach

While iterating through the array of prices, we keep track of `min_price`, and update `max_profit` by comparing to `prices[i] - min_price`.

### Complexity

- Time complexity: $O(n)$.
- Space complexity: $O(1)$.

### Code

```java
class Solution {
    public int maxProfit(int[] prices) {
        int max_profit = 0;
        int min_price = prices[0];
        for (int i = 0; i < prices.length; i++) {
            max_profit = Math.max(prices[i] - min_price, max_profit);
            min_price = Math.min(prices[i], min_price);
        }
        return max_profit;
    }
}
```

## 57. Insert Interval

> You are given an array of non-overlapping intervals intervals where `intervals[i] = [start_i, end_i]` represent the start and the end of the ith interval and `intervals` is sorted in ascending order by `start_i`. You are also given an interval `newInterval = [start, end]` that represents the start and end of another interval.
>
> Insert `newInterval` into `intervals` such that `intervals` is still sorted in ascending order by `start_i` and `intervals` still does not have any overlapping intervals (merge overlapping intervals if necessary).
>
> Return `intervals` after the insertion.
>
> Example 1:
>
> Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
> Output: [[1,5],[6,9]]
>
> Example 2:
>
> Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
> Output: [[1,2],[3,10],[12,16]]
> Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].

