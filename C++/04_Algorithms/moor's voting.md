# Moore’s Voting Algorithm (Majority Element)

## Concept Overview

Moore’s Voting Algorithm is an efficient technique to find the majority element in an array — an element that appears more than ⌊n/2⌋ times.

It works in O(n) time and O(1) space, making it optimal compared to approaches like hashing (which use extra memory).

## Key Principles
- A majority element dominates all other elements combined.
- If we pair each occurrence of the majority element with a different element, the majority element will still remain.
- The algorithm uses this idea of cancellation.

## Explanation

The algorithm runs in two phases:

### Phase 1: Find Candidate
Maintain:
- `candidate` (potential majority element)
- `count` (balance counter)
Traverse the array:
- If `count == 0`, select the current element as the new candidate.
- If the current element equals the candidate → increment `count`
- Otherwise → decrement `count`

This phase guarantees that if a majority element exists, it will be the final candidate.

### Phase 2: Verify Candidate
Count how many times the candidate appears.
If it appears more than n/2, it is the majority element.
Otherwise, no majority element exists.

## Code Example

# Solution Class

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {

        int count = 0;
        int val = nums[0];
        for (int i = 0; i < nums.size(); i++) {
            (nums[i] == val) ? count++ : count--;

            if (count == 0) {
                val = nums[i + 1];
            }
        }

        int doubleCount=0;
        for(int ele:nums)
        {
            if(ele==val)doubleCount++;
        }

        if(doubleCount>nums.size()/2) return val; return -1;
    }
};
```

# Step-by-Step Logic

## Example:

```plaintext
[7,7,5,7,5,1,5,7,5,5,7,7,5,5,5,5]
Start with count = 0
Pick first element as candidate
Increase count for same element
Decrease count for different element
When count becomes 0 → previous candidate is “neutralized”
Choose a new candidate
```

This process eliminates non-majority elements through cancellation.

## Important Notes / Edge Cases
- The algorithm always returns a candidate, even if no majority exists.
- That’s why verification step is mandatory.
- Works only for strict majority (> n/2).
- If the problem guarantees a majority element, the second pass can be skipped.

## Common Mistakes
- Updating candidate incorrectly (e.g., using `nums[i+1]` can cause out-of-bounds errors).
- Skipping the verification step when the majority is not guaranteed.
- Misunderstanding count:
  - It is not frequency; it is a balance counter.

## Key Takeaways
- Moore’s Voting Algorithm is based on pair cancellation.
- **Time Complexity:** O(n)
- **Space Complexity:** O(1)
- Requires two passes if majority is not guaranteed.
- More efficient than using a map when space matters.
