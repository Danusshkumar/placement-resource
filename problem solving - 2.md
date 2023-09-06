> Problem Solving - 2

## Binary search


```
public static void binarySearch(int[] arr,int target){
    int low = 0;
    int high = arr.length - 1;
    while(low<=high){
        mid = low + (high - low)/2;
        if(target == arr[mid])
            return -1;
        else if(target < arr[mid])
            high = mid - 1;
        else if(target > arr[mid])
            low = mid + 1;
    }
    return -1;
}
```

- It's always best practise to use  `mid = low + (high - low)/2` then `mid = (low + high)/2` as the second one may cause overflow (Integer overflow) in some cases
- We use `high = mid - 1` and `low = mid + 1` instead of `high = mid` and `low = mid` because of the nature of floor division
- Binary search works on the principle such that the search space have to shrink and it have to reach 0 (overlapping of two pointers). And division simply won't shrink the search space if the search space is 2 due to the nature of floor division. That's why we increase/decrease the mid and assigning it to low and high respectively.
- condition `low<=high` is also important as `low<high` will return false return if high and low are in the same position and the target also present in same position. The program doesn't enter the loop as the condition fails. 
- The working of binary tree is that it shrinks with division and arithmetic operations(addition and subtraction) until two pointers overlaps. If we can't find the target until the two pointers overlap, then we return -1 which means that the element is not present in the array
- For further reference, check out the conversation between me and bing [here](https://sl.bing.net/fXMlnAnHArY). Use Microsoft edge to view the full chat


### Recursive approach

```
public static int recursiveSearch(int[] arr,int target,int low,int high){
    if(high < low) {
        return -1;
    }
    
    int mid = low + (high - low)/2;
    if(target == arr[mid]){
        return mid;
    }
    else if(target < arr[mid]){
        return recursiveSearch(arr,target,low,mid - 1);
    }
    else {
        return recursiveSearch(arr,target,mid+1,high);
    }
}
```

Here we write the condition as `high < low` instead of `high <= low` as it is not a condition for recursion continuation but for recursion termination

### Time Complexity 

For successful searches (target is present in the array), we have O(logn) time complexity. But in unsuccessful searches (target is not present in the array), we have theta(logn) time complexity.


## Searching element in rotated sorted array

```
class Solution {
    public int search(int[] arr, int target) {
        int low = 0;
        int high = arr.length - 1;

        while(low <= high){
            int mid = low + (high - low)/2;
            if(arr[mid] == target)
                return mid;

            if(arr[low] <= arr[mid]){
                if(arr[low] <= target && arr[mid] > target){
                    high = mid - 1;
                }
                else {
                    low = mid + 1;
                }
            }
            else {
                if(arr[mid] < target && arr[high] >= target){
                    low = mid + 1;
                }
                else {
                    high = mid - 1;
                }
            }
            
        }
        return -1;
    }
}
```

- The problem is interesting and tough to solve. 
- In this problem, we have a guarantee that one side will be sorted
- Let's check whether the first half is sorted
- If yes, then check whether our element present in that range or not
- If yes, then go with first half else, go for second half
- If the first half is not sorted then consider that the second half will be sorted
- Check whether the element will present in those range.
- If yes, then go with second half else go with first half
- All the concept will be clear but I am affected on assigning the low,mid,high value on checking
- for checking target element present between first half ==> `arr[low] < target && arr[mid] > target`
- for checking target element presence between second half ==>  `arr[mid] < target && arr[high] > target` must be used
- And we have to use `<=` and `>=` for all cases except the checking between `arr[mid] and target` as it's equality is checked already by  `if(arr[mid] == target) return mid;`
- But we have to put `<=` for comparing `arr[low]` and `arr[mid]` as it may be equal


## Searching peak element in unsorted array with O(logn) 

```
class Solution {
    public int findPeakElement(int[] arr) {
        int n = arr.length;
        int low = 0;
        int high = n - 1;

        while(low <= high){
            int mid = low + (high - low)/2;
            if( ( ( mid == 0) || (arr[mid] >= arr[mid-1]) ) && ( ( mid == n-1) || (arr[mid] >= arr[mid+1]) ) )
                return mid;
            else if(mid > 0 && arr[mid - 1] >= arr[mid])
                high = mid - 1;
            else 
                low = mid + 1;
        }

        return -1;
    }
}
```

- This was one of the mesmerizing problem that I ever seen.
- The peak element is the element which is not less than its adjacent element (equal is allowed)
- For corner element (arr[0] and arr[n-1]), we don't have to check the non-existing side. If the condition satisfies the existing side, then we can declare it as peak element
- The solution will be developed from the fact that for any independent unsorted array, there must exist atleast one peak element irrespective of length of that independent array
- We have to find that independent array and do binary search on it.
- find the mid element
- If the left adjacent element is greater than or equal to mid element, then we may go to left side as this will be an independent unsorted array or else we may go for right side
- Or any independent element, we may not care about it corner edges, right. But our independent array is not full array and it's a subarray so we have to care about corner case.
- But it's meaningless, because we chooses that array, as it satisfies the corner case (on mid element comparison)
- The solution may be found meaningless but it would make sense if you watch [this video](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-Searching/video/MTU3MDQ%3D)


## Triplets in the sorted array

Refer [this](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-Searching/video/NzAyMg%3D%3D) video

## Sliding window technique on unsorted array

Let's consider [this](https://github.com/Danusshkumar/geeks-for-geeks-problems/blob/main/subarrayWithGivenSum.java) problem, Subarray with given sum.

We can use sliding window technique to find whether there is an subarray with given sum or not. This sliding window technique will work for both sorted and unsorted array but the array must not contains negative elements.
If there is any negative element, it'll break the condition checking (the core principle ) of sliding window technique which results in wrong results. But without negative elements, sliding window technique will be applied for both sorted and unsorted arrays.

In this technique, we have to maintain one array with left and right side ends and if the sum of this subarray is greater than target, remove one element (left element) and if the sum of this subarray is smaller than target, add one element (right element) and if the sum of this subarray is equal to target, then return the starting point (left) and ending point (right) of that subarray. 


## Median of Two sorted array in O(logN)

In this problem, we have to sync the mid point of both the arrays. We have to set the first array as the smaller array ( if not, then swap the arrays). And then,sync the mid point of second array with the formula `(n1 + n2 + 1)/2 - i1` where i1 is the mid point of first array. Here mid point is where the all the elements in the left are smaller than mid point and all the element in the right are greater than mid point. We are using Integer.MAX_VALUE and Integer.MIN_VALUE for some corner cases.

Note that max1 and max2 are the maximum of first half of corresponding arrays and 
min1 and min2 are the minimum of second half of the corresponding arrays.

The core idea is that the left side element must be smaller or equal to both i1 and i2 (i1 and i2 are min1 and min2 respectively) and right side element must be greater than max1 and max2 where max1 and max2 are maximum element in left half of the array. 

>Note: i1 and i2 are the beginning of right half of the array and they are belongs to right half. Left half size will somewhat greater than right half size by 1 if there are odd number of elements present in array)

