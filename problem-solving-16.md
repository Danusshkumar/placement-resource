> Problem Solving - 16

# Stack

## Stack operations

| Functions | Working |
| --- | --- |
| `isEmpty` | Returns true if stack is empty |
| `push(x)` | Inserts an item on top of the stack |
| `pop()` | Removes an item on top of the stack |
| `peek()` | Returns the top item |
| `size()` | Returns the size of the stack |

## Corner conditions on stack

- Stack underflow - occurs when pop() or peek() called on empty stack
- Stack overflor - occurs when push() called on full stack

## Stack implementation using Array

```
import java.util.*;

class MyStack {
    int capacity;
    int[] arr;
    int head;
    
    MyStack(int capacity){
        this.capacity = capacity;
        arr = new int[capacity];
        head = -1;
    }
    
    void push(int data){
        if(head != capacity - 1){
            head += 1;
            arr[head] = data;
            System.out.println(data + " added into stack");
        }
        else {
            System.out.println("Stack is full");
        }
    }
    
    void pop(){
        if(head != -1){
            System.out.println(arr[head] + " remove from stack");
            head -= 1;
        }
        else {
            System.out.println("Stack is empty");
        }
    }
    
    void peek(){
        if(head != -1){
            System.out.println(arr[head] + " is the peek element");
        }
        else {
            System.out.println("Stack is empty");
        }
    }
    
    void size(){
        System.out.println("Size of the stack is " + (head+1));
    }
    
    void isEmpty(){
        if(head != -1)
            System.out.println("false");
        else
            System.out.println("true");
    }
    
}

public class Main {
	public static void main(String[] args) {
	    MyStack stack = new MyStack(10);
	    Scanner sc = new Scanner(System.in);
	    int x;
	    Boolean noExit = true;
	    System.out.println("Stack implemented in array");
	    System.out.println("Stack size : 10");
	    while(noExit){
	        System.out.print("operation: ");
	        String input = sc.nextLine();
	        switch(input){
                case "push":
                    System.out.print("element: ");
                    x = sc.nextInt();
                    stack.push(x);
                    break;
                case "pop":
                    stack.pop();
                    break;
                case "peek":
                    stack.peek();
                    break;
                case "size":
                    stack.size();
                    break;
                case "isEmpty":
                    stack.isEmpty();
                    break;
                case "exit":
                    noExit = false;
                    break;
	        }
	    }
	}
}
```

