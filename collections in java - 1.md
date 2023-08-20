> Collections in Java - 1

# Introduction to Collections in Java 

Java Collections is a framework where we can find architecture to store and manipulate the objects or data

With Java Collections, we can achieve almost all types of operation that involved data manipulations such as 
- searching
- sorting
- insertion
- manipulation
- deletion

## Collections

Collection means single unit of objects, a group.
Java Collections is really a collection, a collection of many classes and interfaces.
Common classes and interfaces, we can find in this collection framework are

### Interfaces
- Set
- List
- Queue
- Deque

### Classes
- ArrayList
- Vector
- LinkedList
- PriorityQueue
- HashSet
- LinkedHashSet
- TreeSet

## Hierarchy of Collection framework

![Hierarchy of Collection framework](https://static.javatpoint.com/images/java-collection-hierarchy.png)

Collection Interface has following methods. All classess implementing this Collection interface will have all of the methods that are defined in Collections interface.
That means for all types of classes, the method remains same. Because all those classes are implemented by this Collections interface.

### Methods in Collection Interface:

- add - Adds element to the collection and return true if successfully added
- addAll - Gets collections as a parameter and add all elements to specified collection. Returns true if successfully done
- remove - Removes element from collection and returns true if successfully done
- removeAll - Gets collections as a parameter and remove all elements from specified collection. Returns true if successfully done
- removelf - Removes or deletes element from collection based on specified Predicate (Predicate is a object which is like a function that takes one agrument as input
  and return boolean) and returns boolean
- retainAll - retain all the element that matches with the elements in the collections that is passed as parameter (intersection) and returns boolean
- size - returns the number of element present in collection
- clear - Removes all the elements from the collections
- contains - Checks whether the given element is present in collection or not and returns boolean
- containsAll - Used to search specified collection in the collection and returns boolean
- iterator - Returns the iterator
- toArray - Converts the collection into array and return the array
- isEmpty - Checks whether the collection is empty or not and returns boolean
- parallelStream
- stream
- spliterator
- equals - Matches two collections and returns the boolean
- hashCode - Returns the hashCode number of the collection

  > **Note:**  *Most of the above method will return boolean. As Java, is the object based programming language, even array( new int[5] ) is also an object,
  > there is nothing called call by value and all the operations are directly performed to the object (collection) itself. No new modified objects will be returned.
  > In languages like Python, some methods will modify the object and return the new object, so we have to assign the modified object to original old
  >  object inorder to make the original object modified*





