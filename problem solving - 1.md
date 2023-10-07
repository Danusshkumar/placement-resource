> Problem Solving - 1

## Common patterns on Problem solving

## Information gained from solved problems

  There may be some tricky questions in the view of binary search but there won't be any new logic applied. Let's
  consider [this problem](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/).
  It's a problem to find minimum element in the rotated sorted array in O(logN) time complexity.
  They are forcing us to use Binary Search. It'a normal way of using binary search in the sorted array and nothing will differ.
  View the solution and explanation for it in [here](https://github.com/Danusshkumar/LeetCode-problems/blob/main/minimumElementInO(logn).java).

  See the difference between these problems ==> [problem](https://practice.geeksforgeeks.org/problems/maximum-index-1587115620/1) and [problem](https://leetcode.com/problems/maximum-difference-between-increasing-elements/description/)
   They are different because in first problem we have to find the maximum index whereas in second problem we have to find the maximum difference.
  value difference matters in second problem whereas index difference matters in first problem. That's why first problem is complicated involving lMin and
  rMax. 
  But second problem's logic is very simple. We have to find the maximum difference between element maintaining i < j where i and j are the position of minimum element and maximum element respectively. That's why we are updating the minimum element as it while iterating through the element and also updating the difference between those two elements if arr[i] > min
  
### Dutch national flag problem

In the below code, the mid is not incremented when arr[mid] == 2 becomes true but mid get
incremented when arr[mid] == 0. Because, the element before mid are processed meaning that there 0 only exists. But after mid, there may be 0, 1 or 2 also exists. Consider the case where 2 swapped with 2 or 2 swapped with 0. Now, the 0 will remains in the mid part without being swapped into first part. That's why on swapping, with last part(`high` controlled part), the mid value not get incremented

```
class Solution
{
    public static void swap(int[] arr, int a, int b){
        int temp = arr[a];
        arr[a] = arr[b];
        arr[b] = temp;
    }
    
    public static void segragate012(int arr[], int n){
        int low = 0, high = n - 1, mid = 0;
        while(mid <= high){
            if(arr[mid] == 0){
                swap(arr,low,mid);
                low++;
                mid++;
            }
            else if(arr[mid] == 2){
                swap(arr,mid,high);
                high--;
            }
            else if(arr[mid] == 1){
                mid++;
            }
        }
    }
}
```

### Duplicates on Arrays

- Commonly when we have to check duplicates on array with O(n) time complexity, there is one approach that comes to my mind. Using HashSet. By using this, I will solve most of my problems as it has time complexity of O(n) for searching an element
- Previously we used another array for storing frequency based on index or we may use arrays for finding the duplicates
- Now, it's easy to implement HashSet then doing those kinds of things as HashSet did all the work for us. This is the way to enjoy the features of Powerful programming languages
 like Java.
- But if we wanted to check duplicates withou using extra space, then it's challenging. But we may do that if we have certain constraints. 
- If the array size is n+1 and each element in array will be in the range[1,n], then we can find duplicate elements using pointer-pointed element approach. 
- This is not a name of the approach but it's the name given by me for that approach. pointer (current element) will point to pointed element. If the current element points one element (pointed) and its already visited, then the pointer element(current element) is duplicated. We may mark the pointed element as visited using several techniques based on the constrains such as marking as -ve and adding n to the number etc.
- Explore all duplicates related problems to learn and feel this

## Questions on problem solving

### Greedy approach: questions and answers

Qn: is getting the value for current index from doing some computation for the value of previous index is considered to be greedy in programming ?

Ans: 
Yes, obtaining the value for the current index by performing some computation based on the value of the previous index is a characteristic often associated with a greedy algorithm in programming.

In a greedy algorithm, you make a series of choices at each step, and the choice you make at each step is the one that seems best at that moment without considering the consequences of that choice on future steps. In the context you mentioned, the "best" choice for the current index is determined based on the value computed for the previous index.

For example, in a situation where you are trying to maximize or minimize some value, and the decision for the current step depends only on the value at the previous step (as opposed to considering all previous steps), this can be seen as a form of greedy strategy.

Greedy algorithms are often used in optimization problems and can be efficient and easy to implement, but they may not always produce the optimal solution in every case. It's important to analyze the problem and ensure that a greedy approach will indeed yield a correct or acceptable solution.

Qn: If this is the case, then finding maximum element in the array is also considered as greedy, right

Ans: Yes, finding the maximum element in an array can be considered a simple form of a greedy approach. In this case, you're making a series of choices where at each step, you're choosing the maximum value seen so far. This approach doesn't involve considering the overall future consequences of each choice; instead, it focuses on making a locally optimal choice (choosing the maximum value at each step).

A simple algorithm to find the maximum element in an array is a form of a greedy approach because you're iteratively selecting the largest element seen up to the current point in the array without considering the entire array at once.

However, it's important to note that not every algorithm that involves finding the maximum element is a greedy algorithm. Greedy algorithms usually involve making a series of choices in a way that at each step, you make the locally optimal choice without revisiting that decision later. The key characteristic is that the choice at each step is based only on the current situation, not on the entire problem or the optimal solution for the entire problem.

Qn: Why this approach is given the name greedy

Ans: The term "greedy" in the context of algorithm design refers to the algorithmic strategy of making the best possible choice at each step, without worrying about the global situation or long-term consequences. Essentially, a greedy algorithm makes a series of choices by always selecting the locally optimal solution at each step in the hopes of finding the overall optimal solution for the entire problem.

The term "greedy" is used because, at each step, the algorithm is being "greedy" or "selfish" by choosing what appears to be the best option right then, without considering the potential future implications or the overall global optimal solution.

It's important to note that while greedy algorithms are often easy to design and computationally efficient, they don't always guarantee the globally optimal solution for every problem. There are cases where a greedy approach may lead to a suboptimal or incorrect result, and it's essential to analyze the problem and determine if a greedy strategy is appropriate and if it indeed produces the desired solution.
