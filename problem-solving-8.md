> Problem Solving - 8

# Strings

## Introduction to Strings

C uses ASCII code for binary to character conversion but Java uses UTF-16 format for binary to character conversion. UTF-16 stores character in 2 bytes and it has a rich character set but the first 128 character set of UTF-16 is same as the ASCII code. So the implementation for string function doesn't vary for Java and C++.

The main advantage of existing `String` data type is that it has a special set of properties such as having limited range (0-128) or (0-255). There are many other kinds of properties that makes String unique.

In the below program, we can sort the string and can get the frequencies of each string without having to use any sorting algorithm to sort and didn't have to use any HashMap like data structure to store the frequencies of each string. 

Get to know about String in C++ [here](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-Strings/video/MTQzNTU%3D)


```
public static void main(String[] args){
    String str="geeksforgeeks";
    int[] count=new int[26];
    for(int i=0;i<str.length();i++){
        count[str.charAt(i)-'a']++;
    }
    for(int i=0;i<26;i++){
        if(count[i]>0){
            System.out.println((char)(i+'a')+" "+count[i]);
        }
    }
}
```

## Strings in Java

There are commonly three ways to create Strings in java

1. character array of character arraylist
2. `String` Class
3. `StringBuffer` and `StringBuilder` class


```
char[] arr = {'t','c','n'}; // character array
ArrayList<Character> ls = new ArrayList<>(); //creating arraylist and adding characters

String str = "tcn"; //using String class
String str = new String("tcn");

StringBuffer strBfr = new StringBuffer("tcn"); //creating string buffer class
StringBuilder strBdr = new StringBuilder("tcn"); //creating string builder class
```

- The advantage of using String class over character array of character ArrayList is that the String class has many built-in functions for manipulating strings. 
- Searching first occurrence or last occurrence of a substring in a given string can be done using built-in function that are available in String class
- But why StringBuffer and StringBuilder class ? These two classes are mutable whereas String class is not mutable, when we concatenate of doing any other operation in String class, it only returns new object of modified string.
- If we want to modify the original string, we can go with StringBuffer and StringBuilder. The main difference between these two are StringBuilder is not threadsafe whereas StringBuffer is thread safe. We can avoid using StringBuffer if we are writing only single threaded program. We can avoid the overhead of having multiple threads.
- `str.length()` - will return the length of the string
- `str.charAt(i)` - will return the character at the position (or) index i. Note that the strings are immutable so that assigning character to `str.charAt(i)` is not possible
- `str.substring(2)` or `str.substring(2,5)` - will return the string from first index to the end of the string. If the second index is mentioned, then this method will return the substring from [startIndex,endIndex) which means the endIndex is excluded.
- As strings in Java are immutable, if the content of the string are same, then those strings refers to the same memory location and new String can't be created.
- But if we create string with `String str = new String("tcn")`, then new object will be created.

```
String s1 = "tcn";
String s2 = "tcn";
if(s1 == s2) //will return true
    print(true); 
String s3 = new String("tcn");
if(s1 == s3) //will return false
    print(true);
```
- `str.contains(s2)` - returns true if the s2 is present in s1
- `str.equals(s2)` - returns true if s2 and s1 are same (equal)
- `str.compareTo(s2)` - compares the s1 and s2 lexicographically
- `str.indexOf(s2)` - return the first occurrence (index) of s2 in str. If not present then it returns -1. It also takes the second argument as index where we want to start searching for s2.

```
String s1 = "tcn";
String s2 = "the complex number";
int res = s1.compareTo(s2);
if(res == 0)
    print("equal");
else if(res < 0)
    print("s1 smaller");
else if(res > 0)
    print("s1 greater");

//output : s1 smaller
```
- One interesting fact about Strings in Java is that if we do concatenation, then the new object is returned. If we store this new object to the existing reference, then the old reference is overridden, meaning that we can able to do concatenation. There is nothing interesting in creating new object while doing modification to the string such as concatenation. But it's inreresting as it overrides the existing reference.

```
String s1 = "the";
String s2 = s1;
s1 = s1 + " complex number";
print(s1); // the complex number
if(s1 == s2); // return false as s1 is replaced with new object that returned from concatenation
```

## Problems on String

## Palindrome check

In naive method, we are having copy of the string and reverse it. If these two are same, then return true else false.
Time complexity : θ(n) and space complexity : θ(n)

```
boolean isPal(String str){
    StringBuilder rev = new StringBuilder(str);
    rev.reverse();
    return str.equals(rev.toString());
}
```

The first and last characters are compared and moved towards each other if those characters are same. Loops runs until mismatch found or until they are equal or crosses each other. It's TC is θ(1) in best case and θ(n) in worst case. So the overall TC is O(n). Space complexity is θ(1).

```
public static boolean isPalindrome(String str) {
    int left = 0, right = str.length() - 1;
    while (left < right) {
        if (str.charAt(left) != str.charAt(right))
            return false;
        left++;
        right--;
    }
    return true;
}
```

## Subsequence of a string

The number of subsequence a string can have is equal to 2<sup>n</sup> where n is the length of the string. Note that the subsequence is not same as substring. Subsequence is as like as the subset of a set but with the same order as it in the original string. Have a look at [this](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-Strings/video/MjMyNw%3D%3D) video for better understanding.

Time complexity : O(n+m) and Space complexity : O(1)

```
class Solution{
    boolean isSubSequence(String s1, String s2){
        
        int m = s1.length(); //substring
        int n = s2.length(); //original string
        
        int i = 0;
        for(int j = 0;j<n;j++){
            if(s2.charAt(j) == s1.charAt(i)){
                i++;
                if(i == m)
                    return true;
            }
        }
        
        return false;
    }
}
```

#### Recursive approach

