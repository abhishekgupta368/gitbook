# 343. Integer Break

* *Difficulty: Medium*

* *Topics: Math, Dynamic Programming*

* *Similar Questions:*

## Problem:

<p>Given a positive integer <i>n</i>, break it into the sum of <b>at least</b> two positive integers and maximize the product of those integers. Return the maximum product you can get.</p>

<p><strong>Example 1:</strong></p>

<div>
<pre>
<strong>Input: </strong><span id="example-input-1-1">2</span>
<strong>Output: </strong><span id="example-output-1">1</span>
<strong>Explanation: </strong>2 = 1 + 1, 1 &times; 1 = 1.</pre>

<div>
<p><strong>Example 2:</strong></p>

<pre>
<strong>Input: </strong><span id="example-input-2-1">10</span>
<strong>Output: </strong><span id="example-output-2">36</span>
<strong>Explanation: </strong>10 = 3 + 3 + 4, 3 &times;&nbsp;3 &times;&nbsp;4 = 36.</pre>

<p><b>Note</b>: You may assume that <i>n</i> is not less than 2 and not larger than 58.</p>
</div>
</div>
## Solutions:

```c++
class Solution {
public:
    int integerBreak(int n) {
        unordered_map<int, int> cache;
        if (n == 2) return 1;
        if (n == 3) return 2;
        
        return helper(n, cache);
    }
    
private:
    int helper(int n, unordered_map<int, int>& cache) {
        if (cache.count(n) > 0) return cache[n];
        if (n == 1) return 1;
        if (n == 2) return 2;
        if (n == 3) return 3;
        
        int prod1 = 2 * helper(n - 2, cache);
        int prod2 = 3 * helper(n - 3, cache);
        
        int ret = max(prod1, prod2);
        cache[n] = ret;
        return ret;
    }
};
```
