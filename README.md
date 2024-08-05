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
### 2053. Kth Distinct String in an Array
[Leetcode link](https://leetcode.com/problems/kth-distinct-string-in-an-array/description/?envType=daily-question&envId=2024-08-05)
<br>
A distinct string is a string that is present only once in an array.
Given an array of strings arr, and an integer k, return the kth distinct string present in arr. If there are fewer than k distinct strings, return an empty string "".
Note that the strings are considered in the order in which they appear in the array.

Example 1:
Input: arr = ["d","b","c","b","c","a"], k = 2
Output: "a"
Explanation:
The only distinct strings in arr are "d" and "a".
"d" appears 1st, so it is the 1st distinct string.
"a" appears 2nd, so it is the 2nd distinct string.
Since k == 2, "a" is returned. 

Example 2:
Input: arr = ["aaa","aa","a"], k = 1
Output: "aaa"
Explanation:
All strings in arr are distinct, so the 1st string "aaa" is returned.

Example 3:
Input: arr = ["a","b","a"], k = 3
Output: ""
Explanation:
The only distinct string is "b". Since there are fewer than 3 distinct strings, we return an empty string "".

#### Brute Force Solution:
```java
class Solution {
    public String kthDistinct(String[] arr, int k) {
        for(int i=0;i<arr.length;i++)
        {
            int f=0;
            for(int j=0;j<arr.length;j++)
            {
                if(i!=j && arr[i].equals(arr[j])) 
                {
                    f=1;
                    break;
                }
            }
            if(f==0) k--;
            if(k==0) return arr[i];
        }
        return "";
    }
}
```
#### Optimal Solution[HashMap]:
```java
class Solution {
    public String kthDistinct(String[] arr, int k) {
        HashMap<String,Integer> map = new HashMap<String,Integer>();
        for(String s:arr) map.put(s,map.getOrDefault(s,0)+1);
        for(String s:arr){
            if(map.get(s)==1) k--;
            if(k==0) return s;
        }
        return "";
    }
}
```

