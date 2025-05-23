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

### 3046. Split the Array
[Leetcode link](https://leetcode.com/problems/split-the-array/?envType=problem-list-v2&envId=hash-table&status=TO_DO&difficulty=EASY)
<br>
You are given an integer array nums of even length. You have to split the array into two parts nums1 and nums2 such that:
nums1.length == nums2.length == nums.length / 2.
nums1 should contain distinct elements.
nums2 should also contain distinct elements.
Return true if it is possible to split the array, and false otherwise.

Example 1:
Input: nums = [1,1,2,2,3,4]
Output: true
Explanation: One of the possible ways to split nums is nums1 = [1,2,3] and nums2 = [1,2,4].

Example 2:
Input: nums = [1,1,1,1]
Output: false
Explanation: The only possible way to split nums is nums1 = [1,1] and nums2 = [1,1]. Both nums1 and nums2 do not contain distinct elements. Therefore, we return false.

Constraints:
1 <= nums.length <= 100
nums.length % 2 == 0 
1 <= nums[i] <= 100

```java
class Solution {
    public boolean isPossibleToSplit(int[] nums) {
        HashMap<Integer,Integer> map = new HashMap<>();
        for(int i=0;i<nums.length;i++)
        {
            map.put(nums[i],map.getOrDefault(nums[i],0)+1);
        }
        int flag = 0;
        for(int x:map.keySet())
        {
            if(map.get(x)>2) flag = 1;
        }
        return flag==0;
    }
}
```
- In this code if we separate the array by half then the tow half will contain only the unique element then we return true other wise we return false.
- SO the idea is if any one element will qppear more than two times then thre must ne repeatation appear. Example 1 2 3 1 1 4 then we separate [1 2 1] [1 3 4] so repetation will occur.
- so first we find each elements frequency then we check if any one of the elemnt have more than three times that time we return false.   

### 2965. Find Missing and Repeated Values
[Leetcode link](https://leetcode.com/problems/find-missing-and-repeated-values/description/?envType=problem-list-v2&envId=hash-table&status=TO_DO&difficulty=EASY)
<br>
You are given a 0-indexed 2D integer matrix grid of size n * n with values in the range [1, n2]. Each integer appears exactly once except a which appears twice and b which is missing. The task is to find the repeating and missing numbers a and b.
Return a 0-indexed integer array ans of size 2 where ans[0] equals to a and ans[1] equals to b.
 
Example 1:
Input: grid = [[1,3],[2,2]]
Output: [2,4]
Explanation: Number 2 is repeated and number 4 is missing so the answer is [2,4].

Example 2:
Input: grid = [[9,1,7],[8,9,2],[3,4,6]]
Output: [9,5]
Explanation: Number 9 is repeated and number 5 is missing so the answer is [9,5].
 
Constraints:
2 <= n == grid.length == grid[i].length <= 50
1 <= grid[i][j] <= n * n
For all x that 1 <= x <= n * n there is exactly one x that is not equal to any of the grid members.
For all x that 1 <= x <= n * n there is exactly one x that is equal to exactly two of the grid members.
For all x that 1 <= x <= n * n except two of them there is exatly one pair of i, j that 0 <= i, j <= n - 1 and grid[i][j] == x.

```java
class Solution {
    public int[] findMissingAndRepeatedValues(int[][] grid) {
        boolean[] ans = new boolean[grid.length*grid.length+1];
        int sum = 0;
        int[] res = new int[2];
        for(int i=0;i<grid.length;i++)
        {
            for(int j=0;j<grid[0].length;j++)
            {
                if(ans[grid[i][j]]==true) res[0]=grid[i][j];
                else 
                {
                    ans[grid[i][j]]=true;
                    sum+=grid[i][j];
                }
            }
        }
        int n = grid.length*grid.length;
        res[1] = (n*(n+1)/2)-sum;
        return res;
    }
}
```
- the n*n grid will given that grid will contains the number from 1 to n*n but the one number is repeated and the another number is missing we find these two numbers from the grid.
- So we using the bool array of size n*n that will assign true if the value will accur. So we check if the grid[i][j] will true then it is the repeated value because it already appear so added to the result array.
- In corrosponding to we find the sum of the grids excluding the repeated value.
- So the total sum for the grid will must n*(n+1)/2 so we subtract our sum from that value we get the missing element.
### 2351. First Letter to Appear Twice
[Leetcode link](https://leetcode.com/problems/first-letter-to-appear-twice/?envType=problem-list-v2&envId=hash-table&status=TO_DO&difficulty=EASY)
<br>
Given a string s consisting of lowercase English letters, return the first letter to appear twice.
Note:
A letter a appears twice before another letter b if the second occurrence of a is before the second occurrence of b.
s will contain at least one letter that appears twice.

Example 1:
Input: s = "abccbaacz"
Output: "c"
Explanation:
The letter 'a' appears on the indexes 0, 5 and 6.
The letter 'b' appears on the indexes 1 and 4.
The letter 'c' appears on the indexes 2, 3 and 7.
The letter 'z' appears on the index 8.
The letter 'c' is the first letter to appear twice, because out of all the letters the index of its second occurrence is the smallest.

Example 2:
Input: s = "abcdd"
Output: "d"
Explanation:
The only letter that appears twice is 'd' so we return 'd'.

Constraints:
2 <= s.length <= 100
s consists of lowercase English letters.
s has at least one repeated letter.

```java
class Solution {
    public char repeatedCharacter(String s) {
        HashMap<Character,Integer> map = new HashMap<>();
        for(int i=0;i<s.length();i++)
        {
            if(map.containsKey(s.charAt(i))) return s.charAt(i);
            else map.put(s.charAt(i),i);
        }
        return 'a';
    }
}
```
- in this code we return the twice appear character first.
- So we create a hashmap and we put the character one by one from the string if the character is already present in the string that time we return that character because that character is the first repeating character.

### 2248. Intersection of Multiple Arrays
[Leetcode link](https://leetcode.com/problems/intersection-of-multiple-arrays/?envType=problem-list-v2&envId=hash-table&status=TO_DO&difficulty=EASY)
<br>
Given a 2D integer array nums where nums[i] is a non-empty array of distinct positive integers, return the list of integers that are present in each array of nums sorted in ascending order.

Example 1:
Input: nums = [[3,1,2,4,5],[1,2,3,4],[3,4,5,6]]
Output: [3,4]
Explanation: 
The only integers present in each of nums[0] = [3,1,2,4,5], nums[1] = [1,2,3,4], and nums[2] = [3,4,5,6] are 3 and 4, so we return [3,4].

Example 2:
Input: nums = [[1,2,3],[4,5,6]]
Output: []
Explanation: 
There does not exist any integer present both in nums[0] and nums[1], so we return an empty list [].

Constraints:
1 <= nums.length <= 1000
1 <= sum(nums[i].length) <= 1000
1 <= nums[i][j] <= 1000
All the values of nums[i] are unique.

```java
class Solution {
    public List<Integer> intersection(int[][] nums) {
        HashMap<Integer,Integer> map = new HashMap<>();
        for(int i=0;i<nums.length;i++)
        {
            for(int j=0;j<nums[i].length;j++)
            {
                map.put(nums[i][j],map.getOrDefault(nums[i][j],0)+1);
            }
        }
        ArrayList<Integer> ans = new ArrayList<>(map.keySet());
        Collections.sort(ans);
        ArrayList<Integer> res = new ArrayList<>();
        for(int x:ans)
        {
            if(map.get(x)>=nums.length) res.add(x);
        }
        return res;
    }
}
```
- In this code we return the integers which are present all the rows of the array.
- we add all the elements count to the hashmap using get or default value another one advantage is the each row contains the unique elements.
- then we return the res in asending order so what we do is we add the maps key value to the array list and sort the array list first.
- then we check each keys value if the value is greater than the rows count then that will added to the result list finally we return the result.

### 3120. Count the Number of Special Characters I
[Leetcode link](https://leetcode.com/problems/count-the-number-of-special-characters-i/?envType=problem-list-v2&envId=hash-table&status=TO_DO&difficulty=EASY)
<br>
You are given a string word. A letter is called special if it appears both in lowercase and uppercase in word.
Return the number of special letters in word.
 
Example 1:
Input: word = "aaAbcBC"
Output: 3

Explanation:
The special characters in word are 'a', 'b', and 'c'.

Example 2:
Input: word = "abc"
Output: 0
Explanation:
No character in word appears in uppercase.

Example 3:
Input: word = "abBCab"
Output: 1
Explanation:
The only special character in word is 'b'.
 
Constraints:
1 <= word.length <= 50
word consists of only lowercase and uppercase English letters.

```java
class Solution {
    public int numberOfSpecialChars(String word) {
        int c = 0;
        for(char i='a';i<='z';i++)
        {
            String s = Character.toString(i);
            if(word.contains(s.toUpperCase()) && word.contains(s)) c++;
        }
        return c;
    }
}
```
- In this code we return the count of the character which are presen tin the string in both upper and lowercase alphabet.
- So i travel through a to z then each character i chech wheather the lowercase i and the uppercase i will present in the string or not if it is present then we increase the c.
- Finaly we return the c.
### 2501. Longest Square Streak in an Array
[Leetcode link](https://leetcode.com/problems/longest-square-streak-in-an-array/?envType=daily-question&envId=2024-10-28)
<br>
You are given an integer array nums. A subsequence of nums is called a square streak if: The length of the subsequence is at least 2, and after sorting the subsequence, each element (except the first element) is the square of th previous number. Return the length of the longest square streak in nums, or return -1 if there is no square streak. A subsequence is an array that can be derived from another array by deleting some or no elements without changing the order of the remaining elements.

Example 1:
Input: nums = [4,3,6,16,8,2]
Output: 3
Explanation: Choose the subsequence [4,16,2]. After sorting it, it becomes [2,4,16].
- 4 = 2 * 2.
- 16 = 4 * 4.
Therefore, [4,16,2] is a square streak.
It can be shown that every subsequence of length 4 is not a square streak.

Example 2:
Input: nums = [2,3,5,6,7]
Output: -1
Explanation: There is no square streak in nums so return -1.
 
Constraints:
2 <= nums.length <= 105
2 <= nums[i] <= 105

```java
class Solution {
    public int longestSquareStreak(int[] nums) {
        Arrays.sort(nums);
        int max = 0;
        HashMap<Integer,Integer> map = new HashMap<>();
        for(int i=nums.length-1;i>=0;i--)
        {
            if(map.containsKey(nums[i]*nums[i]))
            {
                int val = map.get(nums[i]*nums[i])+1;
                max = Math.max(max,val);
                map.put(nums[i],val);
            }
            else map.put(nums[i],1);
        }
        if(max==0) max = -1;
        return max;
    }
}
```
- In this code we find the longest subsequence with continous square values of previous one.
- So first i sor the array and then travel through the last element if the current elements square is already present in the array that time we get the value and put the curent value.
- If it is not present we put the nums value.
- finally we return max. max will be updated each val time.
### 3223. Minimum Length of String After Operations
[Leetcode link](https://leetcode.com/problems/minimum-length-of-string-after-operations/description/?envType=daily-question&envId=2025-01-13)
<br>
You are given a string s.

You can perform the following process on s any number of times:

Choose an index i in the string such that there is at least one character to the left of index i that is equal to s[i], and at least one character to the right that is also equal to s[i].
Delete the closest character to the left of index i that is equal to s[i].
Delete the closest character to the right of index i that is equal to s[i].
Return the minimum length of the final string s that you can achieve.

 

Example 1:

Input: s = "abaacbcbb"

Output: 5

Explanation:
We do the following operations:

Choose index 2, then remove the characters at indices 0 and 3. The resulting string is s = "bacbcbb".
Choose index 3, then remove the characters at indices 0 and 5. The resulting string is s = "acbcb".
Example 2:

Input: s = "aa"

Output: 2

Explanation:
We cannot perform any operations, so we return the length of the original string.

 

Constraints:

1 <= s.length <= 2 * 105
s consists only of lowercase English letters.

```java
class Solution {
    public int minimumLength(String s) {
        int c = 0;
        int[] right = new int[26];
        int[] left = new int[26];
        for(int i=0;i<s.length();i++)
        {
            right[s.charAt(i)-'a']++;
        }
        left[s.charAt(0)-'a'] += 1;
        right[s.charAt(0)-'a'] -= 1;
        for(int i=1;i<s.length();i++)
        {
            right[s.charAt(i)-'a']--;
            for(int j=0;j<26;j++)
            {
                if((left[j]>=1 && right[j]>=1) && (j==s.charAt(i)-'a')) 
                {
                    c++;
                    left[j]--;
                    right[j]--;
                }
            }
            left[s.charAt(i)-'a']++;
        }
        System.out.print(c);
        return s.length()-(c*2);
    }
}
```
- In this code we find left and right count of the current character initailly all are in the right side.
- So find right character then for the zeroth position increase the left count of the character as weill as decrease the right count of the character.
- then travel through each element we remove the current characters left and right occurence.
- So for the index 1 that is the current index did not add both left and right side now that count only in the right side so we decrease then travel with 0 to 26 which character is equal to the current character as well as that characters count is more than one in both left and right side that is left and right hash array. That time increase c it will keep track how many character will remove from string so that will remove from both left and right so remove.
- Then now the current will be added to the left side of the array so add.
- Finally the lenght of the whole string and the character count * 2 that will be remove from the string is return.
### 2661. First Completely Painted Row or Column
[Leetcodelink](https://leetcode.com/problems/first-completely-painted-row-or-column/description/?envType=daily-question&envId=2025-01-20)
<br>
You are given a 0-indexed integer array arr, and an m x n integer matrix mat. arr and mat both contain all the integers in the range [1, m * n].

Go through each index i in arr starting from index 0 and paint the cell in mat containing the integer arr[i].

Return the smallest index i at which either a row or a column will be completely painted in mat.

 

Example 1:
![](https://assets.leetcode.com/uploads/2023/01/18/grid1.jpg)
Input: arr = [1,3,4,2], mat = [[1,4],[2,3]]
Output: 2
Explanation: The moves are shown in order, and both the first row and second column of the matrix become fully painted at arr[2].
Example 2:
![](https://assets.leetcode.com/uploads/2023/01/18/grid2.jpg)
Input: arr = [2,8,7,4,1,3,5,6,9], mat = [[3,2,5],[1,4,6],[8,7,9]]
Output: 3
Explanation: The second column becomes fully painted at arr[3].
 

Constraints:

m == mat.length
n = mat[i].length
arr.length == m * n
1 <= m, n <= 105
1 <= m * n <= 105
1 <= arr[i], mat[r][c] <= m * n
All the integers of arr are unique.
All the integers of mat are unique.

```java
class Solution {
    public int firstCompleteIndex(int[] arr, int[][] mat) {
        HashMap<Integer,int[]> map = new HashMap<>();
        int[] row = new int[mat.length];
        int[] col = new int[mat[0].length];
        for(int i=0;i<mat.length;i++)
        {
            for(int j=0;j<mat[0].length;j++)
            {
                map.put(mat[i][j],new int[]{i,j});
            }
        }
        for(int i=0;i<arr.length;i++)
        {
            int[] ans = map.get(arr[i]);
            row[ans[0]]++;
            col[ans[1]]++;
            if(row[ans[0]]>=mat[0].length || col[ans[1]]>=mat.length) return i;
        }
        return 0;
    }
}
```
- First track if the row or coloum is fill by using the frequency array for row and column.
- Then for know the position first pre compute the position using hash map.
- then for the each array element take the corrosponding row and column then increase that row and column count then check if the row >= column size beacause it will oppositely increase or check for column then return the curren index i.
### 2364. Count Number of Bad Pairs
[Leetcode link](https://leetcode.com/problems/count-number-of-bad-pairs/description/?envType=daily-question&envId=2025-02-09)
<br>
You are given a 0-indexed integer array nums. A pair of indices (i, j) is a bad pair if i < j and j - i != nums[j] - nums[i].

Return the total number of bad pairs in nums.

 

Example 1:

Input: nums = [4,1,3,3]
Output: 5
Explanation: The pair (0, 1) is a bad pair since 1 - 0 != 1 - 4.
The pair (0, 2) is a bad pair since 2 - 0 != 3 - 4, 2 != -1.
The pair (0, 3) is a bad pair since 3 - 0 != 3 - 4, 3 != -1.
The pair (1, 2) is a bad pair since 2 - 1 != 3 - 1, 1 != 2.
The pair (2, 3) is a bad pair since 3 - 2 != 3 - 3, 1 != 0.
There are a total of 5 bad pairs, so we return 5.
Example 2:

Input: nums = [1,2,3,4,5]
Output: 0
Explanation: There are no bad pairs.
 

Constraints:

1 <= nums.length <= 105
1 <= nums[i] <= 109

```java
class Solution {
    public long countBadPairs(int[] nums) {arra
        HashMap<Integer,Integer> map = new HashMap<>();
        long good_pair = 0;
        for(int i=0;i<nums.length;i++)
        {
            if(map.containsKey(nums[i]-i)) good_pair += map.get(nums[i]-i);
            map.put(nums[i]-i,map.getOrDefault(nums[i]-i,0)+1);
        }
        System.out.print(good_pair);
        long n = nums.length;
        return (n*(n-1)/2)-(good_pair);
    }
}
```
- In this code we find i<j so nums[j] - nums[i] != j-i;
- So find this we find the good pairs and minus from the bad pairs.
- For this we rearrange the euation  nums[i]-i != nums[j]-j
- so take the hashmap to keep track the number then add to the good pair when the map already contain the key.
### 2342. Max Sum of a Pair With Equal Sum of Digits
[Leetcode link](https://leetcode.com/problems/max-sum-of-a-pair-with-equal-sum-of-digits/?envType=daily-question&envId=2025-02-12)
<br>
You are given a 0-indexed array nums consisting of positive integers. You can choose two indices i and j, such that i != j, and the sum of digits of the number nums[i] is equal to that of nums[j].

Return the maximum value of nums[i] + nums[j] that you can obtain over all possible indices i and j that satisfy the conditions.

 

Example 1:

Input: nums = [18,43,36,13,7]
Output: 54
Explanation: The pairs (i, j) that satisfy the conditions are:
- (0, 2), both numbers have a sum of digits equal to 9, and their sum is 18 + 36 = 54.
- (1, 4), both numbers have a sum of digits equal to 7, and their sum is 43 + 7 = 50.
So the maximum sum that we can obtain is 54.
Example 2:

Input: nums = [10,12,19,14]
Output: -1
Explanation: There are no two numbers that satisfy the conditions, so we return -1.
 

Constraints:

1 <= nums.length <= 105
1 <= nums[i] <= 109

```java
class Solution {
    public int find(int n)
    {
        int c = 0;
        while(n>0)
        {
            c += n%10;
            n/=10;
        }
        return c;
    }
    public int maximumSum(int[] nums) {
        int max = -1;
        int[] arr = new int[82];
        Arrays.fill(arr,-1);
        for(int i=0;i<nums.length;i++)
        {
            int digit_sum = find(nums[i]);
            if(arr[digit_sum]!=-1)
            {
                max = Math.max(max,nums[i]+arr[digit_sum]);
            }
            arr[digit_sum] = Math.max(arr[digit_sum],nums[i]);
        }
        return max;
    }
}
```
- In this code we find the pair which have both sum of digits equal but we get maximum of them.
- So create table which have size of 82 because (10 power 9 integer constraint) so every update the value by maximum digit if it is not equal to -1 means it have already one elements so update the final answer.
### 781. Rabbits in Forest
[Leetcode link](https://leetcode.com/problems/rabbits-in-forest/description/?envType=daily-question&envId=2025-04-20)
<br>
There is a forest with an unknown number of rabbits. We asked n rabbits "How many rabbits have the same color as you?" and collected the answers in an integer array answers where answers[i] is the answer of the ith rabbit.

Given the array answers, return the minimum number of rabbits that could be in the forest.

 

Example 1:

Input: answers = [1,1,2]
Output: 5
Explanation:
The two rabbits that answered "1" could both be the same color, say red.
The rabbit that answered "2" can't be red or the answers would be inconsistent.
Say the rabbit that answered "2" was blue.
Then there should be 2 other blue rabbits in the forest that didn't answer into the array.
The smallest possible number of rabbits in the forest is therefore 5: 3 that answered plus 2 that didn't.
Example 2:

Input: answers = [10,10,10]
Output: 11
 

Constraints:

1 <= answers.length <= 1000
0 <= answers[i] < 1000

```java
class Solution {
    public int numRabbits(int[] answers) {
        HashMap<Integer,Integer> map = new HashMap<>();
        int sum = 0;
        for(int i=0;i<answers.length;i++)
        { 
            if(answers[i] == 0) sum++;
            else
            {
                map.put(answers[i],map.getOrDefault(answers[i],0)+1);
                if(map.get(answers[i])==(answers[i]+1)) 
                {
                    sum += (answers[i]+1);
                    map.remove(answers[i]);
                }
            }
        }
        List<Integer> li = new ArrayList<>(map.keySet());
        for(int x:li) 
        {
            sum += (x+1);
        }
        return sum;
    }
}
```
> [Refrence](https://www.youtube.com/watch?v=Do2coBlSIFo)
### 3335. Total Characters in String After Transformations I
[Leetcode link](https://leetcode.com/problems/total-characters-in-string-after-transformations-i/description/?envType=daily-question&envId=2025-05-13)
<br>
You are given a string s and an integer t, representing the number of transformations to perform. In one transformation, every character in s is replaced according to the following rules:

If the character is 'z', replace it with the string "ab".
Otherwise, replace it with the next character in the alphabet. For example, 'a' is replaced with 'b', 'b' is replaced with 'c', and so on.
Return the length of the resulting string after exactly t transformations.

Since the answer may be very large, return it modulo 109 + 7.

 

Example 1:

Input: s = "abcyy", t = 2

Output: 7

Explanation:

First Transformation (t = 1):
'a' becomes 'b'
'b' becomes 'c'
'c' becomes 'd'
'y' becomes 'z'
'y' becomes 'z'
String after the first transformation: "bcdzz"
Second Transformation (t = 2):
'b' becomes 'c'
'c' becomes 'd'
'd' becomes 'e'
'z' becomes "ab"
'z' becomes "ab"
String after the second transformation: "cdeabab"
Final Length of the string: The string is "cdeabab", which has 7 characters.
Example 2:

Input: s = "azbk", t = 1

Output: 5

Explanation:

First Transformation (t = 1):
'a' becomes 'b'
'z' becomes "ab"
'b' becomes 'c'
'k' becomes 'l'
String after the first transformation: "babcl"
Final Length of the string: The string is "babcl", which has 5 characters.
 

Constraints:

1 <= s.length <= 105
s consists only of lowercase English letters.
1 <= t <= 105

```java
class Solution {
    public int lengthAfterTransformations(String s, int t) {
        int[] arr = new int[26];
        int ans = 0;
        int mod = 1000000007;
        for(int i=0;i<s.length();i++) arr[s.charAt(i)-'a']++;
        while(t>0)
        {
            int[] next = new int[26];
            for(int i=1;i<26;i++)
            {
                next[i] = arr[i-1];
            }
            next[0] = arr[25]; 
            next[1] = (next[1]+arr[25])%mod;
            for(int i=0;i<26;i++) arr[i] = (next[i])%mod;
            t--;
        }
        for(int i=0;i<26;i++) 
        {
            ans = (ans+arr[i])%mod;
            System.out.print(arr[i]+" ");
        }
        return ans;
    }
}
```
> [Reference](https://www.youtube.com/watch?v=9kShMzSCmLA)
