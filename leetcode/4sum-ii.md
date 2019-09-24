# 454. 4Sum II

* *Difficulty: Medium*

* *Topics: Hash Table, Binary Search*

* *Similar Questions:*

  * [4Sum](4sum.md)

## Problem:

<p>Given four lists A, B, C, D of integer values, compute how many tuples <code>(i, j, k, l)</code> there are such that <code>A[i] + B[j] + C[k] + D[l]</code> is zero.</p>

<p>To make problem a bit easier, all A, B, C, D have same length of N where 0 &le; N &le; 500. All integers are in the range of -2<sup>28</sup> to 2<sup>28</sup> - 1 and the result is guaranteed to be at most 2<sup>31</sup> - 1.</p>

<p><b>Example:</b></p>

<pre>
<b>Input:</b>
A = [ 1, 2]
B = [-2,-1]
C = [-1, 2]
D = [ 0, 2]

<b>Output:</b>
2

<b>Explanation:</b>
The two tuples are:
1. (0, 0, 0, 1) -&gt; A[0] + B[0] + C[0] + D[1] = 1 + (-2) + (-1) + 2 = 0
2. (1, 1, 0, 0) -&gt; A[1] + B[1] + C[0] + D[0] = 2 + (-1) + (-1) + 0 = 0
</pre>

<p>&nbsp;</p>

## Solutions:

```c++
class Solution {
public:
    int fourSumCount(vector<int>& A, vector<int>& B, vector<int>& C, vector<int>& D) {
        unordered_map<int, int> valueFreq;
        
        for (int i = 0; i < A.size(); ++i) {
            for (int j = 0; j < B.size(); ++j) {
                ++valueFreq[A[i] + B[j]];
            }
        }
        
        int count = 0;
        for (int i = 0; i < C.size(); ++i) {
            for (int j = 0; j < D.size(); ++j) {
                count += valueFreq[-C[i] - D[j]];
            }
        }
        
        return count;
    }
};
```