> Problem Solving - 3

# Deep Dive into Sorting - 1

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

Array of objects : {CS,101}, {ECE, 102}, {CS, 104}, {CS, 105}, {ECE, 107} }

If our algorithm is not stable, we will cluster CS, ECE students (sorting with branches) but we won't get the roll numbers in correct order. If our algorithm is stable, we can also get roll nos in correct order apart from branch wise clustering. 

So for the above reason, Java uses two different sorting for arrays when it is primitive or non-primitive. 

On primitive, it uses **Dual Pivot QuickSort** which doesn't guarantee stability but will work fast, and for non-primitive, it uses algorithm that is based on **MergeSort and adaption of TimSort (used in python)**


### Arrays.sort() in Java

`Arrays.sort()` doesn't receive the comparator for the array so that we are only able to sort the primitive data types. Inorder to sort non-primitive data types, `Collections.sort()` is suggested as they receive the custom comparator. `Arrays.sort()` has one more version also. It receives the starting and ending index as parameter and only sorts the array inside that range. Note that start index is included and end index is excluded as it has in all programming languages `[start,end)`.
If we want to sort the non-primitive data types with Arrays.sort(), then we may implement Comparable class in non-primitive data types and define the compareTo() method as I given below.

```
class Point implements Comparable<Point> {
    int x, y;
    Point(int x,int y){
        this.x = x;
        this.y = y;
    }
    public int compareTo(Point p){
        return this.x - p.x;
    }
}

//on main function just do
Arrays.sort(arr); // where arr is the array of Point
```
If we don't want to make our object Comparable, then we can use Comparator class to do this as given below:

```
class Point {
    int x, y;
    Point(int x, int y){
        this.x = x;
        this.y = y;
    }
}

class MyCmp implements Comparator<Point>{
    public int compare(Point p1, Point p2){
        return p1.x - p2.x;
    }
}

// on main function
Arrays.sort(arr,new MyCmp());
```

There is a difference between custom compare function in Collection and Comparable object in Arrays. In Collections, we will create our own boolean function and assign it as compare function. but in Arrays, we must have our data type implements Comparable interface to pass an Comparator objec which implements Comparator class.

```
Integer[] arr = {1,4,5,6,7};
Arrays.sort(arr,Collections.reverseOrder());
```
We may use Collections.reverseOrder()) for non-primitive types inorder to do reversal sorting without reversing the array.


The main thing about compare function is that, if the function returns the positive value, then the element will be swapped, else not. 
If p1.x - p2.x will return true only when p1 is greater than p2. We have to keep in mind that p1 occurs before p2 in the array. That's why if the positive value is returned, then we have to swap the elements. 

If we want to have the even elements front and odd elements back, then we will do
```
class MyCmp implements Comparator<Integer>{
    public int compare(Integer a, Integer b){
        return a%2 - b%2; // if we want odd number on first, then b%2 - a%2
    }
}
```


### Why Collections takes only non-primitive objects as their data-types ?

The Collections are specially made for manipulate with non-primitives, so they compare their data with compareTo function which is a function that is defined in Comparable interface. That means, every custom objects that we add into our Collections must implement the Comparable interface inorder to results on sorting. If we neither have non-primitive data types that implements Comparable interface nor we have custom Comparator object, then we will get **ClassCastException** at run time. So Collections are designed to use the compareTo function in Comparable class or to use compare function in Comparator class. They didn't have any natural comparison techniques as Arrays do with primitve data types. Due to this design of collection, they can't be able to intake the primary data types, instead they have Wrapper classes for primitive data-types (an alternative non-primitive form of primitive data types). Ex: Integer, Character, etc. These classes implements Comparable interface by default and has compareTo function too. This is the reason why Collections sort Integers. 

### Question and Answer about Stability :

#### Question:
What the term "stability in sorting algorithm" represents ? What happens if the algorithm is not stable ? Is there any chance that the array won't be sorted if the algorithm is not stable ? Quick sort is not stable then merge sort ? Is this means that Quick sort gives wrong results in sorting ??


#### Answer:

The term "stability in sorting algorithm" represents how the algorithm treats equal elements in the input array. A sorting algorithm is stable if it preserves the relative order of equal elements in the sorted output. For example, if we have an array of names and ages, and we sort it by age, a stable algorithm will keep the original order of names with the same age.

If the algorithm is not stable, it may change the relative order of equal elements in the sorted output. For example, if we have an array of names and ages, and we sort it by age, an unstable algorithm may swap the names with the same age. This may not matter if we only care about the order of ages, but it may matter if we also care about the order of names.

There is no chance that the array won't be sorted if the algorithm is not stable. An unstable algorithm can still sort the array correctly according to the given criteria. For example, quick sort is an unstable algorithm, but it can sort an array of integers in ascending order correctly. However, it may not preserve the relative order of equal integers in the sorted output.

Quick sort is not stable, while merge sort is stable. This does not mean that quick sort gives wrong results in sorting. It only means that quick sort does not guarantee to preserve the relative order of equal elements in the sorted output, while merge sort does. For example, if we have an array of points with x and y coordinates, and we sort it by x coordinate, quick sort may swap the points with the same x coordinate, while merge sort will keep them in the same order as they appear in the input array.

Stability is important when we want to sort an array by multiple criteria. For example, if we want to sort an array of students by name and then by grade, we can first use a stable algorithm to sort by name, and then use another stable algorithm to sort by grade. This way, we can ensure that the students with the same grade are still sorted by name in the final output. If we use an unstable algorithm for either step, we may lose the order of names or grades in the final output.


### Stabilities in Sorting Algorithms

Stable sorting Algorithms : Bubble sort, Insertion sort, Merge sort

Unstable sorting Algorithms : Selection sort, Quick sort and Heap sort
