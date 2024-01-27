
> Problem Solving - 5

# Deep Dive into Sorting - 3

## Intersection of Two sorted arrays:

### Naive solution : O(n*m)

```
void intersection(int[] a,int[] b,int m,int n){
    for(int i = 0;i<n;i++){
        if(i>0 && a[i] == a[i-1]){
            continue;
        }
        for(int j = 0;j<n;j++){
            if(a[i] == b[j]){
                System.out.println(a[i] + " ");
                continue;
            }
        }
    }
}
```

We are traversing through `b` array for every element in `a` array. To avoid duplicates, we are writing the condition when the previous element and current element are same, then skip the iteration and to avioid duplicates in inner array, we write `continue` statement when two elements (`a[i]` and `b[j]` are same) after printing it.


### Efficient solution : O(n+m)

This solution uses the fact that the array is sorted and this solution is based on the `merge` function of mergeSort.

```
void intersection(int[] a,int[] b, int m, int n){
    int i= 0,j = 0;
    while(i<m && j<m){
        if(i>0 && a[i] == a[i-1]){
            i++;
            continue;
        }
        //to avoid duplicates
        
        
        if(a[i] < b[j])
            i++;
        else if(a[i] > b[j])
            j++;
        else {
            System.out.println(a[i] + " ");
            i++;
            j++;
        }
        // to find intersection element
        
    }
}
```

By the above solution, we are comparing a[i] and b[j] and if `a[i] < b[j]` then increment the i value as there won't be element that is equal to a[i] for upcoming b[j] element.
If a[i] > b[j], then we increment j++ as we do in merge sort. If both elements are same, we print the element and increment both i and j value.

To avoid duplicates, we are using the same logic as we see in naive solution. If the current element is equal to previous element, then increment the i value and skip the iteration with continue statement.


## Union of two sorted arrays

### Naive solution: O((m+n)*log(m+n))

First, we merge both the array into single array using auxiliary space and sort that auxiliary arrays. Now print the distinct element from that auxiliary array using the condtion `if(i == 0 || c[i] != c[i-1])`

```
void printUnion(int[] a,int[] b,int m,int n){
    int c[] = new int[m+n];
    //creating auxiliary array
    
    for(int i = 0;i<m;i++)
        c[i] = a[i];
    //copying auxiliary array a to auxiliary array
    
    for(int i = 0;i<n;i++)
        c[m+i] = b[i];
    //copying array b to auxiliary array
    
    Arrays.sort(c); //sorting array c
    
    
    for(int i = 0;i<m+n;i++)
        if(i == 0 || c[i] != c[i-1])
            print(c[i]);
    //printing distinct element from array c
}
```


### Efficient solution : O(n+m)

```
void printUnion(int[] a,int[] b, int m,int n){
    int i = 0,j = 0;
    while(i < m && j < n){
    
        //check for duplicates in array A
        if(i>0 && a[i] == a[i-1]){
            i++;
            continue;
        }
        
        //check for duplicates in array B
        if(j>0 && b[j] == b[j-1]){
            j++;
            continue;
        }
        
        //modified merge sort logic for getting union
        if(a[i] < b[j]){
            print(a[i];
            i++;
        }
        else if(a[i] > b[j]){
            print(b[j]);
            j++;
        }
        else{
            print(a[i]);
            i++;
            j++;
        }
    }
    
    //printing remaining element in array A
    while(i<m){
        if(i>0 && a[i] != a[i-1]){
            print(a[i]);
            i++;
        }
    }
    
    //printing remaining element in array B
    while(j<n){
        if(j>0 && b[j] != b[j-1]){
            print(b[j];
            j++;
        }
    }
}
```

Refer [this](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-Sorting/video/OTgx) video for explanation of this approach

### Count inversion in the array : 
Learn count inversion in the array on [this](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-Sorting/video/OTgy) video


## Partitions in given array

### Naive partition