![image.png](https://i.postimg.cc/GtnmBYbJ/image.png "Stack implementation using ArrayList in Java")

## Stack implementation using LinkedList

```
import java.util.*;

class Node {
    int data;
    Node next;
    Node(int data){
        this.data = data;
        
    }
}

class Stack {
    
    Node head;
    int size;
    
    Stack(){
        head = null;
        size = 0;
    }
    
    void push(int data){
        Node temp = new Node(data);
        temp.next = head;
        head = temp;
        System.out.println(data + "inserted into stack");
        size++;
    }
    
    void pop(){
        if(head != null){
            System.out.println(head.data + " removed from the stack");
            head = head.next;
            size--;
        }
        else {
            System.out.println("Stack is empty");
        }
    }
    
    void peek(){
        if(head != null){
            System.out.println(head.data + " is the peek element");
        }
        else {
            System.out.println("Stack is empty");
        }
    }
    
    void size(){
        System.out.println("Size of the stack is " + size);
    }
    
    void isEmpty(){
        System.out.println(size == 0);
    }
    
    
}

public class Main {
	public static void main(String[] args) {
	    Stack st = new Stack();
	    Scanner sc = new Scanner(System.in);
	    int x;
	    Boolean noExit = true;
	    System.out.println("Stack implemented in LinkedList");
	    System.out.println("Stack size : dynamic");
	    while(noExit){
	        System.out.print("operation: ");
	        String input = sc.nextLine();
	        switch(input){
                case "push":
                    System.out.print("element: ");
                    x = sc.nextInt();
                    st.push(x);
                    break;
                case "pop":
                    st.pop();
                    break;
                case "peek":
                    st.peek();
                    break;
                case "size":
                    st.size();
                    break;
                case "isEmpty":
                    st.isEmpty();
                    break;
                case "exit":
                    noExit = false;
                    break;
	        }
	    }
	}
}

```

### Applications of Stack

- Function calls
- Balanced parenthesis
- Reversing items
- Infix to Postfix/Prefix
- Evaluation of Postfix/Prefix
- Stock Span problem
- Undo/Redo or Forward/Backward in browsers


### Stack in Java

![image.png](https://i.postimg.cc/YC7ygdPV/image.png "Hierarchy of Stack in Java")

### Balanced parenthesis

```
Class Solution {
    public boolean isMatch(char a,char b){
        return ( (a == '(' && b == ')') || (a == '{' && b == '}') || (a == '[' && b == ']') );
    }

    public boolean isValid(String s) {
        HashMap<Character,Character> map = new HashMap<>();

        ArrayDeque<Character> st = new ArrayDeque<>();

        for(int i = 0;i<s.length();i++){
            char curr = s.charAt(i);
            if(curr == '(' || curr == '{' || curr == '[')
                st.push(curr);
            else{
                if(st.isEmpty())
                    return false;
                else if(isMatch(st.peek(),curr) == false)
                    return false;
                else
                    st.pop();
            }
        }
        return st.isEmpty();
    }
}
```

### Implement two stacks in single array

```
import java.io.*;
import java.util.*;


class TwoStacks { 
    int cap; 
    int top1, top2; 
    int arr[]; 
  
    TwoStacks(int n) 
    { 
        arr = new int[n]; 
        cap = n; 
        top1 = -1; 
        top2 = cap; 
    } 
  
    void push1(int x) 
    { 
        if (top1 < top2 - 1) { 
            top1++; 
            arr[top1] = x; 
        } 
        else { 
            System.out.println("Stack Overflow"); 
            System.exit(1); 
        } 
    } 
  
    void push2(int x) 
    { 
        if (top1 < top2 - 1) { 
            top2--; 
            arr[top2] = x; 
        } 
        else { 
            System.out.println("Stack Overflow"); 
            System.exit(1); 
        } 
    } 
    
    int pop1() 
    { 
        if (top1 >= 0) { 
            int x = arr[top1]; 
            top1--; 
            return x; 
        } 
        else { 
            System.out.println("Stack Underflow"); 
            System.exit(1); 
        } 
        return 0; 
    } 
  
    int pop2() 
    { 
        if (top2 < cap) { 
            int x = arr[top2]; 
            top2++; 
            return x; 
        } 
        else { 
            System.out.println("Stack Underflow"); 
            System.exit(1); 
        } 
        return 0; 
    }
}

class GFG {
    
	public static void main (String[] args) {
	
	    TwoStacks ts=new TwoStacks(5); 
        ts.push1(5); 
        ts.push2(10); 
        ts.push2(15); 
        ts.push1(11); 
        ts.push2(7); 
        System.out.println("Popped element from stack1 is: " + ts.pop1()); 
        ts.push2(40); 
        System.out.println("Popped element from stack2 is: " + ts.pop2());  
	  
	}
	
}
```

### Implementation of K Stacks in an array

![Whats-App-Image-2023-10-09-at-13-59-59-d51142c9.jpg](https://i.postimg.cc/L8ptP48J/Whats-App-Image-2023-10-09-at-13-59-59-d51142c9.jpg "Explanation of Implementation of K stacks in an Array")

### Stock Span Problem

Stock span at the particular day is defined as the no of consecutive days before the current days where the price of that particular item is less than or equal to current price. 

```
void printSpan(int arr[],int n){
    Stack s;
    s.push(0);
    print(1);
    
    for(int i = 1;i<n;i++){
        while(s.isEmpty == false && arr[s.peek()] <= arr[i]){
            s.pop();
        }
        int span = s.isEmpty ? : i+1 : i-s.peek();
        print(span);
        s.push(i);
    }
}
```

**Working of this logic:**
Let's say we got previous greater elements as *prev* and current element is *curr*. And we consider the element that is greater than *prev* as *prev.prev*. Now, by processing for *curr*, we may pop out the previous elements that are smaller than *prev*. These elements won't be the answer for *curr* element. If the *curr* element is smaller than the *prev* element, then *prev* will be the answer and those deleted element won't be the answer as they are not closer to *curr*. If *curr* element is greater than *prev* element, in this case also deleted element won't be the answer, because they'll be even smaller than *prev*. *prev* itself is smaller compared to *curr* and those deleted element definitely not be greater element. We can check for next greater element that is greater than previous. This will be present in the array. 

All the elements are pushed into stack and popped out from stack. O(1) time for push and popping element and thus the time complexity is 2N. So the overall time complexity is O(N). 

