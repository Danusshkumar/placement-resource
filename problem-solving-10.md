> Problem Solving - 10

# LinkedList - I

## Problems with Array Data Structure

```
In C++, 
int arr[100]; //fixed size array and memory is allocated on stack
int arr[n]; //variable sized array and memory is allocated on stack
int* arr = new int[100]; // dynamic array and the memory is allocated at run time on heap
vector<int> v; //allocated on heap

But in Java, memory is always allocated on heap
int arr[100]; //fixed array
int[] arr = new int[n]; //variable sized array
ArrayList<Integer> arr = new ArrayList<>(); //dynamically sized array with size changing
 in run time

```

- The size will be fixed and pre-allocated
- On using dynamically sized array like ArrayList, the time complexity will reach θ(n) when insertion 11th element in arraylist of size 10. New arraylist of size 20 (double the size) will be allocated and all the 10 elements from previous list is copied to new list.
- Insertion and deletion from the middle or at random position is costly and it requires  θ(n) time complexity
- Implementation of data structures like Queue and Deque is complex while using arrays. Inserting element at last will take O(1) but inserting the element at start will require shifting of every element to left position
- In system programming, we will have chunks of random memories, but we didn't have memory contiguously, in that case, we didn't allocate contiguous memory for arrays. But in LinkedList, we can efficiently use those chunks of memory.

**Problems with arrays - example problem**

Replace x with 5 y's in the given string<br><br>
If we are doing this thing with Arrays, we want new ArrayList and we have to copy every element to new arraylist and when we encounter x, we would insert 5y's in that array. But this will require extra array and it also leads to extra overhead of copying array element into the auxiliary array.<br>
*But LinkedList will do this magic in-place*.


## Introduction to LinkedList

- Insertion at random position is not costly
- No need to pre-allocate the memory. If the element is deleted, the memory will be waste in list. But on LinkedList, the memory will actually be deallocated so that there will be `n` memory space for `n` nodes


## Implementatin of LinkedList in C++ and Java

Self-referential structures will form the LinkedList.<br>
Self-referential structure means a structure that has a pointer of type itself. This lead to linkage of one node to another node. So LinkedList is an example for self-referential structure.

```
struct Node {
    int data;
    Node* next;
    Node(int x){
        data = x;
        next = NULL;
    }
}

int main(){
    Node* head = new Node(10);
    Node* temp1 = new Node(20);
    Node* temp2 = new Node(30);
    head->next = temp1;
    temp1->next = temp2;
    return 0;
}
```
Better implementation:
```
struct Node {
    int data;
    Node* next;
    Node(int x){
        data = x;
        next = NULL;
    }
}

int main(){
    Node* head = new Node(10);
    head->next = new Node(20);
    head->next->next = new Node(30);
    return 0;
}
```

Implementation in Java

```
class Node {
    int data;
    Node next;
    Node(int x){
        data = x;
        next = null;
    }
}
class Main{
    public static void main(String[] args){
        Node head = new Node(10);
        Node temp1 = new Node(20);
        Node temp2 = new Node(30);
        head.next = temp1;
        temp1.next = temp2;
    }
}
```

### Applications on LinkedList

1. Worst case insertion at the end and begin are θ(1)
2. Worst case deletion at the end and begin are θ(1)
3. Insertion and deletion at random position is θ(1) if address for previous node is given
4. Round robin implementation is done through LinkedList. Round robin is a CPU scheduling algorithm that is generally implemented using Circular LinkedList.
5. Merging two LinkedList can be done without an auxiliary space so that it's faster than arrays
6. It's a implementation of simple memory manager where we need to link free blocks
7. Easier implementation of Queue and Deque data structures

There are some disadvantages like no cache friendly and no random access


#### LinkedList traversal in C++

Here is an interesting fact about call by reference in C and C++

**Question:** *A function has a parameter of pointer. In this case, if the argument passed to that function is a pointer, then that pointer is copied as a local variable in the function. But if the address is passed as argument, the address got assigned to that pointer. Justify the statement.*<br>
**Answer:**
*The above statement is partially true. A function has a parameter of pointer means that the function expects an address of a variable as an argument. When a pointer is passed as an argument, the pointer itself is copied as a local variable in the function, but it still points to the same address as the original pointer. Therefore, the function can access and modify the value stored at that address through the pointer parameter. However, if the pointer parameter is reassigned to point to another address, it will not affect the original pointer. When an address is passed as an argument, it is equivalent to passing a pointer that points to that address. The address is assigned to the pointer parameter, and the function can access and modify the value stored at that address through the pointer parameter. However, if the pointer parameter is reassigned to point to another address, it will not affect the original address.This behavior is true for both C and C++, since they both use pass-by-value semantics for function parameters. The difference between C and C++ is that C++ also supports pass-by-reference semantics, which means that a function can take a reference (denoted by &) as a parameter instead of a pointer. A reference is an alias for another variable, and any changes made to the reference will be reflected in the original variable. Unlike pointers, references cannot be reassigned to refer to another variable.*

