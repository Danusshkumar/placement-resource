> Problem Solving - 7

# Matrix

## 2-Dimensional arrays in C++

- Elements are stored in row-major order meaning that added elements are stored on first row. Once first row gets filled, it comes to next row.
- Elements are stored at contiguous memory location. then the memories are not actually stored in 2D, instead they are stored contiguously one after another row
- Internal curly braces are optional
- Only the first dimension can be omitted when we initialise the array
- From C++14 standard, C++ allows variable sized array. That means the size of the array will be passed as variable instead of having hardcoded value
- Other ways to create multi-dimensional array is to use double pointer.
- In the below program, a double pointer is created and its pointing to the array of pointers. the space for pointers are allocated through the new keyword `arr = new int* [m]` and each pointer points to the array of integers and space for these integers are allocated by `arr[i] = new int[n]`. 
- By this the memory won't be contiguous. The main disadvantage of not being contiguous is that they are not cache friendly. We will get lot more cache misses by thie approach. Hence these dynamic allocation are made on **heap memory**. 
- But by this, we can create individual array of **different sizes**. because ultimately they are all pointers and the memory is allocated through `new` keyword. Such arrays are called **jagged arrays**.

```
#include <iostream>
using namespace std;
int main(){
    int m = 3, n = 2;
    int** arr;
    arr = new int* [m];
    for(int i = 0;i<m;i++)
        arr[i] = new int[n];
    
    for(int i = 0;i<m;i++)
        for(int j = 0;j<n;j++){
            arr[i][j] = 10;
            cout<<arr[i][j]<<" ";
        }
    return 0;
}
```

- The third way of allocating memory is array of pointers pointing to arrays. Memories are allocated on stack rather than heap. But the individual array memory is allocated on heap.

```
#include <iostream>
using namespace std;
int main(){
    int m = 3, n = 2;
    int* arr[m];
    for(int i = 0;i<m;i++)
        arr[i] = new int[n];

    for(int i = 0;i<m;i++)
        for(int j = 0;j<n;j++){
            arr[i][j] = 10;
            cout<<arr[i][j]<<" ";
        }
    
    return 0;
}
```
- The third method of creating 2-D array is to array of vectors

```
#include <iostream>
#include <vector>
using namespace std;

int main()
{	
	int m = 3, n = 2;

	vector<int> arr[m];

	for(int i = 0; i < m; i++)
		for(int j = 0; j < n; j++)
			arr[i].push_back(10);

	for(int i = 0; i < m; i++)
		for(int j = 0; j < n; j++)
			cout << arr[i][j] << " ";

	return 0;
}
```
- Fourth way is to create 2-D array is to create vector of vectors

```
#include <iostream>
#include <vector>
using namespace std;


int main()
{	
	int m = 3, n = 2;

	vector<vector<int>> arr;

	for(int i = 0; i < m; i++){
		vector<int> v;
		for(int j = 0; j < n; j++)
			v.push_back(10);
		arr.push_back(v);
	}

	for(int i = 0; i < arr.size(); i++)
		for(int j = 0; j < arr[i].size(); j++)
			cout << arr[i][j] << " ";

	return 0;
}
```
Both third and fourth way are not cache friendly and the memory are allocated on heap. On third approach, we can dynamically change the size of columns (inner array) and in fourth approach, we can dynamically change the size of rows (outer array).


## Passing multi-dimensional array as an arguments in C++

- `void print(int arr[3][2])`: In this method, the row and column size are hardcoded and we can't be able to pass arguments without those sizes
- `void print(int arr[][2], int m)`: C++ allows us to omit the row size or size of first (outermost dimension) so that we can pass it seperately and making it variable-oriented. But it's not dynamic.
- `void print(int arr[R][C])`: Here, R and C are considered to be globally declared constant variables
- `void print(int** arr, int m, int n)`: It's a C-styled argument passing where we have double pointers and both rows are column size are changed dynamically. 
- `void print(int* arr[], int m,int n)`: It's also a C-styled argument passing where we have array of pointers and column size are changed dynamically
- `void print(vector<int> arr[], int m)`: It's a C++-styled argument passing which is array of vector. We don't need to pass the inner array's size as it is fetched using `arr[i].size()` as it is a vector.
- `void print(vector<vector<int> &arr)`:It's also a C++-styled arguments which is vector of vectors. Both row size and column size are dynamic in nature and we don't have to mention both row size and column size as arguments. Although these are dynamic, they are not cache-friendly. Note that here the vector is received as reference to do optimisation.
- The 2D array is called **jagged arrays** if individual rows have different no.of elements in them.


