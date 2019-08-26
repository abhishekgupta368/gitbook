# 1083. Two Sum Less Than K

* *Difficulty: Easy*

* *Topics: Array*

* *Similar Questions:*

  * [Two Sum](two-sum.md)

  * [Two Sum II - Input array is sorted](two-sum-ii-input-array-is-sorted.md)

  * [3Sum Smaller](3sum-smaller.md)

  * [Subarray Product Less Than K](subarray-product-less-than-k.md)

## Problem:

<p>Given an array <code>A</code> of integers and&nbsp;integer <code>K</code>, return the maximum <code>S</code> such that there exists <code>i &lt; j</code> with <code>A[i] + A[j] = S</code> and <code>S &lt; K</code>. If no <code>i, j</code> exist satisfying this equation, return -1.</p>

<p>&nbsp;</p>

<p><strong>Example 1:</strong></p>

<pre>
<strong>Input: </strong>A = <span id="example-input-1-1">[34,23,1,24,75,33,54,8]</span>, K = <span id="example-input-1-2">60</span>
<strong>Output: </strong><span id="example-output-1">58</span>
<strong>Explanation: </strong>
We can use 34 and 24 to sum 58 which is less than 60.
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input: </strong>A = <span id="example-input-2-1">[10,20,30]</span>, K = <span id="example-input-2-2">15</span>
<strong>Output: </strong><span id="example-output-2">-1</span>
<strong>Explanation: </strong>
In this case it&#39;s not possible to get a pair sum less that 15.
</pre>

<p>&nbsp;</p>

<p><strong>Note:</strong></p>

<ol>
	<li><code>1 &lt;= A.length &lt;= 100</code></li>
	<li><code>1 &lt;= A[i] &lt;= 1000</code></li>
	<li><code>1 &lt;= K &lt;= 2000</code></li>
</ol>

## Solutions:

```c++
class Solution {
public:
    int twoSumLessThanK(vector<int>& A, int K) {
        if (A.size() < 2)   return -1;
        int ret = INT_MIN;
        int left = 0;
        int right = A.size() - 1;
        sort(A.begin(), A.end());
        while (left < right) {
            if (A[left] + A[right] >= K) {
                --right;
            } else {
                ret = max(ret, A[left] + A[right]);
                ++left;
            }
        }
        
        return ret == INT_MIN ? -1 : ret;
    }
};
```

It is possible to use count sort to reduce the space complexity from `O(nlogn)` to `O(n)`. 

[bucket sort strict O(n) solution](https://leetcode.com/problems/two-sum-less-than-k/discuss/328270/bucket-sort-strict-O(n)-solution)

```c++
class Solution {
    
    class Node {
        int v;
        int f;
        public Node(int v, int f) {
            this.v =v;
            this.f = f;
        }
        
        public String toString(){return v +"-" + f;}
    }
    public int twoSumLessThanK(int[] A, int k) {
        if(A == null || A.length < 1) return -1;
        
       
        int min = Integer.MAX_VALUE, max = Integer.MIN_VALUE;
        for(int a : A) {
            min = Math.min(min, a);
            max = Math.max(max, a);
        }
        
        Node[] buckets = new Node[max+1];
        for(int a : A) {
            if(buckets[a] == null) buckets[a] = new Node(a, 0);
            buckets[a].f ++;
        }
        
        Node cur = null;
        for(int i = 0; i<= max; i++) {
            if( buckets[i] != null && buckets[i].v == i) {
                cur = buckets[i];
            }
            
            buckets[i] = cur;
        }
        int sum = -1;
        
        for(int a : A) {
            int target = k - a - 1;
            if(target < min) continue;
            if(target > max) target = max;
            if(a == buckets[target].v && buckets[target].f == 1) continue;
            sum = Math.max(sum, buckets[target].v + a);
        }
        return sum;
    }
}
```