```
void printlist(Node *head){
    Node *curr=head;
    while(curr!=NULL){
        cout<<curr->data<<" ";
        curr=curr->next;
    }
}
```

### LinkedList traversal in Java

Here is an interesting fact about Call by reference in Java

**Question:** *but in Java, there is no pointer or reference and hence all the non-primitive data types are passed as "call by reference". Justify*

**Answer:** *The statement that all the non-primitive data types are passed as “call by reference” in Java is incorrect. Java does not have the concept of pointers or references as in C or C++. Java only has the concept of object references, which are values that represent the memory location of an object. When an object reference is passed as an argument to a method, the reference itself is copied as a local variable in the method, but it still points to the same object as the original reference. Therefore, any changes made to the object’s fields or methods through the reference parameter will affect the original object. However, if the reference parameter is reassigned to point to another object, it will not affect the original reference. This behavior is called pass by value of the reference, not pass by reference.*

```
import java.util.*;

class Node {
    int data;
    Node next;
    Node(int x){
        data = x;
        next = null;
    }
}

public class Main
{
	public static void main(String[] args) {
	    Scanner sc = new Scanner(System.in);
	    System.out.print("input size:");
	    int n = sc.nextInt();
	    int input = sc.nextInt();
	    Node curr = new Node(input);
	    Node head = curr; //storing head pointer
		for(int i = 1;i<n;i++){
		    input = sc.nextInt();
		    curr.next = new Node(input);
		    curr = curr.next;
		}
		
		while(curr != null){
		    System.out.print(head.data + " -> ");
		    head = head.next;
		}
	}
}
```

#### Working of Java
To understand the complete execution of Java, let's break down the components involved: JDK, JRE, Java compiler, and JIT (Just-In-Time) compiler.

1. **JDK (Java Development Kit):**
   The JDK is a software development package that includes tools and utilities needed for developing, compiling, debugging, and running Java applications. It consists of the Java Compiler (javac), Java Runtime Environment (JRE), development tools, and various libraries and APIs. The JDK is necessary for developing and building Java applications.

2. **JRE (Java Runtime Environment):**
   The JRE is an environment required to run Java applications. It includes the Java Virtual Machine (JVM), core classes, runtime libraries, and necessary runtime components. JRE is used by end-users to run Java applications. It does not include development tools like the compiler (javac).

3. **Java Compiler:**
   The Java compiler, usually invoked using the `javac` command, translates Java source code (files with a .java extension) into Java bytecode (files with a .class extension). Java bytecode is a platform-independent intermediate representation of the source code, which can be executed by the Java Virtual Machine (JVM).

4. **JIT (Just-In-Time) Compiler:**
   The JIT compiler is part of the JVM. When a Java application is executed, the JVM interprets the bytecode. Additionally, the JVM's JIT compiler can dynamically compile parts of the bytecode into native machine code specific to the underlying hardware and cache it for faster execution. This allows for improved performance by combining the portability of bytecode with the speed of native machine code.

Now, let's outline the steps of execution in a typical Java application:

- **Write Java Source Code (.java files):**
  Developers create Java source code files with a .java extension using a text editor or an Integrated Development Environment (IDE).

- **Compile Java Source Code (javac):**
  Use the Java compiler (javac) to compile the .java source files into Java bytecode (.class files).

- **Java Virtual Machine (JVM):**
  When executing a Java application, the JVM loads and interprets the Java bytecode. It is the responsibility of the JVM to execute the bytecode, ensuring platform independence.

- **Just-In-Time (JIT) Compilation:**
  During execution, the JVM's JIT compiler can dynamically compile parts of the bytecode into native machine code for improved performance. Before the introduction of Just-In-Time (JIT) compilation, the Java Virtual Machine (JVM) would primarily interpret the bytecode. Interpreting involves translating and executing the bytecode instructions one by one as the program runs. However, this interpretation process can be relatively slow compared to executing native machine code directly.