## Multidimensional arrays in Java

```
int arr[][] = {{1,2,3,8,9},{4,5,6}};
for(int i = 0;i<arr.length;i++)
    for(int j = 0;i<arr[i].length;j++)
        System.out.print(arr[i][j] + " ");
```

- Consider the above program and here the array size is not mentioned there. And the array size is get by the `length` member in the array. Because array is an object in Java. so the memory are dynamically get allocated in java arrays and the memory is stored in Heap.
- On this, there is no need that the individual arrays are contiguous. We can make it contiguous by initialising single array with size M*N and access the each element.
- Definition and initialisation of array in java is different from C and C++. Refer [here](https://www.javatpoint.com/array-in-java) to know more about declaration and initialisation of arrays in java. Some key takeaways are 

```
// Syntax to Declare an Array in Java

dataType[] arr; (or)  
dataType []arr; (or)  
dataType arr[];  

// Instantiation of an Array in Java (allocating memory)
arrayRefVar = new datatype[size];  

// Declaration, Instantiation and Initialization of Java Array
// We can declare, instantiate and initialize the java array together by:

int a[]={33,3,4,5};//declaration, instantiation and initialization

```
Mentioning array size or dimension inside square brackets are not allowed in Java. The memory is allocated through `new` keyword.

```
int arr[]; //declared but memory is not allocated
arr[0] = 5; //not valid
arr = {1,2,3}; //not valid
```

```
int arr[];
arr = new int[5];
arr[0] = 5; //valid
arr = {1,2,3}; //not valid as this syntax works for declaration, 
// instantiation and initialisation in one line
```


```
        int m = 3;
        
    	int arr[][] = new int[m][];

    	for(int i = 0; i < arr.length; i++){
    		arr[i] = new int[i + 1];

    		for(int j = 0; j < arr[i].length; j++){
    		    arr[i][j] = i;
    			System.out.print(arr[i][j] + " ");
    		}
    		
    		System.out.println();
    	}
```
[Here](https://sl.bing.net/ieq4JgtKE3M) is the conversation between me and bing about Java and arrays in Java. Some key takeaways are
- `int[][] arr = new int[3][]` we can have the dynamic size of individual arrays
- Java arrays are allocated in the heap, because arrays are objects, and all Java objects reside on the heap. However, the reference to the array, which is a local variable, resides on the stack.
- Inner curly braces are neccessary in java on initialisation as the size of rows and columns are not specified on declaration.
- Why Java is designed like this ?

Java is a high-level programming language that aims to be portable, efficient, and secure. One of the design choices of Java is to use a heap-based memory management system, where objects and arrays are dynamically allocated and garbage collected. This has some advantages and disadvantages compared to a stack-based memory management system, where variables are allocated and deallocated automatically as they enter and exit the scope. 

Some of the advantages of heap-based memory management are:

It allows for dynamic allocation of memory, which means that the size of the data structures does not need to be known at compile time, and can grow or shrink as needed at runtime.
It simplifies the implementation of complex data structures, such as linked lists, trees, graphs, etc., which would be difficult or impossible to implement using only stack memory.
It avoids memory fragmentation, which is a problem that occurs when the stack memory becomes full of holes due to variables being allocated and deallocated at different times and sizes.
It enables polymorphism, which is a feature that allows objects of different types to be treated as if they belong to a common type. For example, an array of objects can store references to objects of different subclasses, and invoke the appropriate methods based on their actual type.

Some of the disadvantages of heap-based memory management are:

It requires more memory space, because each object or array has some overhead information, such as its type, size, reference count, etc., that needs to be stored along with its data.
It introduces performance overhead, because allocating and deallocating memory on the heap is slower than on the stack, and garbage collection can cause pauses or delays in the execution of the program.
It can cause memory leaks, which are situations where some objects or arrays are no longer needed by the program, but are still referenced by some variables or other objects, and thus cannot be garbage collected. This can lead to wasting memory resources and eventually running out of memory.


### Passing 2D arrays as arguments in Java
- we can use `public static void print(int arr[][])` or `public static void print(int[][]  arr)` to pass arrays as an arguments in Java.
- It's very cleaner when compared to C++

## Problems on Matrix

### Matrix in snake pattern

```
void printSnake(int mat[][]){
    for(int i = 0;i<mat.length;i++)
        if(i%2 == 0)
            for(int j = 0;j<mat[i].length;j++)
                print(mat[i][j] + " ");
        else 
            for(int j = mat[i].length - 1;j>=0;j--)
                print(mat[i][j] + " ");
    
}
```

### Matrix boundary traversal

```
import java.util.*;

class Main { 

	static int R = 4, C = 4;

	static void bTraversal(int mat[][]) {
		if(R == 1){
			for(int i = 0; i < C; i++)
				System.out.print(mat[0][i] + " ");
		}
		else if(C == 1) {
			for(int i = 0; i < R; i++)
				System.out.print(mat[i][0] + " ");
		}
		else {
			for(int i = 0; i < C; i++)
				System.out.print(mat[0][i] + " ");
			for(int i = 1; i < R; i++)
				System.out.print(mat[i][C - 1] + " ");
			for(int i = C - 2; i >= 0; i--)
				System.out.print(mat[R - 1][i] + " ");
			for(int i = R - 2; i >= 1; i--)
				System.out.print(mat[i][0] + " ");
		}
	}

	public static void main(String args[]) {
        int arr[][] = {{1, 2, 3, 4},
    				   {5, 6, 7, 8},
    				   {9, 10, 11, 12},
    				   {13, 14, 15, 16}};

    	bTraversal(arr);
    } 
}
```


### Transpose of the matrix:

As we guessed, the naive solution is to copy the each row into the each column of new matrix(2-dimensional temporary array) and to copy that temp to the original matrix.
Refer [here](https://ide.geeksforgeeks.org/fdvQJovSi6) for the source code for naive approach.

But the efficient approach is to swap the upper diagonal element with the lower diagonal element. The diagonal element remains same even after the transpose of the matrix. Here is the efficient code implementation

```
void swap(int mat[][], int i, int j) {
		int temp = mat[i][j];
		mat[i][j] = mat[j][i];
		mat[j][i] = temp;
}

void transpose(int mat[][]) {
    int n = mat.length; //no.of rows
	for(int i = 0; i < n; i++)
		for(int j = i + 1; j < n; j++)
			swap(mat, i, j);
}
```

### Rotate matrix by 90<sup>o</sup> in anti-clockwise direction

In this problem, each and every row is converted into column but in reverse direction. 
So by naive approach, we are creating one temporary matrix and copying each rows into each columns in reverse manner. Here is the code for that.

```
void rotate(int[][] mat,int n){
    int temp = new int[n][n];
    for(int i = 0;i<n;i++)
        for(int j = 0;j<n;j++)
            temp[n-1-j][i] = arr[i][j];
    
    for(int i = 0;i<n;i++)
        for(int j = 0;j<n;j++)
            arr[i][j] = temp[i][j];
}
```

But this approach requires, quadratic time complexity and quadratic space complexity. But ultimately we have to convert all the rows into columns in reverse manner.

For that, in the efficient solution, we are first transpose the matrix for converting all rows into columns and reversing every columns using simple row reversal algorithm.

```
void rotate(int[][] mat,int n){
    for(int i = 0;i<n;i++)
        for(int j = i + 1;j<n;j++)
            swap(arr,i,j);
    //transposing matrix
    
    for(int i = 0;i<n;i++){
        int l = 0, h = n - 1;
        while(l < h){
            swap(arr[l][i],arr[h][i]);
            l++;
            h--;
        }
    }
    //reversing the columns (reversing row th element of each column)
}
```

### Spiral traversal of matrix

Here we are doing spiral traversal of the matrix by maintaining 4 variables, top, right, bottom and left. We are manipulating these variables to get the spiral pattern. [Here](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-Matrix/video/MTQ1Mg%3D%3D) is the detailed explanation of the below algorithm

```
static void printSpiral(int mat[][], int R, int C) {

	int top = 0, left = 0, bottom = R - 1, right = C - 1;
	while(top <= bottom && left <= right) {
	
		for(int i = left; i <= right; i++)
			System.out.print(mat[top][i] + " ");
		//top traversal

		top++;

		for(int i = top; i <= bottom; i++)
			System.out.print(mat[i][right] + " ");
		//right traversal
		
		right--;

		if(top <= bottom){
		    for(int i = right; i >= left; i--)
			    System.out.print(mat[bottom][i] + " ");
		    bottom--;
		}
		//bottom traversal

		if(left <= right){
		    for(int i = bottom; i >= top; i--)
			    System.out.print(mat[i][left] + " ");
		    left++;
		}
		//left traversal
	}
}
```

### Search in a Row-wise and Column-wise sorted matrix

#### Naive solution : O(R*C)
```
void search(int[][] mat,int x){
    for(int i = 0;i<R;i++)
        for(int j = 0;j<C;j++)
            if(mat[i][j] == x)
                print("found and position");
    //traversing all the arrays
    
    print("not found");
}
```

#### Efficient solution: O(R+C)

The below solution uses the fact that the rows and columsn are sorted. We begin from top right corner. Now if the `x` is greater then currElement, then there is no point in searching the same row as all the element would be smaller than `x`. So now, move on next row by incrementing `i`. If `x` is smaller then currElement, then ther is no point in searching in that column as all the elements on that column after currElement would be greater because the column also sorted, so move in the row in reverse manner by decrementing `j`. This process continues until we cross the boundaries. Note that we can also take the left bottom element as our starting point. In that case, we have to decrement `i` if the `x` is smaller and we have to increment `j` if the `x` is greater.  To know more about this solution, click [here](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-Matrix/video/MTQ1OQ%3D%3D).

```
void search(int[][] mat,int x){
    int i = 0, j = C - 1;
    while(i > R && j >= 0){
        if(mat[i][j] == x){
            print("found and position);
            return;
        }
        else if(mat[i][j] > x)
            j--;
        else
            i++;
    }
    print("not found");
}
```


### Median of Row Wise sorted matrix

#### Naive approach

In naive approach, all the row elements are added into one auxiliary array and the auxiliary array is sorted. Now we can find the median element which is at mid position of the array if the array length is odd and is the average of mid elements if the array length is even. 


#### Efficient approach

```
import java.util.Arrays;

static public int matMed(int mat[][], int r ,int c) {
	int min = mat[0][0], max = mat[0][c-1];
	for (int i=1; i<r; i++) {
		if (mat[i][0] < min)
			min = mat[i][0];
		if (mat[i][c-1] > max)
			max = mat[i][c-1];
	} // finding the max and min of the matrix
	int medPos = (r * c + 1) / 2; //finding the desired median position
	while (min < max) { // running loop until min and max are same
		int mid = (min + max) / 2;
		int midPos = 0; // calculate median position
        int pos = 0;
		for (int i = 0; i < r; ++i) {
			    pos = Arrays.binarySearch(mat[i],mid);
			    midPos += Math.abs(pos); //updating the median position
		}
		
		// moving min and max according to the deviation
		// between calculated median position and desired median position
		if (midPos < medPos)
			min = mid + 1;
		else
			max = mid;
	}
	return min;
}

```