```
static boolean isSubSeq(String s1, String s2, int n, int m){
    if( m == 0 )
        return true;
    
    if( n == 0 )
        return false;
        
    if ( s1.charAt(n-1) == s2.charAt(m-1) )
        return isSubSeq(s1, s2, n-1, m-1);
    
    else
        return isSubSeq(s1, s2, n-1, m);
}
```


## Anagrams

```
class Solution
{    
    public static boolean isAnagram(String a,String b)
    {
        int[] count1 = new int[26];
        int[] count2 = new int[26];
        int m = a.length(), n = b.length();
        
        for(int i = 0;i<m;i++)
            count1[a.charAt(i) - 'a']++;
        
        for(int i = 0;i<n;i++)
            count2[b.charAt(i) - 'a']++;
            
        for(int i = 0;i<26;i++)
            if(count1[i] != count2[i])
                return false;
        
        return true;
    }
}
```

The auxiliary space here is two count arrays of length 26. Here the length 26 is fixed. So it comes under O(1) auxiliary space even though we use auxiliary array. because the size of this auxiliary array doesn't depends on the size of input string. The solution is based on the special properties of string and its ASCII value properties. The solution is based in [this](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-Strings/video/MTYxNQ%3D%3D) video


## Repeated character

[Problem statement link](https://practice.geeksforgeeks.org/problems/repeated-character2058/1)

[Explanation link](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-Strings/video/MTYxMg%3D%3D)

```
class Solution
{
    char firstRep(String s)
    {
        int[] count = new int[26];
        
        for(int i = 0;i<s.length();i++){
            count[s.charAt(i) - 'a']++;
        }
        
        for(int i = 0;i<s.length();i++)
            if(count[s.charAt(i) - 'a'] > 1)
                return s.charAt(i);
        
        return '#';
    }
}
```

## Left most non-repeated character

[Problem statement link](https://practice.geeksforgeeks.org/problems/non-repeating-character-1587115620/1)

[Explanation link](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-Strings/video/MTYxMQ%3D%3D)

```
//function to find the first non-repeating character in a string
static char nonrepeatingCharacter(String s) {

    int[] count = new int[26];
    
    for(int i = 0;i<s.length();i++)
        count[s.charAt(i) - 'a']++;
    
    for(int i = 0;i<s.length();i++)
        if(count[s.charAt(i) - 'a'] == 1)
            return s.charAt(i);
            
    return '$';
}
```

There are some additional methods that are discussed in those videos of [Leftmost repeating character](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-Strings/video/MTYxMg%3D%3D) and [leftmost non-repeating character](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-Strings/video/MTYxMQ%3D%3D). Check the problem statement submission links and its submission history to know about those efficient methods of solving problems. 

## Reverse words in string
Video reference [here](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-Strings/video/MTYwOA%3D%3D)<br>
Problem solved on LeetCode reference [here](https://leetcode.com/problems/reverse-words-in-a-string/)


## Overview of Pattern searching

![Overview of pattern searching](https://danusshkumar.github.io/reference-images-for-problem-solving/overview-of-pattern-searching.jpg "Overview of pattern searching")

### Naive approach

The pattern is considered as the window and all the elements on the patterns are window element. This window will slide across the character array and checks if the all character in the windows matches with the array. Consider **n** as the length of larger string and **m** as the length of pattern. Hence the Time complexity will be O((n-m+1)*m)).

### Improved Naive approach for distinct characters

This improved naive approach will work if the characters in the pattern are distinct.

```
static void patSearching(String txt,String pat){
    int m=pat.length();
    int n=txt.length();
    for(int i=0;i<=(n-m);  ){
        int j;
        for(j=0;j<m;j++)
            if(pat.charAt(j)!=txt.charAt(i+j))
                break;
        
        if(j==m)
            System.out.print(i+" ");
        
        // this if-else condition is where this algorithm deviates from naive approach
        if(j==0)
            i++;
        else
            i=(i+j);
    }
}
```

In this improved algorithm, it uses the fact that all the characters in the pattern is distinct. If it is so, then there is no use in shifting each character by one. 

```
A B C E A B C D 
 / / / /
A B C D // won't occur, instead

A B C E A B C D
      | | | | 
      A B C D
```
By comparing A B C on the first iteration and came to know that D and E are not equal, we may shift our pattern to the position E as ABC shifted to left can't match with ABC in the text as they are same. So we can safely ignore those iteration. In this way, we may make our traversal as O(n). This algorithm claims that it takes O(n) times, because If inner loop run 4 times, 4 outer loop is saved (or) skipped to run and continues from 5th iteration. In this way, the time complexity will become O(n).<br>
By this optimised approach, we can make the traversal O(n).


## Rabin Karp Algorithm for pattern searching 

Refer video [here](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-Strings/video/MTM5NQ%3D%3D)

```
void RBSearch(String pat, String txt, int m, int n){
    // q value is somewhat set to larger inorder to avoid spurious hit
    int h = 1;
    for(int i = 1;i<=m-1;i++)
        h = (h*d)%q;
    // calculating d^(m-1) % q
    
    //computing hash value for first text window slide and pattern
    int p = 0, t = 0;
    for(int i = 0;i<m;i++){
        p = (p*d + pat[i])%q;
        t = (t*d + txt[i])%q;
    }
    
    for(int i = 0;i<=n-m;i++){
        if(p == t){
            boolean flag = true;
            for(int j = 0;j<m;j++)
                if(txt[i+j] != pat[j]){
                    flag = false;
                    break;
                }
            if(flag == true)
                print(i); // result
        }
        if(i < n-m){
            //moving to the next hash
            p = (d*(p - txt[i]*h) + txt[i+m])%q;
            if(t < 0) t = t + q; // making t into positive if it'll become negative
        }
    }
}
```








