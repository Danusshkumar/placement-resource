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

