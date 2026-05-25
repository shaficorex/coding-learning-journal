# C++ Program to Check if a Number is an Integer

```cpp
#include <iostream>
#include <cmath>
using namespace std;

int main() {

    double x;
    cin >> x;

    // `floor(x)` returns the greatest integer less than or equal to `x`.

    // Examples:
    // floor(5.7) = 5
    // floor(3.2) = 3
    // floor(5.0) = 5

    // Here we are checking:
    // after removing the decimal part,
    // does the number remain the same or not?

    if (floor(x) == x)
    {
        // Example:
        // x = 5.0
        // floor(5.0) = 5
        // 5 == 5.0 -> true

        cout << "Integer";
    }
    else
    {
        // Example:
        // x = 5.8
        // floor(5.8) = 5
        // 5 != 5.8 -> false

        cout << "Not Integer";
    }
}
```
