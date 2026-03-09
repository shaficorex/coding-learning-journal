# String Rotation by Shifting

## Given two strings:

- `s = "abcde"`
- `goal = "cdeab"`

You can shift a string by moving the first character to the end. This operation is called a **left rotation**.

The problem is to determine whether the string `goal` can be obtained by repeatedly shifting `s`.

## Example

**Initial string:**

```plaintext
s = "abcde" 
```

**After the first shift:**

```plaintext
s = "bcdea" 
```

**After the second shift:**

```plaintext
s = "cdeab" 
```

Now, `s` becomes equal to `goal`.

## Algorithm Trick

A common trick to solve this efficiently is **string doubling**.

1. Concatenate the string with itself:
   ```
   s = s + s 
   ```
2. Check whether `goal` exists as a substring inside the doubled string.
3. If `goal` appears inside `s + s`, then `goal` is a valid rotation of `s`.


```cpp
class Solution{	
	public:
		bool rotateString(string& s,string& goal){
            if(s.size()!=goal.size())return false;
            int size=s.size();
			s+=s;
            for(int i=0;i<size;i++)
            {
                if(s.substr(i,size)==goal)return true;
            }
            return false;
		}
};  //time-complexity O(n^2)
     //space-complexity O(n)  
```
