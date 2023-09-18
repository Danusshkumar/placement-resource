> Problem Solving - 6

# Deep Dive into Sorting - 4

## Sorting problems

1. K<sup>th</sup> smallest element
2. Minimum difference in an Array
3. Chocolate distribution problem
4. Sort an array with two types of elements
5. Sort an array with three types of elements
6. Merge overlapping intervals
7. Meeting the maximum guests

#### K<sup>th</sup> smallest element

```
import java.util.*;
import java.lang.*;
import java.io.*;

class Solution
{
    public static void main (String[] args) 
    {
        int arr[] = new int[]{10,4,5,8,11,6,26};
        
        int n = arr.length;int k=5;
        int element=kthSmallest(arr,n,k);
        
        System.out.print(element);
        
    }
    
    static int partition(int arr[], int l, int h)
    {   
        int pivot=arr[h];
        int i=l-1;
        for(int j=l;j<=h-1;j++){
            if(arr[j]<pivot){
                i++;
                int temp=arr[i];
                arr[i]=arr[j];
                arr[j]=temp;
            }
        }
        int temp=arr[i+1];
        arr[i+1]=arr[h];
        arr[h]=temp;
        return i+1;
    } // Lomuto partition
    
    static int kthSmallest(int arr[],int n,int k){
        int l=0,r=n-1;
        while(l<=r){
            int p=partition(arr,l,r);
            if(p==k-1)
                return arr[p];
            else if(p>k-1)
                r=p-1;
            else
                l=p+1;
        } // as like as binary search tree we are traversing for kth smallest element
        // where kth smallest element occurs in (k-1)th index in the sorted array
        return -1;
    }
}

```

In the above approach, we are sorting the elements using Quicksort Lomuto partition method. Because on first partition, the elemen will be splitted according to pivot element. Now, the element should be rearranged within first half and second half inorder to make them sorted. Because pivot element is sorted meaning that it sorted to its correct place. So, if the `pivot == k - 1`, then the pivot element is the index of kth smallest element

#### Minimum difference in an Array

```
    int getMinDiff(int arr[], int n){
        Arrays.sort(arr);
        
        int res = Integer.MAX_VALUE;
        for(int i = 1; i < n; i++){
            res = Math.min(res, arr[i] - arr[i-1]);
        }
        return res;
    }

```
The idea to get minimum difference in the array is so simple. We have to choose two elements from the array such that their difference is minimum. We are sorting the array as it would make the value wise element closer to each other. Now we are traversing array from second element and calculating difference between currentElement(`arr[i]`) and previousElement(`arr[i - 1`). minimum of these difference will be returned(`res`)

#### Chocolate distribution problem

