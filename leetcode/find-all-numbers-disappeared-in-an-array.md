# 448. Find All Numbers Disappeared in an Array

* *Difficulty: Easy*

* *Topics: Array*

* *Similar Questions:*

  * [First Missing Positive](first-missing-positive.md)

  * [Find All Duplicates in an Array](find-all-duplicates-in-an-array.md)

## Problem:

<p>Given an array of integers where 1 &le; a[i] &le; <i>n</i> (<i>n</i> = size of array), some elements appear twice and others appear once.</p>

<p>Find all the elements of [1, <i>n</i>] inclusive that do not appear in this array.</p>

<p>Could you do it without extra space and in O(<i>n</i>) runtime? You may assume the returned list does not count as extra space.</p>

<p><b>Example:</b>
<pre>
<b>Input:</b>
[4,3,2,7,8,2,3,1]

<b>Output:</b>
[5,6]
</pre>
</p>
## Solutions:

```c++
class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int>& nums) {
        for (int i = 0; i < nums.size(); ++i) {
            if (nums[i] == i + 1)   continue;
            int kickout = nums[i];
            nums[i] = 0;
            
            while (kickout != 0 && nums[kickout-1] != kickout) {
                swap(kickout, nums[kickout-1]);
            }
        }
        
        vector<int> ret;
        for (int i = 0; i < nums.size(); ++i) {
            if (nums[i] != i + 1) {
                ret.push_back(i + 1);
            }
        }
        
        return ret;
    }
};
```
