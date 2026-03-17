# 📌 C++ `std::string` Fundamentals  
Storage, ASCII, Substring & Modification

---

## 🔹 Why This Concept Matters

Strings are heavily used in:

- Input parsing : The computer receives input as text.
Parsing means breaking it apart and converting it into the correct data types like integers, strings, arrays, etc.
- Pattern matching
- Sliding window problems
- Palindrome checking
- Frequency counting
- Interview-level DSA problems

Without understanding how `std::string` works internally, performance optimization becomes difficult.

---

<details>
  <summary><b>Core Theory</b></summary>

  ### 1️⃣ How `std::string` Stores Data

`std::string` stores characters in **contiguous memory**, similar to a dynamic array.

That means:

- Characters are stored sequentially.
- Random access is possible.
- Index access is **O(1)**.

### Example

```cpp
string s = "learning";

Index:  0 1 2 3 4 5 6 7
Value:  l e a r n i n g

s[2]  // 'a'  Time Complexity: O(1)
```

---

### 2.  ASCII Understanding

Every character is stored as an integer internally.

| Character Range | ASCII Range |
|----------------|------------|
| 'A' - 'Z'      | 65 – 90    |
| 'a' - 'z'      | 97 – 122   |
| '0' - '9'      | 48 – 57    |

This is important for:

- Character arithmetic
- Frequency arrays
- Case conversion
- Hashing tricks

```cpp
int val = 'A';   // 65
```
---


## 3. Substring

### Syntax
```cpp
s.substr(start, length);
```
Important:

- Second parameter is length, NOT ending index.
- If length is omitted → substring from start to end.

```cpp
string s = "learning";

s.substr(2, 5);  // "arnin"

/*Explanation:
Start at index 2 → take 5 characters.*/

s.substr(2);  // "arning"

```

### Time Complexity

O(k)
Where k = length of the substring.

### Reason:
substr() creates a new string and copies k characters into it.

---


</details>


<details>
  <summary><b>Correct Ways to Add Multiple Characters</b></summary>

  # Method 1 — Using +=

```csharp
string str = "Hello";
str += "[.]";
```

**Result:**

Hello[.]

This works because `+=` supports string concatenation.

---

# Method 2 — Using `append()`

```csharp
string str = "Hello";
str.append("[.]")
```

**Result:**

Hello[.]


# Important Notes

- `push_back()` → adds one character
- `+=` → adds strings or characters
- `append()` → adds strings or characters

## Function signatures:

```cpp
str.push_back(char c);
str += string;
str.append(string);
```

## Common Mistakes
1. Trying to insert multiple characters using `push_back()`

**Incorrect:**

```cpp
str.push_back("[.]");
```
**Reason:**

`push_back()` expects a `char`, not a `string`.

2. Confusing `char` and `string`
- `'.'`   // char
- `'"."'`   // string (note: in C++, double quotes denote a string)

## Key Takeaways
- `push_back()` is limited to inserting a **single character**.
- To insert **multiple characters or substrings**, use `+=` or `append()`.
- Understanding the difference between `char` and `string` is essential when working with C++ strings.


</details>



<details>
  <summary>Correct way to add character</summary>

  ```cpp
    //slow
    
    s = s + 'N';
    
    //better
    
    s += 'N';  // can do : s += "hello";
    
    //even better
    
    s.push_back('N');   // can not do : s.push_back("hello");   because it allows pushing single character
```

### Why?

Because s = s + 'N' may create a new string copy.

Time Complexity (amortized): O(1)

## 🔹 How It Works Internally

`std::string` is essentially a dynamic array wrapper around a character buffer.

It internally maintains:

- A pointer to a memory block (where characters are stored)
- The current **size** (number of characters used)
- The **capacity** (allocated memory size)

---


### 🔁 When Capacity Becomes Full

If you append characters and the capacity is exhausted:

1. A larger memory block is allocated.
2. Existing characters are copied to the new memory.
3. The old memory block is freed.

This resizing strategy is why `std::string` behaves efficiently in most cases.

---

## ⏱ Time Complexity Insights

- **Append (`push_back`, `+=`) → Amortized O(1)**  
  Most insertions do not trigger reallocation. Occasional resizing takes O(n), but spread over many operations it becomes amortized O(1).

- **Substring (`substr`) → O(k)**  
  Creates a new string and copies `k` characters.

- **Index Access (`s[i]`) → O(1)**  
  Direct memory access via pointer arithmetic.

---

</details>


<details>
  <summary><b>Logical Thinking</b></summary>

  When solving string problems, ask yourself:

- Can I use index access?
- Do I need ASCII conversion?
- Will `substring` cost extra time?
- Can I avoid copying by using two pointers instead?
- Is a frequency array better than `map`?

### Core Principle

Think performance first.

</details>


<details>
  <summary>C++ string Implementation Example</summary>

  ```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string s = "learning";

    // Access
    cout << s[2] << endl;  // a

    // ASCII
    int val = 'A';
    cout << val << endl;   // 65

    // Substring
    cout << s.substr(2, 5) << endl;  // arnin
    cout << s.substr(2) << endl;     // arning

    // Modify
    s[1] = 'B';
    cout << s << endl;  // lBarning

    // Append
    s.push_back('X');
    cout << s << endl;

    return 0;
}
```

---

## 🔹 Time & Space Complexity

| Operation      | Time Complexity     |
|---------------|--------------------|
| Index access  | O(1)               |
| Modify char   | O(1)               |
| Append        | Amortized O(1)     |
| Substring     | O(k)               |
| Length        | O(1)               |

---

## 🔹 Common Mistakes

- Thinking `substr(a, b)` means from index `a` to index `b`.  
  → The second parameter is **length**, not ending index.

- Using `s = s + char` inside loops.  
  → May cause repeated reallocations and degrade performance.

- Forgetting ASCII range values.  
  → Leads to incorrect character arithmetic.

- Creating unnecessary substrings inside loops.  
  → Can increase time complexity to **O(n²)** and cause TLE.


</details>
 


---

  ## 🔹 Key Learnings

- `std::string` behaves like a dynamic array of `char`.

- Understanding ASCII values is critical in DSA for:
  - Character arithmetic
  - Frequency counting
  - Case conversion
  - Digit manipulation

- `substr()` creates a new copy of characters → can be expensive.

- `push_back()` is more efficient than using `+` inside loops.

- Performance awareness is essential when solving string problems.


