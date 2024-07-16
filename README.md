# Hash_Table
### 3146. Permutation Difference between Two Strings
[LeetCode Link](https://leetcode.com/problems/permutation-difference-between-two-strings/description/)
<br />
You are given two strings s and t such that every character occurs at most once in s and t is a permutation of s.
The permutation difference between s and t is defined as the sum of the absolute difference between the index of the occurrence of each character in s and the index of the occurrence of the same character in t.
Return the permutation difference between s and t.

Input: s = "abc", t = "bac"
Output: 2
<br />
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
  #### Other Method Using *HASHMAP*
  ```java
  class Solution
  {
    public int findPermutationDifference(String s, String t)
    {
        int c=0;
        HashMap<Character,Integer> map1=new HashMap<Character,Integer>();
        HashMap<Character,Integer> map2=new HashMap<Character,Integer>();
        for(int i=0;i<s.length();i++){
            map1.put(s.charAt(i),i);
            map2.put(t.charAt(i),i);
        }
        for(int i=0;i<s.length();i++)
        {
            c=c+Math.abs(map1.get(s.charAt(i))-map2.get(s.charAt(i)));
        }
        return c;
    }
  }
  ```

#### Other Method Using *indexOf* function
```java
class Solution {
    public int findPermutationDifference(String s, String t) {
        int sum = 0;
        for(int i=0;i<s.length();i++) {
            char c = s.charAt(i);
            int id = t.indexOf(c);
            sum += Math.abs(i-id);
        }
        return sum;
    }
}
```
### 771. Jewels and Stones
[LeetCode Link](https://leetcode.com/problems/jewels-and-stones/)
<br />
You're given strings jewels representing the types of stones that are jewels, and stones representing the stones you have. Each character in stones is a type of stone you have. You want to know how many of the stones you have are also jewels.
Letters are case sensitive, so "a" is considered a different type of stone from "A".

Input: jewels = "aA", stones = "aAAbbbb"
Output: 3
```java
class Solution {
    public int numJewelsInStones(String jewels, String stones) {
        int c=0;
        int[] arr1=new int[256];
        for(int j=0;j<stones.length();j++) arr1[stones.charAt(j)]++;
        for(int i=0;i<jewels.length();i++)
        {
            c=c+arr1[jewels.charAt(i)];
        }
        return c;
    }
}
```

