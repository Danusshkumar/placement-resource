> Problem Solving - 3

# Deep Dive into Sorting

## Overview

### Special case sorting algorithms

1. Binary array sorting ( lomato, hoare, naive )
2. Sorting arrays with three types of values (0s,1s ans 2s, etc)
3. Arrays of size n but the range is small (ex: [100,200] only) - **Counting sort**

Auxiliary space - O(k)
Time complexity - O(n+k) where k is the maximum range

4. Arrays of size n and range is of size n<sup>2</sup> or n<sup>3</sup> or closer - **Radix sort**

5. Array of uniformly distributed data over a range - **Bucket sort**
6. When memory writes are costly, then we go to - **Selection sort & Cycle sort**
7. When only adjacent swaps are allowed - **Bubble sort**.

There is one optmised version of Bubble sort exists and it is called **Cocktail sort**

8. When the array size is too small, we can go with **Selection sort or Insertion sort**.

Here Insertion sort works best. On some standard libraries on some languages, they do switch to Insertion sort when the number of element in the array are smaller. Note that based on the size of array, the sorting algorithm implementation differs when we use pre-defined functions.

9. Many standard algorithms like Quick sort or Merge sort needs extra space, but when you are programming in a space contrained place like kernel, or hardware programming, we won't use those standard algorithms. For this purpose, there is an algorithm called **Shell sort**. Time complexity of this shell sort is O(nlog<sup>2</sup>n) or O(n*(logn)<sup>2</sup>)

### General pupose sorting algorithm - implemented in libraries

* Merge sort - O(nlogn)
* Heap sort - O(nlogn)
* Quick sort - O(n<sup>2</sup>) but O(nlogn) on average

Quick sort is faster of all but Merge sort is stable of all. Merge sort is well suitable for linked list and it doesn't require random access. But Heap sort requires random access. Quick sort requires random access, but it can be modified so that without random access, it can work in same O(nlogn) time complexity.

Both Quick sort and Merge sort works in the principle or Divide and Conquer


### Hybrid sorting algorithms

Most of the library functions use hybrid sorting algorithms

TimSort in python: It's a mix of insertion sort and merge sort. When the input array size is small or when it becomes smaller in recursive calls, it uses insertion sort, else it uses mergeSort

IntroSort in C++: mix of Quick sort, Heap sort and insertion sort - when the space complexity is beyond nlogn (unfair partioning) it swtiches to heap sort from quick sort. When the array size is small or smaller in recursive calls, it uses insertion sort.


## Sort in C++ STL

sort function will only work for containers with random access. Ex: array, vector and deque. It internally uses introsort

```
#include <algorithm> // sort function is present inside algorithm library
sort(arr, arr+n); // sort(startingAddress, addressAfterLastElement);
sort(arr, arr+n, greater<int>); // sort(startingAddress,addressAfterLastElement,comparatorFunction);
```

greater<int> will compare the elements in reverse manner and as a result, we will get the array as decreasingly sorted

**Sorting vectors:**
```
#include <vector>
#include <algorithm>
vector<int> v = {5,7,20,10};
sort(v.begin(),v.end());
sort(v.begin(),v.end(),greater<int>);
```

We can also write our own comparator

```
#include <iostream> 
#include <algorithm> 
Using namespace std;
Struct Point {
int x, y;
};
bool myCmp(Point p1, Point p2){
    // compares with respect to y value in reverse order
    return (p1.y >= p2.y);
}
int main(){
    Point arr[] = { {3,10},{2,8},{5,4} };
    sort(arr,arr+n,myCmp);
}

```

## Sort in Java

We have Arrays.sort() for arrays class and Collections.sort() for all collections class (list interfaces).

On Arrays class, they are of two types, Arrays of primitive and array of non-primitive.
but when it comes to Collections class, all the elements are non-primitive

### Stability in sorting arrays with objects

Array of objects : { {CS,101}, {ECE, 102}, {CS, 104}, {CS, 105}, {ECE, 107} }

If our algorithm is not stable, we will cluster CS, ECE students (sorting with branches) but we won't get the roll numbers in correct order. If our algorithm is stable, we can also get roll nos in correct order apart from branch wise clustering. 

So for the above reason, Java uses two different sorting for arrays when it is primitive or non-primitive. 

On primitive, it uses **Dual Pivot QuickSort** which doesn't guarantee stability but will work fast, and for non-primitive, it uses algorithm that is based on **MergeSort and adaption of TimSort (used in python)**


### Arrays.sort() in Java










