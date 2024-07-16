# Hash_Table
### 3146. Permutation Difference between Two Strings
[LeetCode Link](https://leetcode.com/problems/permutation-difference-between-two-strings/description/)
```java
class Solution {
    public int findPermutationDifference(String s, String t) {
        int c=0;
        for(int i=0;i<s.length();i++){
            for(int j=0;j<t.length();j++){
                if(s.charAt(i)==t.charAt(j)) {
                    c=c+Math.abs(i-j);
                    break;
                }
            }
        }
        return c;
    }
}
```
- example : s="abc" t="bac"
- so the permutation difference for a=abs(0-1)
- for b=abs(1-0)
- for c=abs(2-2)
- so the total = 1+1+0 = 2 output will be 2