In this method, on first traversal, all the values less than or eqaul to  the pivot value is added to the temp array and in the second traversal, all the values that are greater than pivot value is added to the temp array. Now, the element got seperated according to the pivot. It's not neccessary that the pivot element must occur in the centre between left and right. Here, pivot element will comes in first half.


```
// Auxiliary space : O(n)
// Time complexity : O(1)
public static  void naivePartition(int[] arr, int l, int h, int p){
    int[] temp = new int[h - l + 1];
    int k = 0;
    for(int i = l; i<=h;i++){
        if(arr[i] < arr[p]){
            temp[k] = arr[i];
            k++;
        }
    }

    temp[k] = arr[p];
    k++;

    for(int i = l;i<=h;i++){
        if(arr[i] > arr[p]){
            temp[k] = arr[i];
            k++;
        }
    }

    for(int i = 0;i<temp.length;i++){
        arr[i + l] = temp[i];
    }
}

```

### Lomuto partition

Lomuto partition assumes that the pivot element is present in last of the array and if the element didn't occur in the last, then the pivot element must be swapped with the last element.
In this partition, if the element is less than the pivot element, then the element will be added to the left half. It's done using this step. By incrementing the i value, we will increase the size of left window and with this window, we will swap current element with ith position so that our element will be added to the end of the left window. 
Note that only the element that are less than the pivot will be added to left half. Here, the pivot element will present in right half of the array. After traversal to (n - 2) as the (n - 1) is pivot, the pivot element get swapped with (i+1)th index. In this partition, the pivot element seperates the left and right window array and the pivot element will be in center position 

```
//Lomuto partition
public static int lPartition(int[] arr,int l, int h, int p){
    swap(arr,h,p);
    int pivot = arr[h];
    int i = l - 1;
    for(int j = l;j<h - 1;j++){
        if(arr[j] < pivot){
            i++;
            swap(arr,i,j);
        }
    }
    swap(arr,i+1,h);
    return i;
}
```

### Hoare's partition

Hoare's partition is similar to lomuto's partition. In this partition, the we have i and j pointer on initially l - 1 and h + 1 which comes towards each other as they filter the elements. On the iteration for i, the element will be checked whether it is placed in left window or to be swapped (curr < pivot), if true, then continue and increment the window size and if false, then go to j iteration.
On j iteration, the loop iterates until mismatch found ( curr > pivot == false ). If curr is less than pivot, then we will, swap the ith and jth index as they are not in correct position. This loop occurs until i and j meet or cross each other. 

In this partition, the pivot element will come under second half of the array and need not present in between right and left half of the array. Hoare's partition is comparatively faster than Naive partition and Lomuto partition.

```
//Hoare's partition
public static int hPartition(int[] arr, int l, int h, int p){
    swap(arr,l,p);
    int pivot = arr[l];
    int i = l - 1, j = h + 1;
    while(true){
        do{
            i++;
        }while(arr[i] < pivot);

        do{
            j--;
        }while(arr[j] > pivot);

        if(i >= j) return j;

        swap(arr,i,j);
    }
}
```


## Quick Sort Introduction

