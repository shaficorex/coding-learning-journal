# Leaders in an Array

## Concept Overview

A leader in an array is an element that is strictly greater than all elements to its right.
The rightmost element is always a leader because there are no elements to its right.

## Key Principles
- Traverse the array from right to left.
- Maintain a variable (`largest`) to track the maximum value seen so far.
- If the current element is greater than `largest`, it is a leader.
- Store leaders and reverse the result at the end to maintain original order.

## Explanation

Instead of comparing every element with all elements to its right (which is inefficient), we can optimize:

- Start from the last element.
- Keep updating the maximum value (`largest`).
- Any element greater than this maximum is a leader.

This reduces time complexity significantly.

## Code Example
```cpp
class Solution {
public:
    vector<int> leaders(vector<int>& nums) {
        vector<int> ans;
        int largest = INT_MIN;

        for(int i = nums.size() - 1; i >= 0; i--) {
            if(nums[i] > largest) {
                ans.push_back(nums[i]);
                largest = nums[i];
            }
        }

        reverse(ans.begin(), ans.end());
        return ans;
    }
};
```


# Brute Force Approach (For Understanding)

```cpp
vector<int> leaders(vector<int>& nums) {
    vector<int> ans;

    for(int i = 0; i < nums.size() - 1; i++) {
        bool isLeader = true;

        for(int j = i + 1; j < nums.size(); j++) {
            if(nums[i] < nums[j]) {
                isLeader = false;
                break;
            }
        }

        if(isLeader) ans.push_back(nums[i]);
    }

    ans.push_back(nums.back());
    return ans;
}
```

## Important Notes / Edge Cases
- Works with negative numbers as well.
- For a single-element array, that element is the only leader.
- Duplicate values:
  - Only considered leader if strictly greater than all elements to the right.
- Always reverse the result in optimal approach.

## Time and Space Complexity
| Approach     | Time Complexity | Space Complexity |
|--------------|-----------------|------------------|
| Brute Force  | O(n²)           | O(1)             |
| Optimal      | O(n)            | O(n)             |

## Common Mistakes
- Forgetting to reverse the result.
- Using `>=` instead of `>` (violates strict condition).
- Not initializing largest properly.
- Traversing from left instead of right in optimal approach.

## Key Takeaways
- Right-to-left traversal is key for optimization.
- Maintain a running maximum.
- This is a classic example of greedy observation + reverse traversal.
- Reduces complexity from O(n²) to O(n).