```
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int n1 = nums1.length, n2 = nums2.length;
        //swapping the reference if n1 > n2
        if(n1 > n2){
            return findMedianSortedArrays(nums2,nums1);
        }
        int begin = 0, end = n1;
        
        while(begin <= end){
            int i1 = begin + (end - begin)/2;
            int i2 = (n1 + n2 + 1)/2 - i1;

            int min1 = (i1 == n1) ? Integer.MAX_VALUE : nums1[i1];
            int min2 = (i2 == n2) ? Integer.MAX_VALUE : nums2[i2];
            int max1 = (i1 == 0) ? Integer.MIN_VALUE : nums1[i1 - 1];
            int max2 = (i2 == 0) ? Integer.MIN_VALUE : nums2[i2 - 1];

            //main logic goes here
            if(max1 <= min2 && min1 >= max2){
                // we found the mid element here
                if( (n1+n2)%2 == 0 ){
                    //even number of elements
                    return (double) (Math.min(min1,min2) + Math.max(max1,max2))/2;
                }
                else {
                    // odd number of elements
                    return (double) Math.max(max1,max2);
                }

            }
            else if(max1 > min2){
                // move to right side
                end = i1 - 1;
            }
            else {
                //move to left side
                begin = i1 + 1;
            }
        }

        return -1;
    }
}
```
