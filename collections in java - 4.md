> Collections in Java - 4

# Java Queue, Priority Queue, Deque and ArrayDeque

![Hierarchy of Collection](https://static.javatpoint.com/images/java-collection-hierarchy.png "Hierarchy of Collection")

## Java Queue

Queue is an interface in java (available in java.util package) and it extends the Collection interface. It is used to keep the elements that are processed in First In First Out (FIFO) manner. It's an ordered list of objects where the insertion occurs at end of the list and deletion(removal) occurs at the beginning of the list.

Being an interface, Queue is implemented by LinkedList and PriorityQueue. LinkedList implements both List and Queue, so if we can use LinkedList as List, Queue and Stack. But PriorityQueue implements only Queue interface so it's designed only for implementing Queue data structure. 

## Methods - Java Queue Interface

- `boolean add()` - adds the element into queue and return true upon success
- `boolean offer()` - adds the element into the queue and return true upon success
- `Object remove()` - used to retrieve and remove the head of queue
- `Object poll()` - used to retrieve and remove the head of queue, return null if queue is empty
- `Object element()` - used to retrieves, but does not remove, the head of this queue
- `Object peek()` - used to retrieves, but does not remove, the head of this queue and returns null if the queue is empty

> **What's the difference between `.add()` and `.offer()` ?**<br>
`.add()` methods adds the element if the queue is not full. But when the queue has a capacity limit and it is full, it will throw `IllegalStateException`. but `.offer()` method will return false if the queue is full. Therefore, the offer method is generally preferable when using a capacity-restricted queue, as it allows you to handle the failure gracefully.



## Features of Queue

Queue supports all its unique methods and also supports the methods that are general for all collections. But using general methods (methods defined in Collection class) is not suggested to use with Queues. For example, we can get the random access of elements in Collection using `.get()` method. But it's not possible in Queue. If you try to do so, you may get UnsupportedOperationException or an incorrect result.

- As discussed earlier, FIFO concept is used for insertion and deletion of elements from a queue.
- PriorityQueue, LinkedList, ArrayBlockingQueue are the implementations that are used frequently
- Deque supports insertion and removal of elements from the both side so with Deque we can build both Stack and Queue data structure. Note that Deque implements Queue only and doesn't implement Stack interface which is subclass of vector
- The stack interface is considered deprecated and should be replaced by the deque interface for better performance and quality

## PriorityQueue

Other than doing insertion and removal operations ( Queue function ), it also do another work that is arranging the elements of the queue based on certain priority. Priority queue uses a comparison function (Comparator) and with that function the element will be arranged as soon as it is inserted into the PriorityQueue. 

### Constructor 

```
PriorityQueue<String> queue = new PriorityQueue<>();
Queue<String> queue_2 = new PriorityQueue<>();
```

#### How to use Comparator in PriorityQueue ?

```
import java.util.*;

class Main {
    public static void main(String[] args) {
        Comparator<String> comp = new Comparator<String>(){
            @Override
            public int compare(String s1,String s2){
                return s1.compareTo(s2);
            }
        };
        PriorityQueue<String> queue = new PriorityQueue<>(comp);
        queue.add("Hello");
        queue.add("Danusshkumar");
        queue.add("Java");
        queue.add("CPP");
        System.out.println(queue);
    }
}

Output : 

[CPP, Danusshkumar, Java, Hello]
```

## Deque

The interface Deque is present in java.util package. Deque extends the Queue interface and supports addtion and removal of element on both the sides. Thus, it can be used as both Stack or Queue. Stack is Last In First Out (LIFO) based and Queue is First In First Out based. As Deque supports both, either of the mentioned operation can be performed in it. Deque is an acronym of **Double Ended Queue**


## Methods

- `add()`,`offer()`,`remove()`,`poll()`,`element()`,`peek()` are the methods that are found in Queue. It's also found in Deque
- `peekFirst()` - returns the head element of the deque, returns null if deque is empty
- `peekLas()` - returns the last element of the deque, returns null if deque is empty
- `offerFirst(E e)` - inserts element at the front of deque and returns true upon success
- `offerLast(E e)` - inserts element at the end of deque and returns true upon success

## ArrayDeque

It's not possible to create object for interface and that's why we need a class to implement Deque. It's ArrayDeque. It grows and shinks per usage. It also inherits AbstractCollection class.

![Hierarchy of ArrayDeque](https://static.javatpoint.com/java/collection/images/arraydeque.png "Hierarchy of ArrayDeque")

- We can add or remove elements from both the sides
- Null elements are not allowed
- No capacity restrictions
- Faster than LinkedList and Stack

```
import java.util.*;

class Main {
    public static void main(String[] args) {
        Deque<String> deque = new ArrayDeque<>();
        deque.offer("Hello"); // adds element at start
        deque.offerLast("Hello world"); //adds element at end
        deque.poll(); //remove element at start
        deque.pollLast(); //remove element at end
        System.out.println(deque);
    }
}

Output : []
```


