## **Finding Factors of a Number Efficiently in Node.js**

### **Problem Statement**

Given a number `n`, list all its factors. The factors of a number include all positive integers that can divide the given number without leaving a remainder.
https://leetcode.com/problems/the-kth-factor-of-n/

### **Understanding the Problem**

The simplest approach to find all factors of a number is to iterate from `1` to the number `n` and check for numbers which divide `n` without a remainder. This naive approach runs in \(O(n)\) time complexity. However, this isn't the most efficient. We can optimize it by only iterating till the square root of the number, thus reducing the time complexity.

### **Iterative Strategy: The Key to the Solution**

The primary strategy to efficiently determine all factors is:

1. **Iterate until the square root**: Only iterate up to the square root of the number to find factors, reducing the time complexity.
2. **Pair finding**: For each value `i` found that divides the number evenly, two factors are found: `i` itself and `n/i`.

### **Algorithmic Approach**

1. **Initialization**: Start by initializing an empty array `factors`.
2. **Iterative Check**: Loop from `1` to the square root of `n`. For every number `i` that divides `n` without leaving a remainder, push `i` and `n/i` into the `factors` array.
3. **Sorting (Optional)**: Sort the `factors` array to get the factors in ascending order.

### **Time and Space Complexity**

The time complexity for this approach is \(O(\sqrt{n})\) for the iteration plus \(O(f \log f)\) for sorting the factors, where \(f\) is the number of factors. However, since the number of factors is generally small for most numbers, the dominant time complexity is \(O(\sqrt{n})\).

The space complexity is \(O(f)\) where \(f\) is the number of factors. 

### **Example**
Let's walk through the example of finding factors for the number `28`.

### Factors Finding:

1. **Example: `getFactors(28)`**

   **Loop from `1` to square root of `28`:**
   - For `i = 1`, `28 % 1 == 0`, so add `1` and `28/1` to the factors.
   - For `i = 2`, `28 % 2 == 0`, so add `2` and `28/2` to the factors.
   ... (skipping numbers that don't divide 28)
   - For `i = 7`, `28 % 7 == 0`, so add `7` and `28/7` to the factors.

   **Final list of factors (after sorting):** `[1, 2, 4, 7, 14, 28]`

### **Code Implementation**

```javascript
function getFactors(num) {
    let factors = [];

    for (let i = 1; i <= Math.sqrt(num); i++) {
        if (num % i === 0) {
            factors.push(i);
            if (i !== num / i) {
                factors.push(num / i);
            }
        }
    }

    return factors.sort((a, b) => a - b);
}

console.log(getFactors(28));  // [1, 2, 4, 7, 14, 28]
```
