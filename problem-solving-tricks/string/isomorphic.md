# Core Idea #
Two strings are isomorphic if characters in s can be replaced to get t, while maintaining a consistent one-to-one mapping.

## Rules: ##

Every character in s must map to exactly one character in t.

No two characters in s can map to the same character in t.

Mapping must be consistent throughout the string.


# Character Mapping Analysis

## Given Strings
- `s = paper`
- `t = title`

## Check character mapping position by position.

| Index | s | t | Mapping |
|-------|---|---|---------|
| 0     | p | t | p → t |
| 1     | a | i | a → i |
| 2     | p | t | p → t (same as before ✔) |
| 3     | e | l | e → l |
| 4     | r | e | r → e |

## Forward Mapping
- `p → t`
- `a → i`
- `e → l`
- `r → e`

## Reverse Mapping (Important)
- `t → p`
- `i → a`
- `l → e`
- `e → r`

Each character maps **uniquely**, so the strings are **isomorphic**.


# Correct Algorithm Idea (DSA thinking)

Use two hash maps:

- `maps`
- `mapt`

For each index:

1. Check if `s[i]` already maps to something different.
2. Check if `t[i]` already maps to another character.

If either happens → return `false`.



```cpp
class Solution {
   public:
    bool isomorphicString(string s, string t) {
        unordered_map<char, char> mpps;
        unordered_map<char, char> mppt;

        for (int i = 0; i < s.size(); i++) {
            if ((mpps.count(s[i]) && mpps[s[i]] != t[i]) ||
                (mppt.count(t[i]) && mppt[t[i]] != s[i])) {
                return false;
            } else {
                mpps[s[i]] = t[i];
                mppt[t[i]] = s[i];
            }
        }

        return true;
    }
};         //time-complixity O(n)
            //space-complixity O(1)  limited character
