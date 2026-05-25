# 3Sum Problem — Two Pointer Approach

## Concept Overview

The 3Sum problem asks us to find all unique triplets in an array such that:

```plaintext
nums[i] + nums[j] + nums[k] == 0
```
where:
- `i != j`
- `j != k`
- `i != k`

**The main challenges are:**
- Avoiding duplicate triplets
- Improving time complexity from brute force O(n³)

This optimized solution uses:
- Sorting
- Two Pointer Technique
- Duplicate skipping

## Optimized Approach
### Key Idea
1. Sort the array.
2. Fix one element using a loop.
3. Use two pointers to find the remaining two numbers.
4. Skip duplicates to avoid repeated triplets.

### Time Complexity
| Approach | Complexity |
| --- | --- |
| Brute Force | O(n³) |
| Optimized Two Pointer | O(n²) |

**Brute force:**

```cpp
#include <vector>
#include <set>
#include <algorithm>

// Function to find all unique triplets in the array which gives the sum of zero
std::vector<std::vector<int>> threeSum(std::vector<int>& nums) {
    std::set<std::vector<int>> st;

    for (int i = 0; i < nums.size(); i++) {
        for (int j = i + 1; j < nums.size(); j++) {
            for (int k = j + 1; k < nums.size(); k++) {
                if (nums[i] + nums[j] + nums[k] == 0) {
                    std::vector<int> temp = {nums[i], nums[j], nums[k]};
                    std::sort(temp.begin(), temp.end());
                    st.insert(temp);
                }
            }
        }
    }

    // Convert set to vector of vectors
    std::vector<std::vector<int>> ans(st.begin(), st.end());
    return ans;
}
```

**OPtimized:**

# Solution

```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {

        sort(nums.begin(), nums.end());

        vector<vector<int>> ans;
        int n = nums.size();

        for(int i = 0; i < n; i++)
        {
            // Skip duplicate fixed elements
            if(i > 0 && nums[i] == nums[i - 1]) continue;

            int j = i + 1;
            int k = n - 1;

            while(j < k)
            {
                int sum = nums[i] + nums[j] + nums[k];

                if(sum < 0) j++;    
                else if(sum > 0)  k--;
                else
                {
                    ans.push_back({nums[i], nums[j], nums[k]});

                    j++;
                    k--;

                    // Skip duplicate values
                    while(j < k && nums[j] == nums[j - 1]) j++;
                    while(j < k && nums[k] == nums[k + 1]) k--;
                }
            }
        }

        return ans;
    }
};
```

# Step-by-Step Logic

## Step 1 — Sort the Array
```cpp
sort(nums.begin(), nums.end());
```

**Sorting helps because:**
- Duplicates become adjacent
- Two pointer traversal becomes possible

**Example:**

Original array:
[-1, 0, 1, 2, -1, -4]

After sorting:
[-4, -1, -1, 0, 1, 2]

## Step 2 — Fix One Element
```cpp
for(int i = 0; i < n; i++)
```

**At each iteration:**
- `nums[i]` becomes the first element of the triplet.
- Search for two remaining numbers.

## Step 3 — Skip Duplicate Fixed Elements
```cpp
i > 0 && nums[i] == nums[i - 1]) continue;
```

This prevents repeated triplets.

**Without this condition:**
- Example array: `[-1, -1, 0, 1]`
- Would generate duplicate answers.

## Step 4 — Use Two Pointers
```cpp
int j = i + 1;
t int k = n - 1;
```
- `j` starts from the left side.
- `k` starts from the right side.


# Step 5 — Calculate Sum

```cpp
int sum = nums[i] + nums[j] + nums[k];
```

## Case 1 — Sum is Smaller

```cpp
if (sum < 0)
{
    j++;
}
```

*Move left pointer right to increase sum.*

## Case 2 — Sum is Larger

```cpp
else if (sum > 0)
{
    k--;
}
```

*Move right pointer left to decrease sum.*

## Case 3 — Valid Triplet Found

```cpp
e else {
    ans.push_back({nums[i], nums[j], nums[k]});
}
```

*Store the triplet.*

# Step 6 — Skip Duplicate Pairs

```cpp
while (j < k && nums[j] == nums[j - 1]) j++;
while (j < k && nums[k] == nums[k + 1]) k--;
```

