
<details>

  <summary><b>Selection Sort</b></summary>

  # Key Idea

Repeatedly find the minimum element from the unsorted portion and place it at the beginning.

## 🔍 Explanation
Divide the array into two parts:
- Sorted (left)
- Unsorted (right)

For each position `i`, find the minimum element from `i` to `n-1` and swap it with `i`.

## 🧠 Step-by-Step Logic
1. Start from index 0.
2. Assume current index is the minimum.
3. Traverse the rest of the array to find the actual minimum.
4. Swap with the current index.
5. Repeat for next index.

## 💻 Code Example
```cpp
void selectionSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 0; i < n - 1; i++) {
        int minIndex = i;
        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        swap(arr[i], arr[minIndex]);
    }
}
```

## ⚠️ Important Notes
- Time Complexity: O(n²)
- Always performs `n-1` swaps (not optimized)

## ❌ Common Mistakes
- Starting inner loop from `j = i` instead of `i + 1`
- Forgetting to update `minIndex`

</details>


<details>

  <summary><b>Bubble Sort</b></summary>

# Bubble Sort Algorithm

Repeatedly swap adjacent elements if they are in the wrong order.

## 🔍 Explanation
- In each pass, the largest element moves to the end.
- After each iteration, the unsorted portion reduces.

## 🧠 Step-by-Step Logic
1. Compare adjacent elements.
2. Swap if left > right.
3. Repeat for all elements.
4. Reduce range after each pass.

## 💻 Code Example
```cpp
void bubbleSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = n - 1; i > 0; i--) {
        bool swapped = false;
        for (int j = 0; j < i; j++) {
            if (arr[j] > arr[j + 1]) {
                swap(arr[j], arr[j + 1]);
                swapped = true;
            }
        }
        if (!swapped) break; // optimization
    }
}
```

## ⚠️ Important Notes
- **Time Complexity:**
  - Worst: `O(n²)`
  - Best: `O(n)` (if already sorted with optimization)

## ❌ Common Mistakes
- Not reducing inner loop range.
- Forgetting optimization flag (`swapped`).
</details>


<details>

  <summary><b>Insertion Sort</b></summary>

  # Key Idea

Build the sorted array one element at a time by inserting elements into their correct position.

## 🔍 Explanation
- Compare current element with previous elements
- Shift elements to the right until correct position is found

## 🧠 Step-by-Step Logic
1. Start from index 1
2. Compare with previous elements
3. Shift larger elements right
4. Insert element at correct position

## 💻 Code Example
```cpp
def insertionSort(vector<int>& arr):
    int n = arr.size()
    for (int i = 1; i < n; i++) {
        int j = i;
        while (j > 0 && arr[j] < arr[j - 1]) {
            swap(arr[j], arr[j - 1]);
            j--;
        }
    }
}
```

## ⚠️ Important Notes
- **Time Complexity:**
  - Worst: O(n²)
  - Best: O(n) (already sorted)
- Efficient for small datasets

## ❌ Common Mistakes
- Forgetting `j > 0` condition
- Incorrect comparison direction
</details>


<details>

  <summary><b>Merge Sort</b></summary>

  # Key Idea

**Use divide and conquer:**

- Divide array into halves
- Recursively sort each half
- Merge sorted halves

## 🔍 Explanation

Keep dividing until single-element arrays (base case)
Merge two sorted arrays into one

## 🧠 Step-by-Step Logic

- Divide array using mid
- Recursively sort left and right halves
- Merge both sorted halves

## 💻 Code Example
```cpp
to merge(vector<int>& arr, int low, int mid, int high) {
    vector<int> temp;
    int left = low;
    int right = mid + 1;

    while (left <= mid && right <= high) {
        if (arr[left] <= arr[right]) {
            temp.push_back(arr[left++]);
        } else {
            temp.push_back(arr[right++]);
        }
    }

    while (left <= mid) temp.push_back(arr[left++]);
    while (right <= high) temp.push_back(arr[right++]);

    for (int i = low; i <= high; i++) {
        arr[i] = temp[i - low];
    }
}

void mergeSort(vector<int>& arr, int low, int high) {
    if (low >= high) return;

    int mid = (low + high) / 2;
    mergeSort(arr, low, mid);
    mergeSort(arr, mid + 1, high);
    merge(arr, low, mid, high);
}
```

## ⚠️ Important Notes
- **Time Complexity:** O(n log n)
- **Space Complexity:** O(n) (extra array used)
- Stable sorting algorithm

## ❌ Common Mistakes 
- Incorrect base case (`low >= high`)
- Not copying back from temp array properly 
- Index mismatch (`temp[i - low]`)

</details>


# Key Takeaways

- **Selection Sort:** Simple but inefficient, fixed swaps
- **Bubble Sort:** Easy, can be optimized for sorted arrays
- **Insertion Sort:** Efficient for small or nearly sorted data
- **Merge Sort:** Efficient and scalable, uses recursion

<details>

  <summary><b>Hand Note for merge sort</b></b></summary>

  ![merge1](https://github.com/user-attachments/assets/66de6c9c-b0da-41eb-a6fc-d84aac48454e)



</detail![merge2](https://github.com/user-attachments/assets/0c5da2d8-d4b7-4a00-9610-25fef316090f)
s>


![merge3](https://github.com/user-attachments/assets/8c19fec2-8bab-4285-b76f-6fad197d4127)



![merge4](https://github.com/user-attachments/assets/cbfff21d-43e1-46c7-aab2-6524e73b4fd0)
</details>

<details>
  <summary><b>Hand Note for all sort</b></summary>

  ![sort1](https://github.com/user-attachments/assets/6007f0d8-bb9e-4ac0-b8e7-d05eba45e952)

![Uploading sort2.jpeg…]()

</details>
