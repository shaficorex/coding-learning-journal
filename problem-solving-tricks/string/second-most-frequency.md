# Second Most Frequent Element in an Array

## Problem
Given an array of integers `nums`, return the **second most frequent element**.  
If multiple elements have the same frequency, the **smaller element should be preferred**.

---

## Key Concept Learned

### 1. Using `map` for Frequency Counting
```cpp
map<int,int> mpp;
```

# Map in C++

In C++, a `map` stores keys in **sorted order (ascending)**. This guarantees that during iteration:

- Smaller keys appear first.
- If two elements have the same frequency, the smaller number naturally gets priority.

## Example

```cpp
nums = [4,4,2,2,3]
```

**Map contents:**

| Key | Value |
|---|---|
| 2 | 2 |
| 3 | 1 |
| 4 | 2 |

The map automatically keeps elements sorted by key.

## Frequency Counting

```cpp
for(int ele : nums)
{
    mpp[ele]++;
}
```

This counts how many times each number appears.

### Example:

```cpp
nums = [1,2,2,3,3,3]
```

**Frequency map:**

| Element | Frequency |
|---|---|
| 1 | 1 |
| 2 | 2 |
| 3 | 3 |

## Tracking Most and Second Most Frequent Elements

We maintain four variables:

| Variable     | Meaning                                   |
|--------------|--------------------------------------------|
| most_freq    | Highest frequency found so far             |
| most_ele     | Element with highest frequency             |
| second_freq  | Second highest frequency                   |
| second_ele   | Element with second highest frequency      |

# 4. Update Logic

## Case 1: New Most Frequent Element
```python
if (ele.second > most_freq):
```
   ### When this happens:
   The previous most frequent becomes second most.
   Then the current element becomes the new most frequent.
    
  
    second_freq = most_freq
    second_ele = most_ele
    
    most_freq = ele.second
    most_ele = ele.first


## Case 2: Candidate for Second Most Frequent
```python
e else if (ele.second > second_freq and ele.second < most_freq):
```
  ### Conditions:
  Frequency must be greater than current second
  Frequency must be less than most frequent
    
  ### Then update second most.
    second_freq = ele.second
    second_ele = ele.first

<details>
  <summary>Full code</summary>

  ```cpp
class Solution {
public:
    int secondMostFrequentElement(vector<int>& nums) {

        map<int,int> mpp;

        for(int ele : nums)
        {
            mpp[ele]++;
        }

        int most_freq = -1;
        int most_ele = -1;
        int second_freq = -1;
        int second_ele = -1;

        for(auto ele : mpp)
        {
            if(ele.second > most_freq)
            {
                second_freq = most_freq;
                second_ele = most_ele;

                most_freq = ele.second;
                most_ele = ele.first;
            }
            else if(ele.second > second_freq && ele.second < most_freq)
            {
                second_freq = ele.second;
                second_ele = ele.first;
            }
        }

        return second_ele;
    }
};
```
</details>


# Time Complexity

## Building Frequency Map
- **Time:** `O(n 
log n)`
- **Reason:**
  - Map insertion takes `O(
log n)`
  - Done for `n` elements.

## Traversing Map
- **Time:** `O(n)`

**Total Time Complexity:** `O(n 
log n)`

## Space Complexity
- **Space:** `O(n)`
- For storing the frequency map.

# Important Takeaway
Using `map` instead of `unordered_map` ensures:
- Sorted keys
- Consistent tie-breaking
- Correct result when frequencies are equal.