1. It works based on Divide and Conquer algorithm
2. Worst case time : O(n<sup>2</sup>)
3. Despite this time complexity, it is considered faster, because of the following reasons
- In-place
- Cache friendly. As it is in-place, most of the values will more likely to be found in cache. But in case of auxiliary space, there will be two places where value get stored so there will be less chance of CACHE hit
- Average case is O(nlogn)
- Tail recursive
4. Partition is key function( Naive, Lomuto, Hoare's)


### QuickSort using Lomuto partition

```
void qSort(int[] arr,int l, int h){
    if(l < h){
        int p = partition(arr,l,h);
        qSort(arr,l,p-1);
        qSort(arr,p+1,h);
    }
}
// from Lomuto partition as a partition
```
Sorting using Lomuto partition did its work when the array size is 3 as the left element is smaller than or equal to pivot (middle element) and right element is greater than or equal to pivot (middle element). But Hoare's partition did its work when the array size is 2 as the left element is smaller than or equal to pivot and right element is greater than or equal to pivot (middle element). middle element may present in right half and its not the case if there is duplicate element in pivot ( element having same values as pivot) will also appear in first half. So by this, we can conclude that pivot can go anywhere. The hoare's partition only guarantees the left side values will be less than or equal to pivot

### Quicksort using Hoare's partition

```
void qSort(int[] arr,int l,int h){
    if(l < h){
        int p = partition(arr,l,h);
        qSort(arr,l,p);
        qSort(arr,p+1,h);
    }
}
// from hoare's partition
```

There is an study that says that Hoare's partition is three times faster than Hoare's partition on average.

## Analysis of QuickSort

#### Best case

Let's consider the best case, where the chosen pivot is exactly the mid element of the array. So half of the element will be in right half and half of the element in left half. If we do in this manner, it's as like as binary search tree where the element is equally divided into two parts. now, here, the maximum number of recursion call levels will be O(log<sub>2</sub>n). For each levels, we have n time complexity. By overrall time complexity it will be n * logn and we also have some θ(n) work in leaf nodes, recursive call having only one element. There, the time complexity will be

` Tc = O(nlogn) + θ(n)`

` Tc = O(nlogn) `


#### Worst case

In worst case, the pivot is selected in a way such that it's too maximum or too minmum. If pivot is two minimum, there will be only one element in left and n - 1 element in the right window. This state continues as 1 on left, n-2 on right, 1 on left and n-3 on right and so on. In this type, the recursion call stack goes until n times. So the time complexity will be n * (n times of recursion call stack height). So the time complexity will be O(n<sup>2</sup>). 

>Note that these types of cases will arise based on how we choose our pivot. We will discuss about this further on upcoming topics


#### Average case

If we consider that the pivot is selected in a way such that it divides the array into 1 part and 9 parts out of 10 parts ( n and 9n on 10n). Now, the tree will be formed in a irregular way where in one call, the tree will reach the end in too shallowly (where we have only one part) and in some part it will reach the end in too deeply (where we have 9 parts out of 10 parts). In this way, the height of the tree will be log<sub>9/10</sub>n. Hence the height of the recursion tree is logn and there will be n work in every level of tree, so the Tc will be`Tc = O(nlogn)`

Refer [this](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-Sorting/video/OTg5) video for further clarification


## Auxiliary space analysis of QuickSort

We are considering that we are using Lomuto partition and Hoare' partition for QuickSort because considering Naive partition will make our Auxiliary space complexity as O(n). 

When we are not using Naive partition the auxiliary space required will only the goes to recursive call stack. the maximum entry in the recursive call stack is equal to the height of recursion tree. The height of recursion tree again depends on the input, pivot and best, worst and average case. On average, the height of this tree will be logn so our Space complexity will be `O(logn)`. On the first case, where we get the tree like left skew or right skew tree, the height of the tree will be O(n) and thus the space complexity will be `O(n)` in such cases. For further clarification, refer [this](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-Sorting/video/OTkw) video.

### Relationship between choice of pivot and worst case

Worst case always happens when we choose pivot which is too minimum or too maximum. Let's say we are using Hoare's partition (1st element as pivot) and the array is sorted. Every time we partition the array, the call will be like for 1 element on left and n - 1 element on right. 

Consider another case where our array is reversely sorted and we are using Lomuto partition where last element is pivot. In thie every time recursive function is called the call will be like n - 1 on left and 1 element on right side array.

In both the above cases, the time complexity will be O(n<sup>2</sup>) and space complexity will be O(n). This is only due to choosing of pivot as first element/last element. If the input given too our algorithm is sorted then our algorithm will work in slow way. In order to avoid this the pivot will be choosen as random from lth index (low) to hth index (high). In most of the library function that uses quicksort as a sorting algorithm, they choose random number as pivot. In this way, we can increase the probability of not getting worst case and especially we will escape from having worst case for sorted array and reverse sorted arrays.

For further clarification, refer [this](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-Sorting/video/OTkx) video

### Tail call elimination

Learn about tail call elimination for quick sort in [this](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-Sorting/video/OTky) video
