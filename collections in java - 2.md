> Collections in Java - 2
# Java List Interface

## List Interface in Java

- List in Java provides the facility to maintain the ordered collection. It contains the index-based methods to insert, update, delete and search the elements. It can have the duplicate elements also.
- We can also store the null elements in the list.
- List interface is found in `java.util` package and it implements Collection interface.
- Implementation class for List interface are  `ArrayList`,`LinkedList`,`Stack`, and `Vector`. 

> **Note:** *Vector class is deprecated since Java 5*.

#### Advantages of using List to create ArrayList and LinkedList

- The advantage of creating ArrayList from List is that it allows you to use the polymorphism feature of Java. Polymorphism means that an object can have different forms or behaviors depending on the context. 
- By creating an ArrayList from List, you are declaring a variable of type List, but assigning it an object of type ArrayList. This means that you can use the same variable to refer to different types of lists, such as LinkedList, Vector, Stack, etc., as long as they implement the List interface.
- We can use the same method to manipulate with ArrayList and LinkedList and no individual elements are required. It's also an example of polymorphism.
- This gives you more flexibility and reusability in your code.

```
ArrayList<Integer> ls = new ArrayList<>();
LinkedList<Integer> linkedList = new LinkedList<>();
ls = linkedList;
// It will generate compile-time error
// error: incompatible types: LinkedList cannot be converted to ArrayList

List<Integer> ls = new ArrayList<>();
LinkedList<Integer> linkedList = new LinkedList<>();
ls = linkedList;
// works fine as the ArrayList is declared as List

```

```
public static void printList(List<Integer> ls){
    for(Integer i : ls){
        System.out.print(i + " ");
    }
}
public static void main(String[] args) {
    List<Integer> list = Arrays.asList(1,2,3);
	List<Integer> ls = new ArrayList<>(list);
	List<Integer> linkedList = new LinkedList<>(list);
	printList(ls);
	printList(linkedList);
}
```

#### How to create List

```
List<String> ls = new ArrayList<>();
List<Integer> ls = new ArrayList<>();
List<Book> ls  new ArrayList<>();
List<Animal> ls = new LinkedList<>();

```

#### How to convert List from arrays

> Only ways to convert an array(already declared as variable) into the List is to
add all the elements in the array to List by using loops

```
int arr[] = {1,2,3,4,5};
List<Integer> ls = new ArrayList<>();
for(int element : arr)
    ls.add(element);
```

#### How to convert arrays from List

```
 List<String> fruitList = new ArrayList<>();    
 fruitList.add("Mango");    
 fruitList.add("Banana");    
 fruitList.add("Apple");    
 fruitList.add("Strawberry");    
 //Converting ArrayList to Array  
 String[] array = fruitList.toArray(new String[fruitList.size()]);    
 System.out.println("Printing Array: "+Arrays.toString(array));  
 System.out.println("Printing List: "+fruitList);  
```

***

> Why  `new String[fruitList.size()]` is passed as an argument to the method `.toArray()` ?

The toArray method of ArrayList is used to convert the ArrayList object into an array object of the same type. However, due to the way generics are implemented in Java, there is no way to create a generic array at runtime. Generics are a compile-time feature that allows you to write generic code that can work with different types of objects. However, at runtime, the generic type information is erased by the compiler, and all generic types are replaced by Object, the common superclass of all classes in Java.

This means that if you try to create an array of a generic type, such as T[], the compiler will not know what T is at runtime, and will create an array of Object instead. For example, if you have an ArrayList<String> and you try to call toArray() without any argument, you will get an Object[] instead of a String[]. This will cause a ClassCastException if you try to assign it to a String[] variable.

To avoid this problem, you need to pass an array of the desired type as an argument to the toArray method. This way, the compiler can use the array’s runtime type as a hint to create an array of the same type as the argument. For example, if you pass a String[] array as an argument to toArray, the compiler will create a String[] array and copy the elements from the ArrayList to it.

However, you do not need to pass a pre-sized array as an argument to toArray. You can pass an empty array instead, such as new String[0]. The toArray method will check the size of the argument array and create a new array of the same type and size as the ArrayList if the argument array is too small. This may be more efficient than passing a pre-sized array, as it avoids creating an extra array that is not needed.

Therefore, the recommended way to convert an ArrayList<String> to a String[] is:

String[] array = fruitList.toArray(new String[0]);

This will create a new String[] array with the same size and elements as fruitList.

Still we can't get the array of `int`. We can only get the array of `Integer`.

***

#### How to sort the List

There are various ways to sort the List, here we are going to use Collections.sort() method to sort the list element. The java.util package provides a utility class Collections which has the static method sort(). Using the `Collections.sort()` method, we can easily sort any List.




## ArrayList in Java

ArrayList is a Class that is found in `java.util.Collection`

We can import ArrayList by `import java.util.Collection` or `import java.util.*`