```

class Solution
{
    public long findMinDiff (ArrayList<Integer> arr, int n, int m)
    {
        Collections.sort(arr);
        long minRes = Integer.MAX_VALUE;
        for(int i = 0;i<=(n - m);i++){
            long res = arr.get(i + m - 1) - arr.get(i);
            minRes = Math.min(minRes,res);
        }
        
        return minRes;
        
    }
}
```
Read the problem statement [here](https://practice.geeksforgeeks.org/problems/chocolate-distribution-problem3825/1). In this problem statement, we have to distribute the chocolates among m children. This problem is similar to minimum difference problem, but in this problem, we are taking the difference between elements at m distance instead of taking difference between adjacent elements. From those differences, the minimum difference will be returned

#### Sort an array with two types of elements

```
static void sort(int arr[],int n){
    int i=-1,j=n;
    while(true)
    {
        do{i++;}while(arr[i]<0);
        do{j--;}while(arr[j]>=0);
        if(i>=j)return;
        
        //swapping arr[i] & arr[j]
        int temp=arr[i];
        arr[i]=arr[j];
        arr[j]=temp;
        
    }
}
```
Sorting the odd and even elements based on Hoare's partition. We may also solve the problem using Lomuto partition

#### Sort an array with three types of elements

```
static void sort(int arr[],int n){
    int l=0,h=n-1,mid=0;
    while(mid<=h){
        switch(arr[mid]){
            case 0:
                //swapping arr[l] & arr[mid])
                int temp=arr[l];
                arr[l]=arr[mid];
                arr[mid]=temp;
                
                l++;
                mid++;
                break;
            case 1:
                mid++;
                break;
            case 2:
                //swapping arr[h] & arr[mid])
                temp=arr[h];
                arr[h]=arr[mid];
                arr[mid]=temp;
                    
                h--;
                break;
        }
    }
    
}
```
Refer [this](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-Sorting/video/OTk2) video for clear explanation and interesting and related problem statements

#### Merge overlapping intervals

The solution of the problem will somewhat like [this](https://leetcode.com/problems/merge-intervals/) LeetCode problem solution

#### Meeting the maximum guests

```
import java.util.*;
import java.lang.*;
import java.io.*;

class Solution
{
    public static void main (String[] args) 
    {
        int arr[] = { 900, 600, 700};
        int dep[] = { 1000, 800, 730};
        int n = arr.length; 
        
        System.out.print(maxGuest(arr,dep, n));
        
    }
    
    static int maxGuest(int arr[],int dep[],int n)  
    {  
        Arrays.sort(arr);
        Arrays.sort(dep);
        
        int i=1,j=0,res=1,curr=1;
        while(i<n && j<n){
            if(arr[i]<dep[j]){
                curr++;i++;
            }
            else{
                curr--;j++;
            }
            res=Math.max(curr,res);
        }
       return res;
    } 
}

```

Some problems like maximum railway tracks, maximum number of meeting that we can attend and maximum number of guests we can meet and all other problems that involves intervals are solved using this approach. If we have to maximum number of meeting happen at time t, we have to choose the time that is common to most of the interval. Previously we got a auxiliary space for starting most time and ending most time. Now, we will increment the numbers on those indexes by 1. then we will return the maximum value of these auxiliary array. But this optmised solution involving merge function of mergeSort is somewhat intersting. By this, we are sorting arrival and departure array, and if we found arrival of one person, then increment the count and if we found departure of one person, decrement the count. By this way, we are keeping track of count and getting maximum on those counts as results. Refer [this](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-Sorting/video/MTU4NQ%3D%3D) video for further understanding.

## Special case sorting

1. Cycle sort
2. Heap sort
3. Counting sort
4. Radix sort
5. Bucket sort


### Cycle sort

#### Properties of cycle sort:

1. Worst case time complexity is O(n<sup>2</sup>)
2. It does minimum memory writes and will be useful where the memory writes are costly
3. In-place algorithm (no extra memory is required) and the algorithm is not stable
4. This will be useful to solve the questions like minimum number of swaps required to sort the array.

##### Algorithm
```
void cycleSort(int[] arr){
    int n = arr.length;
    for(int cs = 0;cs<n-1;cs++){
        int pos = cs;
        int item = arr[pos];
        for(int i = cs + 1;i<n;i++)
            if(arr[i] < item)
                pos++;
        swap(item,arr[pos]);
        //processing first element of cycle
        while(pos != cs){
            pos = cs;
            for(int i = cs + 1;i<n;i++)
                if(arr[i] < item)
                    pos++;
            swap(item,arr[pos]);
        }
        //processing remaining elements of cycle until cycle ends
        // cycle will ends when the cycle again comes to its staring position
    }
}
```

### Heap sort

### Counting sort

1. The time complexity of this algorithm is O(n+k) where k is the maximum element of the array. space complexity will be O(n+k).
2. It's not a comparisong based algorithm which takes O(nlogn) time complexity
3. This won't be a better choice if the k value is too large.
4. This algorithm works in linear time complexity but works better than other comparison based only if the k is smaller
5. The time complexity will increase if the k is n<sup>2</sup> or n<sup>3</sup>

##### Algorithm
```
void countingSort(int[] arr){
    int k = arr[0];
    int n = arr.length;
    for(int i = 0;i<n;i++){
        k = Math.max(k,arr[i]);
    }
    k += 1;//to store the max element (k)
    int count = new int[k];
    for(int i = 0;i<n;i++){
        count[arr[i]] += 1;
    }
    
    int idx = 0;
    for(int i = 0;i<k;i++){
        for(int j = 0;i<count[i];j++){
            arr[idx] = i;
            idx++;
        }
    }
}
```

##### General purpose counting sort algorithm

```
void countingSort(int[] arr){
    int k = arr[0];
    int n = arr.length;
    
    for(int i = 0;i<n;i++)
        k = Math.max(k,arr[i]);
    k += 1;// to stor the max element (k)
        
    int count = new int[k];
    for(int i = 0;i<n;i++)
        count[arr[i]] += 1;
        
    for(int i = 1;i<n;i++)
        count[i] = count[i] + count[i-1];
    
    int output = new int[n];
    for(int i = n-1;i>=0;i--){
        output[count[arr[i]] - 1] = arr[i];
        count[arr[i]] -= 1;
    }
    
    for(int i = 0;i<n;i++)
        arr[i] = output[i];
}
```

Refer [this](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-Sorting/video/MTQyNQ%3D%3D) video for clear explanation of the **general purpose counting sort algorithm**


### Radix sort

Radix sort internally uses counting sort but will works in less time complexity even though k is n<sup>2</sup> or n<sup>3</sup>. Time complexity of this algorithm is O(d * log(n*b)) where b is the base of the digit. Here base is 10. we can increase the base so that the space complexity increases and time complexity decreases. The base is simply a trade-off between time complexity and space complexity.

Refer [this](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-Sorting/video/MTQyOA%3D%3D) video for complete understanding and visualisation of radix sort

##### Algorithm

```
void radixSort(int[] arr){
    int n = arr.length;
    int k = arr[0];
    for(int i = 0;i<n;i++)
        k = Math.max(k,arr[i]);
    
    for(int exp = 1;k/exp > 0;exp *= 10)
        countingSort(int[] arr,k,exp);
}

void countingSort(int[] arr,int k,int exp){
    int[] count = new int[10];
    int[] output =new int[10];
    
    for(int i = 0;i<n;i++)
        count[(arr[i]/exp)%10] += 1;
    
    for(int i = 1;i<n;i++)
        count[i] = count[i] + count[i - 1];
    
    for(int i = n - 1;i>=0;i--){
        count[(arr[i]/exp)%10] -= 1;
        output[count[(arr[i]/exp)%10] - 1] = arr[i];
    }
    
    for(int i = 0;i<n;i++)
        arr[i] = output[i];
}
```

### Bucket sort

Bucket sort is known for its linear time complexity for sorting the uniformly distributed array. I here mention that the array is uniformly distributed which means if we seperate array elements into five buckets (consider array has 100 elements) each and every bucket must hold 20 element. Note that the range of element that bucket must hold will be as follows (1 to 19), (20, 39), (40, 59), (60, 79), (80, 99). These type of distribution is called uniform distribution and if the list elements are not uniformly distributed, then the time complexity will ultimately reach O(n<sup>2</sup>). Inorder to achieve the linear time complexity we assume that the elements are distributed uniformly and the number of buckets will be equal to number of elements (k = n). Note that increased no.of buckets won't increase space complexity. because 5 buckets with 20 elements each will give 100 elements and 100 buckets with 1 element will also gives 100 elements. But making k ~= n will reduce the time complexity making sorting for the individual bucket will take constant time O(1). 

```
void bucketSort(int[] arr,int k){
    //assuming here that the no.of bukets are given as input
    int max = arr[0];
    int n = arr.length;
    
    //finding maximum of the array
    for(int i  = 0;i<n;i++){
        max = Math.max(max,arr[i]);
    }
    max += 1;
    
    //creating buckets
    ArrayList<ArrayList<Integer> bkts = new ArrayList<>();
    for(int i = 0;i<k;i++)
        bkts.add(new ArrayList<Integer>());
    
    //adding elements to the buckets
    for(int i = 0;i<n;i++){
        int btkIdx = (k * (arr[i])/max;
        bkts.get(bktIdx).add(arr[i]);
    }
    
    //sorting individual buckets
    for(int i = 0;i<k;i++)
        Collections.sort(bkts.get(i));
        
    //getting elements from buckets and adding it into original array
    int idx = 0;
    for(int i = 0;i<k;i++)
        for(int j = 0;j<bkts.get(i).size();j++){
            arr[idx] = bkts.get(i).get(j);
            idx++;
        }
}
```

Bucket sort is ultimately using `Collections.sort()` or any other sorting algorithm to sort the individual buckets. Main purpose of the algorithms is to make the no.of elements in the individual buckets as low as possible so that sorting individual buckets will take O(1) time complexity. The core part of this bucket sort is to put the element in the correct buckets and that's done using the formula `(k*arr[i])/max` where `max` is the maximum element + 1. If max is not max + 1, then max element will require new bucket that is out of bound index to store the maximum element. That's why we are incrementing the max by one. Refer [this](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-Sorting/video/MTU1MQ%3D%3D) video for further clarification.




