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