*This ensures only unique triplets.*

# Step 5 — Calculate Sum

```cpp
int sum = nums[i] + nums[j] + nums[k];
```

## Case 1 — Sum is Smaller

```cpp
if (sum < 0)
{
    j++;
}
```

*Move left pointer right to increase sum.*

## Case 2 — Sum is Larger

```cpp
else if (sum > 0)
{
    k--;
}
```

*Move right pointer left to decrease sum.*

## Case 3 — Valid Triplet Found

```cpp
e else {
    ans.push_back({nums[i], nums[j], nums[k]});
}
```

*Store the triplet.*

# Step 6 — Skip Duplicate Pairs

```cpp
while (j < k && nums[j] == nums[j - 1]) j++;
while (j < k && nums[k] == nums[k + 1]) k--;
```

*This ensures only unique triplets.*



# Chunk of importent concept

<details>
  <summary><b>Sorting Technique</b></summary>

  ## When to Use

Use sorting when:
- ordered data can simplify the problem
- duplicates exist
- binary search or two pointers may help
- relative order matters

## What Sorting Helps With
| Problem Type | Benefit |
|----------------|---------|
| Pair Sum | Easier searching |
| Duplicate removal | Adjacent duplicates |
| Two pointers | Requires sorted array |
| Binary search | Requires sorting |

## Important Thinking Pattern

Ask:
> Will ordering the data simplify decisions?

If yes → sort first.
  
</details>

<details>
  <summary><b>Two Pointer Technique</b></summary>

  # When to Use

Usually used when:
- array/string is sorted
- searching pairs
- working from both ends
- need optimization

## Basic Structure
```c
int left = 0;
int right = n - 1;

while(left < right)
{
    // logic
}
```

## How Pointer Movement Works
- If sum is small, `left++` because increasing left increases sum.
- If sum is large, `right--` because decreasing right decreases sum.

## Where Used
| Problem | Usage |
| --- | --- |
| 3Sum | Find remaining 2 numbers |
| Valid Palindrome | Compare both ends |
| Container With Most Water | Move optimal side |
| Trapping Rain Water | Left-right traversal |

## Important Thinking Pattern
> Ask: Can I intelligently move from both ends instead of checking everything?
</details>

<details>
  <summary><b>Duplicate Skipping Technique</b></summary>

  # When to Use

## Use when:
- Problem asks for unique answers
- Duplicates exist
- Array is sorted

## How to Use
- Skip duplicate fixed elements:
  ```
  if(i > 0 && nums[i] == nums[i - 1]) continue;
  ```
- Skip duplicate pointers:
  ```
  while(left < right && nums[left] == nums[left - 1]) {
      left++;
  }
  ```

## Why Important
Without duplicate skipping, the array `[-1, -1, 0, 1]` may generate repeated triplets.

## Where Used
| Problem | Usage |
|---------|--------|
| 3Sum | Unique triplets |
| 4Sum | Unique quadruplets |
| Subset problems | Avoid repeated subsets |
| Combination Sum II | Avoid duplicate combinations |

## Important Thinking Pattern
**Ask:**
> Can repeated values generate repeated answers?
> If yes → handle duplicates.
</details>

<details>
  <summary><b>Fix One Element + Search Remaining</b></summary>

  # Core Idea

Instead of solving everything together:

- Fix part of the problem
- Solve smaller remaining problem

## Example in 3Sum
- Fix one number `nums[i]`
- Then solve:
  - Two Sum on remaining array

## Example Structure
```cpp
for(int i = 0; i < n; i++)
{
    // solve smaller problem
}
```

## Why Powerful?
It reduces complexity.

## Complexity Reduction Example
| Method | Complexity |
|---------|------------|
| Brute Force 3 loops | O(n) |
| Fix one + two pointers | O(n) |

## Where Used?
| Problem | Pattern |
|---------|---------|
| 3Sum | Fix 1, search 2 |
| 4Sum | Fix 2, search 2 |
| K Sum | Fix some, recurse remaining |
| Subarray problems | Fix start, expand end |

## Important Thinking Pattern
Ask:
> Can I reduce the problem dimension?

### Example:
- 3Sum → Two Sum
- 4Sum → 3Sum
</details>