- **Execution:**
  The JVM executes the Java bytecode (and potentially JIT-compiled native code) on the target hardware, producing the desired program output.

In summary, the JDK is essential for development, providing the Java compiler and development tools, while the JRE is necessary for running Java applications, including the JVM and runtime components. The Java compiler translates source code to bytecode, which is executed by the JVM. The JIT compiler further optimizes performance by dynamically compiling bytecode into native machine code during runtime.

## Recursive traversal of Singly LinkedList in C++ and Java

Recursive traversal of LinkedList in C++
```
void rPrint(Node *head){
    if(head == NULL)
        return;
    cout<<(head->data)<<" ";
    rPrint(head->next);
}
```
Recursive traversal of LinkedList in Java
```
void rPrint(Node head){
    if(head == null)
        return;
    System.out.print(head.data + " ");
    rPrint(head.next);
}
```
### Insert at end in Java


Java implementation:
```
Node temp = new Node(20);

if(head == null)
    return temp;

while(head != null)
    head = head.next;

head.next = temp;
return head;

// if head is null, we have to return the newly created node as head. But it's not a
problem on insert at beginning.
```

### Insert at given position in LinkedList

```
Node insertAtPos(Node head, int x, int pos) {
    Node temp = new Node(x);
    if (head == null) {
        if (pos == 1) return temp;
        else return head;
    } // head null check
    
    if (pos == 1) {
        temp.next = head;
        return temp;
    } //similar to insert at beginning
    
    Node curr = head;
    for (int i = 1; i < pos - 1; i++) {
        curr = curr.next;
        if (curr == null) {
            System.out.println("Position out of range");
            return head;
        }
    }
    temp.next = curr.next;
    curr.next = temp;
    return head;
} //note that the position will be 1-indexed
```

### Delete First node of LinkedList in Java

```
Node delFirstNode(Node head){
    if(head == null)
        return null;
    else
        return head.next;
}
```

#### Garbage collectors in Java

We don’t need to care about deallocation while deleting at the beginning of a linked list in Java because Java has automatic memory management and garbage collection. This means that Java automatically allocates and frees up memory space for objects and variables, without requiring explicit intervention from the programmer. Garbage collection is the process of freeing up memory space by deleting objects that are no longer reachable by any reference variable.

The JVM identifies the object that is no longer referenced by using a process called garbage collection. Garbage collection is the process of freeing up memory space by deleting objects that are no longer reachable by any reference variable. The JVM runs garbage collection periodically to reclaim memory and improve performance.

There are different types of garbage collectors that the JVM can use, but they all follow a similar principle. They start from the so-called garbage collection roots, which are objects that are always reachable by the program, such as static variables, local variables, thread objects, etc. They then traverse all the object references from the roots, and mark every object they find as alive. This is called the mark phase. After the mark phase is completed, they sweep through the heap memory and delete every object that is not marked as alive. This is called the sweep phase. The memory space occupied by the deleted objects can then be reused for new objects.

The JVM is intelligent in choosing when and how to run garbage collection. It can monitor the memory usage and decide when to trigger garbage collection based on various factors, such as the available heap size, the allocation rate, the pause time, etc. It can also use different algorithms and strategies for different regions of the heap, such as generational garbage collection, which divides the heap into young and old generations and collects them separately according to their lifetimes. The JVM can also adapt to different workloads and environments by using different garbage collector implementations, such as serial, parallel, concurrent, or G1 collectors.

Garbage collection is one of the features that makes Java a powerful and versatile programming language. It allows Java programmers to focus on the logic and functionality of their programs, without worrying about memory management or deallocation. It also improves the security and reliability of Java programs, by preventing memory leaks, dangling pointers, or segmentation faults.


## Delete Last of LinkedList in Java

```
Node delTail(Node head){
    if(head == null || head.next == null)
        return null;
    Node curr = head;
    if(curr.next.next != null)
        curr = curr.next;
    curr.next = null;
    return head;
}
```

## Search in LinkedList

Iterative approach:

```
int search(Node head,int x){
    int pos = 1;
    while(head != null){
        if(head.data == x)
            return pos;
        else{
            pos++;
            head = head.next;
        }
    }
    return -1;
}
```

Recursive approach:

```
int search(Node head,int x){
    if(head == null)
        return -1;
    if(head.data == x)
        return 1;
    else {
        int res = search(head.next,x);
        if(res == -1)
            return -1;
        else
            return (res+1);
    }
}
```


