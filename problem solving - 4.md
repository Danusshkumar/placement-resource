> Problem Solving - 4

# Deep Dive into Sorting - 2


## Bubble Sort:

![Bubble sort Visualisation](https://danusshkumar.github.io/reference-images-for-problem-solving/WhatsApp%20Image%202023-09-09%20at%2023.26.51.jpg "Bubble sort Visualisation")


- In every pass of the bubble sort, the largest element get **bubbled up** to the corresponding last position. It compares only adjacent elements (current element and next element).
- Bubble sort is the stable sorting algorithm because it maintains the order of the element that has equal values. 
- The time complexity will be (n - 1) * (n - 1) and thus the Time Complexity will be O(n<sup>2</sup>)
- Implementation of this algorithm is given below

```
for(int i= 0;i<n - 1;i++){
    for(int j = 0;j<n-1;j++){
        if(arr[j] > arr[j+1]
            swap(arr[j],arr[j+1]);
    }
}
```

- We can optimise the algorithm further. On the first swap, the largest element get moved to last place. So there is no sense in comparing it again with n - 2 th element. So our optimisation is to do not consider swapping for the elements that are sorted to correct position in previous passes. Note that I refer outer for loop as passes.
- So the Optimised code will be as follows.

```
for(int i= 0;i<n - 1;i++){
    for(int j = 0;j<n-i-1;j++){
        if(arr[j] > arr[j+1]
            swap(arr[j],arr[j+1]);
    }
}
```

- If the array is sorted, then there is no sense in taking O(N<sup>2</sup>) time complexity. That's why we are appointing on listener called `swapped`. It's a variable that listens when there swapping occured in current pass or not. If there is no swapping occured, then the array is swapped in current pass and we should get out of further passes. If the array is sorted, then, our swapped variable will report that no swapping occured meaning that the array is sorted. Now, we break our loop so no further passes occurs. In this way, we can make our Time Complexity to O(N) in these kinds of sorted or partially sorted or almost sorted arrays. 
- Below is the implementation for the optimised approach:

```
for(int i= 0;i<n - 1;i++){
    swapped = false;
    for(int j = 0;j<n-i-1;j++){
        if(arr[j] > arr[j+1]{
            swap(arr[j],arr[j+1]);
            swapped = true;
        }
    }
    if(swapped == false)
        break;
}
```


## Selection sort:

- Selection sort takes θ(n<sup>2</sup>) in all the cases. Note that the time complexity is θ(n<sup>2</sup>) and not O(n<sup>2</sup>) which means that this algorithm always takes N square time complexity regardless of the input whether the array is sorted or not sorted. 
- It does less memory writes when compared with any other popular algorithms like quicksort, mergesort etc. It will be useful when we are working with EEP ROM where memory write is very costly and it would damage the hardware.
- It's the basic idea of Heap sort. that means Heap sort uses the selection sort but in heap data structure

*Heap sort is similar to selection sort, but not exactly the same. Both algorithms divide the input array into a sorted and an unsorted region, and iteratively shrink the unsorted region by extracting the largest or smallest element from it and inserting it into the sorted region. However, the way they extract the largest or smallest element is different. Selection sort uses a simple linear scan to find the largest or smallest element in the unsorted region, which takes O(n) time for each extraction. Heap sort uses a binary heap data structure to maintain the unsorted region, which allows finding and removing the largest or smallest element in O(log n) time for each extraction.*

- This algorithm is not stable as it doesn't maintain the order of element when both element has same values.
- The Selection sort is in-place which means it doesn't require any extra space for sorting.

### WORKING

- There are two different types of Selection sort that differs based on some optimisation techniques. Watch [this](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-Sorting/video/MTQyOQ%3D%3D) video to get a quick understanding of working of selection sort. 
- The smallest element get **selected** and placed in appropriate place (first place) and the process is repeated.
- The main idea is to find the smallest element's index and add it with auxiliary array and make that smallest integer place as INF (infinite). Now find the second smallest element from the array and add it to auxiliary array. Repeat this process until last and copy the elements of auxiliary space to original array.
- As a optimisation, we don't have to use auxiliary array and make the smallest element's place INFINITE. Instead, we can swap the smallest element with first element maintaining the swapped and non-swapped part of the array.

>Note: **The interesting point is till now, we are taught to swap the minimum element with starting element to find the first minimum, second minimum and so on. But in reality, we are only updating the element's position and finally we swap the minimum element's position with first element position. We can reduce the memory write only if we do this. else we will have more memory writes as other algorithms do.**

- The time complexity of the algorithm is explained in the below picture

![Time Complexity](https://danusshkumar.github.io/reference-images-for-problem-solving/image.png "Time Complexity")


## Insertion sort:

- The time complexity will be O(n<sup>2</sup>) in worst case.
- The algorithms works in-place and stable
- Used in practice for small arrays (TimSort and IntroSort)
- The Algorithm takes θ(n<sup>2</sup>) when the array is reversely sorted. This algorithm takes O(n) when the array is sorted.
- The elements are **inserted** into the appropriate position and that's why it is insertion sort. 

### WORKING

![Working of Insertion sort](https://danusshkumar.github.io/reference-images-for-problem-solving/Screenshot%202023-09-10%20005759.jpg "Working of Insertion sort")

![Working of Insertion sort II](https://danusshkumar.github.io/reference-images-for-problem-solving/Screenshot%202023-09-10%20010140.jpg "Working of Insertion sort II")

We have to use `>` in `arr[j] > key` and not `>=` as it is the only thing that makes this insertion sort a stable algorithm

## Merge Sort

### Merge Sort Introduction

- The Merge Sort is based on **divide and conquer rule**. The algorithms splits the array into two parts and recursively sort those two parts and merge them. Note that merging two sorted array is not about concatenation of two arrays. It's about perfect merging.
- Merge sort is a stable sorting algorithm
- Time complexity is θ(nlogn) which is the best possible time complexity for single processor and random inputs. 
- Merge sort in its typical form requires θ(n) auxiliary space and in one of its variant named block merge sort, it works in in-place
- It's well suited to work with LinkedList and it'll take only O(1) aux space in LinkedList. 
- Merge sort is good at external sorting.


#### What is external sorting ??

*External sorting is a term for a class of sorting algorithms that can handle massive amounts of data that do not fit into the main memory of a computing device. External sorting typically uses a hybrid sort-merge strategy, which consists of two phases: sorting and merging. In the sorting phase, chunks of data small enough to fit in the main memory are read, sorted, and written out to temporary files. In the merge phase, the sorted sub-files are combined into a single larger file using a k-way merge algorithm.*

*Merge sort is good at external sorting because it is a stable, divide-and-conquer algorithm that can efficiently sort and merge large files. Merge sort divides the input array into two halves, recursively sorts each half, and then merges them together in sorted order. The merge operation can be done in linear time and space by using a buffer to store one block of each sub-file and selecting the smallest element among them. Merge sort can also be easily adapted to handle different types of data, such as records with multiple fields or variable-length strings.*

*Merge sort has a time complexity of O(n log n) and a space complexity of O(n) for internal sorting, where n is the number of elements in the input array. For external sorting, the time complexity is O(n log k), where k is the number of sub-files, and the space complexity is O(k), where k is the number of blocks that can fit in the main memory. Merge sort is faster than other external sorting algorithms, such as selection sort or insertion sort, which have quadratic time complexities for internal sorting.*


### Merge two sorted arrays

For merging two sorted array, we are creating one array with size m+n and all the elements of array A and array B are copied into this array C. Now we may sort the array C to get the desired output.

![Naive solution](https://danusshkumar.github.io/reference-images-for-problem-solving/merge-sort-naive.jpg "Naive solution")

![Optimised solution](https://danusshkumar.github.io/reference-images-for-problem-solving/merge-sort-optimised.jpg "Optimised solution")

In this method, we maintain two pointer i and j that will move according to which element is greatest, the smallest element get printed and corresponding pointer get incremented until anyone of these pointer reaches end. After that the remaining element on the remaining array will get printed without any comparisons.


### Merge function of Merge sort

![Merge function of Merge sort](https://danusshkumar.github.io/reference-images-for-problem-solving/merge-function-1.jpg "Merge function of merge sort")

- Instead of having two arrays, single array will be given and we have to copy the elements of this single array into two different array as from low to mid and mid+1 to high. 
- low and high need not to be starting and ending of the whole index.
- Now apply the Merge two sorted arrays technique to overwrite the element to the original array on that particular part of the entire array.
- Below is the implementation of the program

![Merge function of Merge sort II](https://danusshkumar.github.io/reference-images-for-problem-solving/merge-function-2.jpg "Merge function of Merge sort II")

- In the above program, `left[i] = a[low+i]` and `right[i] = a[mid+i+1]` is important as low is need not to be 0.
- There the k pointer will be used to track the no.of elements filled (overwrited) in the original array.
- Other logics remains same as merge two sorted arrays

### Merge Sorting Algorithm


```
void mergeSort(int[] arr,int l,int r){
    if(r > l){
        int m = l + (r - l)/2;
        mergeSort(arr,l,m);
        mergeSort(arr,m+1,r);
        merge(arr,l,m,r);
    }
}
```

As we said before, this mergeSort will recursively sort the first and second half and merge both first and second half using merge function. But first and second half are again sorted using same merge function. We put r > l condition before proceeding as we want atleast two elements inorder to sort the array else there is no need to sort the array. Refer [this](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-Sorting/video/OTc3) video for further clarification.


### Merge sort analysis

#### Time complexity of Merge sort

![](https://danusshkumar.github.io/reference-images-for-problem-solving/merge-sort-tc.jpg)

In the view of this mergeSort, the merge() function is called at each level. But for each level, θ(n) of time complexity is required. Let's consider level 1. Here θ(n) tc is required and for level 2, there is only θ(n/2) tc is required but for 2 times, It means θ(n/2)*2 ==> θ(n). Like this, we will get θ(n) for all the levels and we will sum all the θ(n) for all levels.

Number of levels will be expressed as logn and that's why the time comlexity of this algorithm is θ(nlogn)

#### Space complexity of Merge sort

Merge sort will have atmost θ(n) space complexity on level 1, but for subsequence level calls, the space complexity decreases as θ(n/2) for every calls. We have to notice that the space will be deallocated once the function call get finished. the left[] and right[] array got deallocated while doing other calls on the same level. So the atmost auxiliary space required for this is θ(n) in level 1. Note that the auxiliary space is not O(n) as it can't change by the input values (like θ(n) for sorted array and θ(1) for unsorted array like that)