![ArrayList Hierarchy](https://static.javatpoint.com/images/arraylist.png "ArrayList Hierarchy")

Wrapper class is used for all the elements in java as wrappper class supports some of the features that ArrayList class wants

```
ArrayList<int> al = ArrayList<int>(); // does not work  
ArrayList<Integer> al = new ArrayList<Integer>(); // works fine
```
### Constructor

```
ArrayList<Integer> list = new ArrayList<>(); // empty array list
ArrayList<Integer> list = new ArrayList<>(int); //ArrayList with specified capacity
List<Integer> arr = Arrays.asList(1,2,3);
ArrayList<Integer> list = new ArrayList<>(arr);
```

### Methods


- `add(int index,int element)` -  add element at specified index
- `add(int element)` - add element to the end
- `addAll(int index,Collection collection)` - add collection at specified index
- `addAll(Collection collection)` - add collection to the end
- `get(int index)` - return element at specified index
- `lastIndexOf(int element)` - returns the index of last occurence of the element 
and returns -1 if element not found
- `toArray()` - returns the collection as arrays
- `E remove(int index)` - used to remove the element present at the specified position in the list.
- `boolean remove(Object o)` - used to remove the first occurrence of the specified element.
- `removeRange(int startIndex,int endIndex)` - removes the element at that range
- `Object clone()` - returns the shallow copy of the ArrayList
- `set(int index,int element)` - used to replace the `element` at the `index`
- `size()` - will return the size of the ArrayList
- `sort()` - used to sort the ArrayList in ascending order
- `trimToSize(int size)` - trims the ArrayList to the specified size

> **Note:** *Above are the list of methods that are specific to ArrayList class (generic method may also be found) but Other methods that are discussed in the Collection interface will be found in ArrayList. Also note that  important methods of ArrayList only discussed here. It's not the complete list of methods*


### Generics vs Non-generics

- Java collections are non-generic before JDK 1.5. Since 1.5, it's generic
- Java collections stores only one type of objects in a collection and hence, no typecasting is required in runtime
- `ArrayList list = new ArrayList();` - non-generic ArrayList (not supported now)
- `ArrayList<Integer> list = new ArrayList<>();` - Generic ArrayList

### Iterators

We can iterate the ArrayList with iterator
```
 Iterator itr=list.iterator();//getting the Iterator
 while(itr.hasNext()){ // itr.hasNext() - checks if the next element is present or not 
   System.out.println(itr.next());// itr.next() - returns the current element and moves to next
  }  
```

### Six ways to iterate Collections in Java

1. Iterator interface.
2. for-each loop.
3. ListIterator interface.
4. for loop.
5. forEach() method.
6. forEachRemaining() method.

## LinkedList in Java

![LinkedList hierarchy](https://static.javatpoint.com/images/linkedlist.png "LinkedList Hierarchy")

- Java LinkedList class uses a doubly linked list to store the elements. It inherits the AbstractList class and implements List and Deque interfaces.
- It maintains insertion order.
- Manipulation is faster than ArrayList as no shifting is needed
- Java LinkedList can be used as List, Stack or Queue

### Constructor

```
LinkedList<Integer> linkedList = new LinkedList<>(); //empty linked list

List<Integer> list = Arrays.asList(1,2,3);
LinkedList<Integer> linkedList = new LinkedList<>(list); // linked list with specified element

```

### Methods in LinkedList

-  `add(int element), add(int index,int element), addAll(Collection collection)
, addAll(int index, Collection collection),` are found in LinkedList
- `addFirst(int element)` - Adds element at the beginning of the linked list
- `addLast(int element` - Appends the element at the end of the linked list
- `Object clone()` - returns the shallow copy of the LinkedList
- `contains(int element)` - returns boolean whether the element is present in linkedlist or not 
- `element()` - Used to get the first element of the linkedlist
- `get(int index), getFirst(), getLast(), indexOf(int element), lastIndexOf(int element), ` - are also found in LinkedList (accessing by index is also possible in linkedlist. 
*Note: indexOf() returns the index of first occurrence of tat element but lastIndexOf() will return the index of last occurrence of that element*
- `set(int index,int element)` - set the `element` at the `index`.
- `toArray()` - returns the LinkedList as array

> **Note:** *Above are the list of methods that are specific to LinkedList class (generic method may also be found) but Other methods that are discussed in the Collection interface will be found in LinkedList. Also note that  important methods of LinkedList only discussed here. It's not the complete list of methods*

## ArrayList vs LinkedList


><br> All the methods that are found in ArrayList are almost found in LinkedList. All the methods that are found in LinkedList is almost found in ArrayList. Then what's the difference between ArrayList and LinkedList in Java ?<br><br>

| ArrayList | LinkedList
| --- | --- |
| ArrayList internally uses dynamic array to store elements | LinkedList internally uses doubly linked list to store the elements |
| Manipulation is slow as it internally uses array and shifting is required when deletion occurs | Manpulation is faster as it uses linked list where no shifting is required for manipulation |
| It can act as list only as it's an implementation of List |It can act as list, stack and queue as it's an implementation of List and Deque interfaces |
| Better for storing and accessing data | Better for manipulation data |
| Memory is contiguous | Memory is non-contiguous |
| Default size is 10 when the array list is initialised | No default size as it is a doubly linked list |
| To be precise, it's an resizable array | It's an exact implementation of doubly linked list |


### Where to use ArrayList and LinkedList ?
- When the rate of addition or removal rate is more than the read scenarios, then go for the LinkedList. On the other hand, when the frequency of the read scenarios is more than the addition or removal rate, then ArrayList takes precedence over LinkedList.
- Since the elements of an ArrayList are stored more compact as compared to a LinkedList; therefore, the ArrayList is more cache-friendly as compared to the LinkedList. Thus, chances for the cache miss are less in an ArrayList as compared to a LinkedList. Generally, it is considered that a LinkedList is poor in cache-locality.
- Memory overhead in the LinkedList is more as compared to the ArrayList. It is because, in a LinkedList, we have two extra links (next and previous) as it is required to store the address of the previous and the next nodes, and these links consume extra space. Such links are not present in an ArrayList.
