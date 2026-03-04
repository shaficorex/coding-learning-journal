## longest common prefix ##
just sort the string array and i will get the array sorted like dictionary.
Then compare  last and first string that's it.

### corner case ###
```
if (strs.empty()) return "";
f (strs.size() == 1) return strs[0];
```
### to compare ###
```
int i=0;     
 while (i < first.size() && i < last.size() && first[i] == last[i]) {
    i++;
}
```


### full solution ###

```
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        if (strs.empty()) return "";
        if (strs.size() == 1) return strs[0];
        
        sort(strs.begin(),strs.end());
        string first=strs[0];
        string last=strs.back();
       
        int i=0;
        
         while (i < first.size() && i < last.size() && first[i] == last[i]) {
            i++;
        }
        return first.substr(0,i);
    }
};
```

