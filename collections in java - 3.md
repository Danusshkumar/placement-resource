> Collections in Java - 3

# Java HashSet, LinkedHashSet and TreeSet

## Java HashSet

![Heirarchy of HashSet](https://static.javatpoint.com/images/hashset.png "Hierarchy of HashSet")

- HashSet stores the element by hashing
- Duplicate values are not allowed and null values are allowed (null value is allowed only once
- Doesn't maintain insertion order as it internally works with hash table
- HashSet is a best approach for search operation
- Initial default capacity of HashSet is 16 (Hashtable with size 16) and the load factor is 0.75

*Before learning further about HashSet, let's learn about hashtable and working of hashtable*

***
> What is Load factor ?

Load factor is a term that is used to measure the performance of a hash table or a hash map, which are data structures that store key-value pairs. A hash table or a hash map uses a hash function to map each key to an index of an array, where the corresponding value is stored. However, sometimes, different keys may have the same hash value, which leads to a collision. A collision occurs when two or more key-value pairs are mapped to the same index of the array. To resolve collisions, there are different methods, such as chaining or linear probing.

The load factor of a hash table or a hash map is defined as the ratio of the number of elements (key-value pairs) stored in the table to the size of the array (the number of buckets or slots). The load factor indicates how full the table is, and how likely it is to have collisions. A low load factor means that the table is mostly empty, and there are fewer chances of collisions. A high load factor means that the table is almost full, and there are more chances of collisions.

The load factor affects the performance of the hash table or the hash map in terms of search, insert, and delete operations. A low load factor may result in faster search and insert operations, but it also wastes space and memory. A high load factor may result in slower search and insert operations, due to more collisions and longer chains or probes. Therefore, there is a trade-off between space and time efficiency when choosing the load factor.

To maintain a balance between space and time efficiency, most implementations of hash tables or hash maps use a dynamic resizing technique, which means that they increase or decrease the size of the array according to the load factor. For example, in Java, the HashMap class has a default initial capacity of 16 buckets and a default load factor of 0.75. This means that when the number of elements in the HashMap reaches 12 (75% of 16), the capacity of the array is doubled to 32 buckets, and all the elements are rehashed to fit into the new array. This process is called rehashing, and it helps to reduce collisions and improve performance.

> Internal working of ArrayList and LinkedList

ArrayList and LinkedList have other factors that affect their performance, such as capacity and size. Capacity is the number of elements that an ArrayList or a LinkedList can hold without resizing its internal data structure. Size is the number of elements that are actually stored in an ArrayList or a LinkedList. Capacity and size are related, but not the same.

For example, an ArrayList has an initial capacity of 10 elements, but it can be empty or have less than 10 elements. When an ArrayList reaches its capacity and needs to store more elements, it will create a new array with a larger capacity and copy all the existing elements to the new array. This process is called resizing, and it can affect the performance of adding or removing elements from an ArrayList.

Similarly, a LinkedList has no fixed capacity, but it has a size that reflects the number of elements stored in it. A LinkedList does not need to resize its internal data structure, because it uses nodes that are linked by pointers. However, a LinkedList may use more memory than an ArrayList, because each node has an overhead of storing two pointers.

Therefore, when choosing between ArrayList and LinkedList, you should consider the trade-offs between space and time efficiency, and the frequency of different operations on the list.


> key, value, index and hashCode (or) hashValue


- A key is an object that is used to identify or access a value in a hash table. A key can be any type of object that implements the hashCode() and equals() methods, which are used to compare keys for equality and generate hash codes for them. For example, in a HashMap, you can use a String object as a key to store and retrieve a value associated with it.

- A value is an object that is stored in a hash table along with its corresponding key. A value can be any type of object that you want to store in the hash table. For example, in a HashMap, you can use an Integer object as a value to store and retrieve along with its key.
- An index is an integer value that represents the position or location of an element in an array. An array is a data structure that stores multiple elements in a contiguous memory space. Each element in an array has a unique index that starts from zero and goes up to the length of the array minus one. For example, in an array of size 10, the first element has an index of 0 and the last element has an index of 9.
- A hashValue (or) hashCode is an integer value that is generated by applying a hash function to an object. A hash function is a mathematical function that takes an object as input and produces an integer as output. The purpose of a hash function is to map objects of different types and sizes to integers of a fixed range, such as 0 to 15. A good hash function should produce different hash values for different objects with high probability, and avoid collisions or conflicts between objects that have the same hash value. For example, in Java, every object has a hashCode() method that returns its hash value.


A HashSet is a data structure that implements the Set interface, which is a collection of unique elements. A HashSet does not store key-value pairs, but only values. However, internally, a HashSet uses a HashMap to store its elements. It uses the values as keys and a dummy object as values in the HashMap. The dummy object is a constant variable that has no meaning or significance. It is just used to fill the value slot in the HashMap. Therefore, when you add or remove an element from a HashSet, it actually adds or removes the element as a key from the underlying HashMap.

> Hash function used in Java

The hash function that is used in HashMap in Java is not exactly `key%sizeOfHashTable`, 
but it is similar. The actual hash function that is used in HashMap in Java is:

**`hash = (key.hashCode() ^ (key.hashCode() >>> 16)) & (sizeOfHashTable - 1)`**


This means that:

- The hashCode() method of the key object is called to obtain its initial hash value.
- The initial hash value is then XORed with itself right-shifted by 16 bits. 
This is done to reduce collisions for keys that have similar lower bits.
- The result of the XOR operation is then ANDed with sizeOfHashTable - 1. 
This is done to ensure that the final hash value is within the range of 0 to sizeOfHashTable - 1.
- This hash function is designed to provide a good distribution of keys across the array, and reduce collisions and performance degradation.

> **Note:** We can't use same keys on HashMap as it overrides the newly added value to the old key-value pair with the same key

>The hashtable is inserted with the number 100 numbers with the range (1 to 100). What's the probability of having O(n) Time complexity for searching an element in same hash table ?

We can calculate the probability of having O(n) time complexity for searching an element in that HashMap. To do that, we need to use the formula for the probability of collision in a hash table, which is:

```Probability (collision (T, M)) = 1 - 2 n! / (2 kn (2 n - k)!)```

where T is the number of unique hash values, M is the number of elements, and n is the number of bits.

In our case, T = 128, M = 100, and n = 7 (because 128 = 2^7).

Plugging these values into the formula, we get:

```Probability (collision (128, 100)) = 1 - 2^7! / (2^700 (2^7 - 100)!)```


Using Wolfram Alpha, we can enter the expression and get the result:

**```Probability (collision (128, 100))= 0.999999999999999999999999999999999999999999999999999999999999999998```**

This means that the probability of having O(n) time complexity for searching an element in that HashMap is almost 1, which means it is almost certain to happen.

This is because the hash function that is used in HashMap in Java is not very good at handling small integer keys, as it produces many collisions for them. Also, the load factor of the HashMap is too high, as it exceeds the recommended threshold of 0.75.

Therefore, using HashMap with 100 numbers with range (1 to 100 ) as keys and some arbitrary values as values is not a good idea, as it will result in poor performance and high probability of collisions.

***

## Constructors

- `HashSet()` - used to constructor empty HashSet with initial capacity as 16 and load factor as 0.75
- `HashSet(int capacity)` - used to construct HashSet with specified capacity
- `HashSet(int capacity, float loadFactor)` - used to construct HashSet with specified capacity and load factor
- `HashSet(Collection collection)` - used to construct HashSet with values present in collections

## Methods

- `add()` - adds an element to HashSet
- `addAll(Collection collection)` - adds all the elements in the `collection` to HashSet
- `clear()` - removes all the element from HashSet
- `clone()` - returns the shallow copy of the HashSet instance
- `contains(int element)` - returns boolean whether the element is present or not
- `isEmpty()` - returns whether the HashSet is empty or not
- `iterator()` - returns iterator for HashSet
- `remove(int element)` - removes the element from HashSet
-  `retainAll(Collection collection)` - removes the element that are not in `collection`(as like as intersection)
- `size()` - returns the size of the HashSet

> **Note:** We can print all the Collections using output statement and no need to print the element individually. We can also print the array using output statement by converting the arrays to string using `arr.toString()` method where `arr` is the array which is converted into string


***

## Java LinkedHashSet

- Java LinkedHashSet class contains unique elements only like HashSet
- Java LinkedHashSet class provides all optional set operations and permits null elements
- Java LinkedHashSet class maintains insertion order

>**Note:** Keeping the insertion order in the LinkedHashset has some additional costs, both in terms of extra memory and extra CPU cycles. Therefore, if it is not required to maintain the insertion order, go for the lighter-weight HashMap or the HashSet instead.

![Hierarchy of LinkedHashSet](https://static.javatpoint.com/images/linkedhashset.png "Hierarchy of LinkedHashSet")

## Constructors

- `LinkedHashSet()` - initialise LinkedHashSet with initial capacity as 16
- `LinkedHashSet(Collection collection)` - initialise LinkedHashSet with all the elements that are present in `collection`
- `LinkedHashSet(int capacity)` - initialise the LinkedHashSet with capacity as `capacity`
- `LinkedHashSet(int capacity, float fillRatio)` -used to initialize both the capacity and the fill ratio (also called load capacity) of the hash set from its argument.


> All the methods in Java HashSet (all optional set operations) are also present in LinkedHashSet


## Java TreeSet

Java TreeSet class implements the Set interface that uses a tree for storage. It inherits AbstractSet class and implements the NavigableSet interface. The objects of the TreeSet class are stored in ascending order.

![Hierarchy of TreeSet](https://static.javatpoint.com/images/treeset.png "Hierarchy of TreeSet")


- Duplicates are not allowed as it's one type of set
- access and retrieval is quiet fast
- Null element is not allowed
- maintains insertion order

TreeSet is being implemented using a binary search tree, which is self-balancing just like a Red-Black Tree. Therefore, operations such as a search, remove, and add consume O(log(N)) time. The reason behind this is there in the self-balancing tree. It is there to ensure that the tree height never exceeds O(log(N)) for all of the mentioned operations. Therefore, it is one of the efficient data structures in order to keep the large data that is sorted and also to do operations on it.

## Constructor

- `TreeSet()` - used to initialise the empty TreeSet
- `TreeSet(Collection collection)` - used to initialise a TreeSet with the elements that are present inside `collection`
- `TreeSet(Comparator comparator)` - used to initialise a TreeSet that will be sorted according to the `comparator`
- `TreeSet(SortedSet set)` - used to initiliase a TreeSet that contains the element of given  `set`

### Comparator

- We can create our custom Comparator definition as Comaparator is a interface in Java. It can compare two objects and return integer according to the comparison. We can also use those comparators to sort the array using `Collections.sort(arr,comparator)`

Comparator is implemented by the concept called anonymous inner class. In Java, we have the feature to define the class inside another class. This feature is called Nested class and the class defined inside the OuterClass is called inner class.
There are five types of inner classes in Java

1. Member Inner class
2. Anonymous Inner class
3. Local Inner class
4. Static nested class
5. Nested Interface

##### Member Inner class

In this type, the class is defined as member inside another class.

```
import java.util.*;

public class Main
{
    
	public static void main(String[] args) {
		Outer outer = new Outer();
		Outer.Inner inner = outer.new Inner();
		inner.print();
	}
}

class Outer {
    class Inner {
        public void print(){
            System.out.println("Inner class");
        }
    }
}
```

##### Anonymous Inner class

Anonymous inner class is a special type of inner class. It's not actually an inner class but it's an class which implements the outer class anonymously. This inner class won't have any name but named at runtime.

```
import java.util.*;


interface Outer {
    public void print();
}

public class Main
{
    
	public static void main(String[] args) {
		Outer outer = new Outer(){
		    @Override
		    public void print(){
		        System.out.println("Anonymous inner class");
		    }
		};
		
		outer.print();
	}
}
```

The above code is equivalent as creating an class `Anonymous` that implements or extends the outer class Outer and creating a object of `Anonymous` class with  `Outer` object type. But in the above code (anonymous inner class), we didn't have to create a named class (`Anonymous`), as it is created by default. This anonymous inner class is used when one-time inheritance of any abstract class or implementation of interface is needed.

```
import java.util.*;

public class Main
{
    
	public static void main(String[] args) {
		Outer outer = new Anonymous();
		outer.print();
	}
}

interface Outer {
    public void print();
}

class Anonymous implements Outer {
    @Override
    public void print(){
        System.out.println("Anonymous inner class");
    }
}
```

By this feature of anonymous inner class, Comparator is implemented.

#### Implementation of Comparator

```
import java.util.*;

public class Main
{
	public static void main(String[] args) {
		String[] arr = {"Java","C","CPP","Python"};
		Comparator<String> comp = new Comparator<String>(){
		    @Override
		    public int compare(String s1,String s2){
		        return s1.compareTo(s2);
		    }
		};
		Arrays.sort(arr,comp);
		System.out.println(Arrays.toString(arr));
	}
}
```

## Methods - Java TreeSet

- `add(Object element)` - adds the `element` to the TreeSet
- `addAll(Collection collection)` - adds all the element that are present inside `collection`
- `ceil(Object element)` - returns the equal or closest greatest element of the specified element from the set and returns null if there is no such element exists
- `floor(Object element)` - returns the equal or closest least element of the specified element from the set and returns null if there is no such element exists
- `higher(Object element)` - returns the closest greatest element of the specified element from the set and returns null if there is no such element exists
- `lower(Object element)` - returns the closes least element of the specified element from the set and returns null if there is no such element exists
- `comparator()` - returns the comparator of the TreeSet
- `descendingSet()` - returns the set in reverse order
- `headSet(Object element)` - returns the set of elements that are less than the specified element
- `tailSet(Object element)` - returns the set of elements that are greater than the specified element
- `pollFirst()` - used to retrieve and remove the lowest(first) element. Note that first element is always the lowest element as TreeSet is sorted in ascending order
- `pollLast()` - used to retrieve and remove the largest(last) element. Note that lasst element is always the largest element as TreeSet is sorted in ascending order
- `subSet(E fromElement, Boolean fromInclusive,E toElement,Boolean toInclusive)` - returns the subset from `fromElement` to `toElement`. fromElement and toElement may or may not be included that depends on the Boolean `fromInclusive` and `toInclusive` respectively
- `subSet(E fromElement,E toElement)` - returns subset from `fromElement` to `toElement` excluding `toElement`
- `first()`, `last()` - used to retrieve first and last element of the TreeSet respectively
- `contains(E element)`,`isEmpty()`,`remove(E element)`,`clear()`,`clone()`,`size()` are also found in TreeSet
