---
title: Sort Colors
tags:
    - algorithms
    - array
    - sorting
    - two pointers
    - leetcode
    - interview
---

## Question
Given an array `nums` with `n` objects colored red, white, or blue, sort them **[in-place](https://en.wikipedia.org/wiki/In-place_algorithm)** so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers `0`, `1`, and `2` to represent the color red, white, and blue, respectively.

You must solve this problem without using the library's sort function.

**Example 1:**

**Input:** nums = [2,0,2,1,1,0]
**Output:** [0,0,1,1,2,2]

**Example 2:**

**Input:** nums = [2,0,1]
**Output:** [0,1,2]

**Constraints:**

- `n == nums.length`
- `1 <= n <= 300`
- `nums[i]` is either `0`, `1`, or `2`.

**Follow up:** Could you come up with a one-pass algorithm using only constant extra space?

## Key Idea
- Dutch National Flag Algorithm

## Initial Implementation

```cpp

class Solution {
public:
    void sortColors(vector<int>& nums) {


        int zeroCount = 0, oneCount = 0, twoCount = 0;

        for(int i = 0; i < nums.size(); i++) {
            if (nums[i] == 0) zeroCount++;
            if (nums[i] == 1) oneCount++;
            if (nums[i] == 2) twoCount++;
            
        }

        int i = 0;

        while(zeroCount > 0){

            nums[i] = 0;
            i++;
            zeroCount--;

        }

        while(oneCount > 0){

            nums[i] = 1;
            i++;
            oneCount--;

        }

        while(twoCount > 0){

            nums[i] = 2;
            i++;
            twoCount--;

        }

        return;
        
    }
};
```