# Recursion in Programming

## Concept Overview

**Recursion** is a programming technique where a function calls itself to solve a problem.  
Instead of solving the entire problem at once, recursion breaks the problem into **smaller subproblems** of the same type.

Each recursive call creates a new **function frame in the call stack**, and these frames are removed when the function finishes execution.

Recursion continues until a **base condition** is reached that stops further recursive calls.

---

## Key Principles

### 1. Recursive Function Call

A recursive function calls itself during execution.

```cpp
void func() {
    func(); // recursive call
}
```
Without a stopping condition, this will lead to infinite recursion.


# 2. Call Stack Behavior

## Every time a function is called:
- A new stack frame is created in memory.
- Local variables and parameters are stored in that frame.

## A function returns when:
- It encounters the return statement.
- There are no more lines left to execute.

## When a function returns, its stack frame is removed from the stack.

## Example call stack behavior:
```
main()
 └── func(3)
      └── func(2)
           └── func(1)
                └── func(0)  <-- base case reached
```

Then the stack starts unwinding.


# 3. Base Case (Stopping Condition)

A recursive function must have a base case.

The base case is the condition where the function stops calling itself.

## Example:

```cpp
void print(int n) {
    if (n == 0) return; // base case
    cout << n << endl;
    print(n - 1);
}
```

## Without a base case:
- Recursive calls continue indefinitely
- The stack memory fills up
- This results in a **Stack Overflow**


# Output Order in Recursion

The position of the recursive call determines when operations execute.

## Case 1 — Work Before Recursive Call (Tail Recursion)

If the function performs work before calling itself:

```cpp
def print(int n) {
    if (n == 0) return;

    cout << n << " ";
    print(n - 1);
}
```

**Execution order:**

`3 2 1`

The output happens during the forward recursive calls.

This pattern is commonly called **Tail Recursion** because the recursive call is the last operation.

## Case 2 — Work After Recursive Call (Head Recursion / Backtracking)

If the function performs work after the recursive call:

```cpp
def print(int n) {
    if (n == 0) return;

    print(n - 1);
    cout << n << " ";
}
```

**Execution order:**

`1 2 3`

Here, the output happens while the recursion stack is unwinding.

This behavior is often described as **backtracking**.


# Step-by-Step Execution Example

## Example:

```cpp
void print(int n) {
    if (n == 0) return;

    print(n - 1);
    cout << n << " ";
}
```

## Function calls:
- `print(3)`
- `print(2)`
- `print(1)`
- `print(0)`  &larr; *base case*

## Stack unwinding:
- `print(1)` → output `1`
- `print(2)` → output `2`
- `print(3)` → output `3`

## Final output:
`1 2 3`

---

## Time and Space Complexity

### Time Complexity

If the function calls itself once per step:

**Time Complexity = O(N)**

Where **N** is the number of recursive calls.

### Space Complexity

Recursive functions use call stack memory.

**Space Complexity = O(N)**

Where **N** is the maximum recursion depth (number of active stack frames).

---

# Important Notes

- Recursion uses stack memory, so deep recursion can cause stack overflow.

- Every recursive problem can also be solved using iteration, but recursion often makes the solution cleaner.

- Recursion is commonly used in:
  - Tree traversal
  - Graph algorithms
  - Divide and conquer algorithms
  - Backtracking problems

# Common Mistakes

## Missing Base Case
```c
void func() {
    func(); // infinite recursion
}
```
This will cause a stack overflow.

## Incorrect Base Condition
If the base condition is wrong, recursion may stop too early or never stop.

## Too Many Recursive Calls
Example:
T(n) = 2T(n-1)
This can lead to exponential complexity.

# Key Takeaways
- Recursion is when a function calls itself.
- Every recursive call creates a new stack frame.
- A base case is mandatory to stop recursion.
- Code before the recursive call executes during forward recursion.
- Code after the recursive call executes during stack unwinding (backtracking).

## Typical Complexity:
- Time: O(N)
- Space: O(N) due to recursion stack.

<details>
    <summary><b>How to Solve Problems Using Recursion</b></summary>

## Core Idea
Recursion solves a problem by repeatedly calling the same function with a smaller input until a base condition is reached.

## 1. Convert Loop Logic to Recursion
Many problems solved with loops can also be solved using recursion.

**Conversion idea:**
- Loop condition → Base case
- Loop update → Recursive call

**Example concept:**
```c
for(i = 0; i < n; i++)
```
becomes
```c
if(i == n) return;
solve(i + 1);
```

## 2. Base Case
The base case is the condition that stops recursion.
It usually comes from:
- the loop stopping condition
- a break or termination condition inside the loop

If a recursive function does not reach a base case, it will continue calling itself and eventually cause a stack overflow.

## 3. Recursive Progress
Every recursive call must move the problem closer to the base case.

**Typical progression examples:**
- `i` → `i + 1`
- `n` → `n - 1`
- `(i, j)` → `(i + 1, j - 1)`

This guarantees that recursion eventually stops.

# 4. Example: Prime Number Check Using Recursion

```cpp
class Solution {
public:
    bool isPrime(int div, int num) {
        if (num <= 1) return false;
        else if (div * div > num)
            return true;
        else if (num % div == 0)
            return false;
        return isPrime(div + 1, num);
    }

    bool checkPrime(int num) {
        return isPrime(2, num);
    }
};
```
## Logic

- Start checking divisibility from 2.
- If `num <= 1`, the number is not prime.
- If `div * div > num`, no divisor exists up to √`num` → the number is prime.
- If `num % div == 0`, a divisor is found → not prime.
- Otherwise, continue checking the next divisor recursively.


  # 5. Two-Pointer Recursion Pattern

Some problems require working from both ends of a structure.

Use two indices:

- `i` → start position
- `j` → end position

## Base case

`i >= j`

When the pointers meet or cross, recursion stops.

This pattern is commonly used for:
- Palindrome checking
- Symmetric array comparison
- Problems involving both ends of a structure

## Key Points

- Recursion works by solving smaller versions of the same problem.
- A correct recursive function must contain:
  - a base case
  - a recursive call
  - progress toward termination
- Loop termination conditions often translate into recursion base cases.
- Two-pointer recursion is useful for problems involving start and end comparisons.
- Ensure every execution path returns a value.
</details>
