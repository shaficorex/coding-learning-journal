# Problem Statement

Given an array of integers `arr`, and three integers `a`, `b`, and `c`. You need to find the number of *good triplets*.

## Definition of a Good Triplet
A triplet `(arr[i], arr[j], arr[k])` is considered *good* if the following conditions are true:

- `0 <= i < j < k < arr.length`
- `|arr[i] - arr[j]| <= a`
- `|arr[j] - arr[k]| <= b`
- `|arr[i] - arr[k]| <= c`

Where `|x|` denotes the absolute value of `x`.

## Objective
Return the number of *good triplets*.

## Example 1
**Input:**
```plaintext
arr = [3,0,1,1,9,7], a = 7, b = 2, c = 3
```
**Output:**
```plaintext
4
```
**Explanation:** There are 4 good triplets: `(3,0,1)`, `(3,0,1)`, `(3,1,1)`, `(0,1,1)`.



```cpp
class Solution {
public:
    int countGoodTriplets(vector<int>& arr, int a, int b, int c) {
        
        int n=arr.size();
        int count=0;
        for(int i=0;i<n-2;i++)
        {
            for(int j=i+1;j<n-1;j++)
            {
                if(abs(arr[i]-arr[j])<=a) //this is slightly optimized. if this false we no need to run loop for k
                {
                    for(int k=j+1;k<n;k++)
                    {
                        if(abs(arr[j]-arr[k])<=b && abs(arr[i]-arr[k])<=c) count++;
                    }
                }
                
            }
        }

        return count;
    }
};
