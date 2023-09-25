## **Finding the Longest Increasing Subsequence in an Array**

### **Problem Statement**

Given an array of integers `nums`, return the length of its longest increasing subsequence (LIS). A subsequence is obtained from the original sequence by deleting zero or more elements without changing the order of the remaining elements.
https://leetcode.com/problems/longest-increasing-subsequence/

### **Understanding the Problem**

A naive approach to find the LIS is to generate all possible subsequences of the given sequence and check each subsequence to see if it's increasing and find its length. This brute force solution can be incredibly time-consuming, especially for larger arrays. Hence, an optimized dynamic programming approach is needed.

### **Dynamic Programming Strategy: The Key to the Solution**

The core idea is:

1. **Subproblem Decomposition**: The problem can be decomposed into overlapping subproblems. For each index `i` in `nums`, compute the length of the LIS ending at index `i`.
2. **Build Solutions Iteratively**: Use the solutions of smaller subproblems to construct the solution for the current subproblem.

### **Algorithmic Approach**

1. **Initialization**: Start by initializing an array `dp` of the same length as `nums` with all entries set to 1.
2. **Nested Loop**: Loop through each pair of indices `(i, j)` with `j < i`. If `nums[i]` is greater than `nums[j]`, then the sequence can be extended, and we update `dp[i]`.
3. **Result Extraction**: The maximum value in the `dp` array is the length of the LIS.

### **Time and Space Complexity**

The time complexity for this approach is \(O(n^2)\) because of the nested loop over the array. The space complexity is \(O(n)\) due to the `dp` array.

### **Detailed Walkthrough of the Example**

1. **Example: `lengthOfLIS([10,9,2,5,3,7,101,18])`**

   Starting with our `nums` array: `[10,9,2,5,3,7,101,18]`.

   - For `i = 0`: Only one number (10) is considered, so the LIS ending here is `[10]`. `dp[0]` is `1`.
   - For `i = 1`: We have numbers 10 and 9. The longest increasing subsequence ending in 9 is just `[9]`. `dp[1]` is `1`.
   - For `i = 2`: The LIS ending in 2 is `[2]`. `dp[2]` is `1`.
   - For `i = 3`: The LIS ending in 5 is `[2,5]`. `dp[3]` is `2`.
   - For `i = 4`: The LIS ending in 3 is `[2,3]`. `dp[4]` is `2`.
   - For `i = 5`: The LIS ending in 7 is `[2,3,7]`. `dp[5]` is `3`.
   - For `i = 6`: The LIS ending in 101 is `[2,3,7,101]`. `dp[6]` is `4`.
   - For `i = 7`: The LIS ending in 18 is `[2,3,7,18]`, but since the sequence `[2,3,7,101]` is longer, we'll consider that as the optimal solution for this subproblem. `dp[7]` is `4`.

   Given the `dp` array: `[1,1,1,2,2,3,4,4]`.

   The maximum value is `4`, which is the length of the longest increasing subsequence `[2,3,7,101]`.

### **Code Implementation**

```javascript
function lengthOfLIS(nums) {
    if (nums.length === 0) {
        return 0;
    }
    
    // Initialize the dp array with 1s
    let dp = new Array(nums.length).fill(1);

    // Nested loop to find LIS for every index
    for (let i = 1; i < nums.length; i++) {
        for (let j = 0; j < i; j++) {
            if (nums[i] > nums[j]) {
                dp[i] = Math.max(dp[i], dp[j] + 1);
            }
        }
    }
    
    // Find and return the maximum value in dp, which represents the length of LIS
    return Math.max(...dp);
}

console.log(lengthOfLIS([10,9,2,5,3,7,101,18]));  // Outputs: 4
```
