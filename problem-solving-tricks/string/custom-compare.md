# Custom Comparator and Sorting by Frequency in C++

## Concept Learned
Understanding how to implement a **custom comparator function** in C++ and why associative containers like `unordered_map` cannot be sorted directly using `std::sort`.

This learning focused on how to:

- Count character frequencies
- Convert map data into a sortable container
- Apply a custom comparison rule during sorting

---



# Problem Scenario

Given a string, determine the frequency of each character and return the characters sorted by:

1. **Higher frequency first**
2. **If frequencies are equal, sort alphabetically**


# Analysis of the Input Data

**Input:** "tree"

**Frequency:**
- t → 1
- r → 1
- e → 2

## Sorted Order

- e → 2
- r → 1
- t → 1

## Output

```json
[e, r, t]
```
---
# Key Learning Points

> [!IMPORTANT]
## 1. `unordered_map` Cannot Be Sorted 
- `unordered_map` stores elements using a **hash table**, so its iterators are **not random-access iterators**.
- `sort()` requires random-access iterators.
- Therefore, sorting directly is invalid.

### Correct Approach:
1. Move elements into a vector.
2. Sort the vector.

>  [!IMPORTANT]
## 2. Custom Comparator Function
- Defines the ordering rule between two elements.
- General form:
```cpp
bool cmp(Type a, Type b)
{
    return condition;
}
```
>  [!IMPORTANT]
- Rules:
  - Return true if `a` should come before `b`.
  - Return false otherwise.

  >  [!IMPORTANT]

## 3. Multi-Condition Comparator Logic
### Sorting rule implemented:
- Higher frequency first.
- If equal frequency → alphabetical order.
### Comparator:
```cpp
satic bool cmp(pair<char,int> a, pair<char,int> b)
{
    if(a.second == b.second)
        return a.first < b.first;
    return a.second > b.second;
}
```

# Explanation

| Condition | Meaning |
| --- | --- |
| `a.second > b.second` | Higher frequency first |
| `a.first < b.first` | Alphabetical order when frequency equal |

>  [!VERY VERY IMPORTANT]

## 4. Converting Map to Vector

To enable sorting, copy map elements into a vector:

```cpp
vector<pair<char,int>> vec(mpp.begin(), mpp.end());
```

Now the vector can be sorted.


## Full implimentation ##

```cpp
class Solution {
   public:
    static bool cmp(pair<char, int> a, pair<char, int> b) {
        if (a.second == b.second)
            return a.first < b.first;
        else
            return a.second > b.second;
    }
    vector<char> frequencySort(string& s) {
        unordered_map<char, int> mpp;

        for (char ele : s) {
            mpp[ele]++;
        }

        vector<pair<int, char>> vec(mpp.begin(), mpp.end());

        sort(vec.begin(), vec.end(), cmp);

        vector<char> v;

        for (auto ele : vec) {
            v.push_back(ele.first);
        }

        return v;
    }
};
```

# Algorithm Workflow

**Input String**
```
     │
     ▼
Count frequencies (unordered_map)
     │
     ▼
Convert map → vector<pair>
     │
     ▼
Sort vector using custom comparator
     │
     ▼
Extract characters into result vector
```

## Time Complexity

Let:
- `n` = length of string
- `k` = number of unique characters

| Step | Complexity |
| --- | --- |
| Frequency counting | O(n) |
| Vector creation | O(k) |
| Sorting | O(k log k) |

**Total complexity:**

`O(n + k log k)`


### Why `unordered_map` Cannot Be Sorted

`unordered_map` cannot be sorted using `std::sort()` because it **does not provide random access iterators**.

The `std::sort()` algorithm requires **random access iterators** to jump between elements (e.g., `it + n`). However, `unordered_map` only provides **forward iterators**, which allow traversal in one direction (`it++`) but not direct access to arbitrary positions.

Additionally, `unordered_map` is implemented using a **hash table**, where elements are stored in buckets based on their hash value. Therefore, elements are **not stored in any meaningful order**.

**Correct approach when sorting is required:**


First copy the elements into a `vector`, then apply sorting.


## Key Pattern Learned

A common competitive programming pattern:
- `unordered_map` → `vector<pair>` → custom sort

Used frequently for:
- Frequency problems
- Ranking problems
- Top-K elements

## Important C++ Rule Learned
When using a comparator inside a class with `sort()`, the comparator must be:
- static, or
- defined outside the class, or
- implemented using a lambda function.
Otherwise, `sort()` cannot access it.

## Practical Takeaway
When sorting data from hash maps or associative containers:
1. Store frequency in a map.
2. Convert to a vector.
3. Apply a custom comparator.
4. Extract required values.
