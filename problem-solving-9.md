> Problem Solving - 9

# Hashing

## Introduction to Hashing

- No duplicates allowed
- Search, Insertion, Delete will take O(1) on average


Let's consider the time complexity of Array.

#### Sorted array:
- Search: O(logn)
- Insertion: O(n) (for shifting process - right shifting)
- Deletion: O(n) (for shifting process - left shifting)

#### Unsorted array:
- Search: O(n)
- Insertion: O(1) (no position based insertion. only appending)
- Deletion: O(n) (for shifting process - left shifing and to find the element)

- For search operation, ultimately in sorted array form, we are going to get O(logn) time complexity. This will be comparatively high with O(1) if n value is too high. Thus, hashing provides searching in O(1) time complexity. 
- In AVL tree or Red-black tree we will get the values just above the given key or below the given key, but in hashing the searching is strict and results only if the key is present or not present.
- Hashing will be good if we doesn't care about closest values or sorted order. It even not good at **prefix searching**.
- Prefix search is searching the string with prefixes of that string. Learn [here](https://sl.bing.net/ipgtNvDSSvQ) more about prefix search.

## Applications of Hashing

1. Dictionaries
2. Database indexing
3. Cryptography
4. Caches
5. Symbol tables in compilers/interpreters
6. Routers
7. Getting data from database and <br>
many more ...
<br><br>
- Dictionaries in languages are implemented using Hashes.
- Primary and secondary indexing. These indexing are implemented with B or B+ tree (or) it can be implemented with Hashing.
- When signup for first time, the password is hashed and stored in the database and next time, we login, the hash is again computed and check for match with previously stored match. If they are equal, we are allowed to enter. 
- Hashes are used in browser caches. The URL will and the data associated wih that URL will be stored as key value pairs in the browser cache. Everytime, we visit the website, the data will be searched in cache for availability and if found, then the data in the cache will be returned. 
- Symbol tables in compilers/interpreter. Symbol tables are hashtables for variable names and corresponding values. The variable names and values are stored in symbol table and when called with variable names, variable value will be returned and if not found, undefined name "varaible name" error will be thrown.
- Simple problems like MAC address for an IP address in routing is actually done using hashing. 
- Getting data from database : When we query a single row from a database, the data will be retrived as associative arrays or maps or dictionaries. With those arrays, we can get the name on that query using res["name"], age using res["age"], and etc. These associative arrays are nothing but hashes. **Wherever the map (or) dictionaries like data structure exists, hashing is working behind the scenes**

## Hashing functions

- The main purpose of the hashing is to take Universe of keys as an input and convert those
input into the values that ranges from 0 to m - 1 where m is the size of our hashtable (array). Here Universe of keys include phone numbers that have 10 digits, strings, αnumerical values, decimal values, etc.
- The hash function should take O(1) time for numbers and O(len) for strings where "len" is the length of strings. 
- Our hash functions should uniformly distribute the large keys into Hash Tables slots. 

#### Some examples of hash functions

```
h(large_key) = large_key%m
here the value 'm' will be the prime number that is close to the table size. If the
m value is even number like 2 (or) 4 (or) powers of 10 like 10, 100, 1000, then we are
going to consider only last 2 to 3 digits of the information for hashing which is not
a good practice. 
```

```
for str[] = "abcd",
```
str[0]*x<sup>0</sup> + str[1]*x<sup>1</sup> + str[2]*x<sup>2</sup>
The above hash function is better than the sum of ascii values because, when we consider the sum of ascii values as our hash function, all the permutation of the string "abcd" will only points to the single index. The value "bbbd" also have same ASCII value. By the above hash function (weighted sum), we can avoid the problem of having permutations.

#### Uniform Hash functions
In this, there will be some group of hash function where we can choose one hash function from those hash function randomly. In this way, we can avoid having some pattern of inputs that can lead to collisions. we can't find patterns of input that will lead to collisions. 


## Collision handing

**Birthday paradox** states that "if there are 23 people in a room, then there is 50% of probability that two people from 23 have same birthday". If the no.of peoples are 70, then the probability will reach upto, 99.9%. And if the room has 257 people, then the probability of having 2 people sharing a one birthday will reach 100%. <br>
This paradox explains how serious the collision problem is. 


If we know the keys in advance, then we can do **perfect hashing** which guarantees 100% no collisions. If we want to store the values of known english words in dictionaries, then we would do some preprocessing to get that perfect hashing that requires no collisions at all. 

1. Chaining
2. Open Addressing
 - Linear probing
 - Quadratic probing
 - Double hashing
 

### Chaining
 
Let's make the assumption that the hash functions and keys are given in such a way that hash function generates unique hash for all different keys. Under these assumption, 

```
m = no. of slots in the hash table
n = no. of keys to be inserted
Load factor (α) = n/m
Expected chain length = α
Expected search time = O(1 + α) (1 - for hash computation)
Expected insertion, deletion time = O(1 + α) (1 - for hash computation)

If m = n and our assumption uniform distribution is true, then we will achieve O(1)
search time, insertion time and deletion time
```

- There are some disadvantages using LinkedList for chaining. It is not cache friendly, it requires extra space for storing next and previous references. time complexity for search is O(l) where 'l' is the length of the linked list
- Dynamic sized arrays : Time complexity is same as linked list but it is cache friendly and the elements are located in contiguous locations.
- Self Balancing BSTs : In this self-balancing BSTs, searching.insertion and deletion becomes O(logl) where 'l' is the chain length. From Java 8, they started using Self balancing BST's for HashMap.

##### Implementing Hashing with Chaining 

```
import java.util.*;


public class Main
{
	public static void main(String[] args) {
	    Scanner sc = new Scanner(System.in);
	    MyHash hash = new MyHash(10);
	    while(true){
	        System.out.print("1 - insert, 2 - delete, 3 - search, 4 - exit: ");
	        int input = sc.nextInt();
	        if(input == 1){
	            System.out.print("key : ");
	            int key = sc.nextInt();
	            hash.insert(key);
	        }
	        else if(input == 2){
	            System.out.print("key : ");
	            int key = sc.nextInt();
	            hash.delete(key);
	        }
	        else if(input == 3){
	            System.out.print("key : ");
	            int key = sc.nextInt();
	            hash.search(key);
	        }
	        else if(input == 4){
	            break;
	        }
	    }
	}
}


class MyHash {
    int BUCKET;
    ArrayList<LinkedList<Integer>> table;
    
    MyHash(int size){
        BUCKET = size;
        table = new ArrayList<LinkedList<Integer>>();
        for(int i = 0;i<BUCKET;i++)
            table.add(new LinkedList<Integer>());
    }
    
    void insert(int key){
        int i = key%BUCKET;
        table.get(i).add(key);
    }
    
    void delete(int key){
        int i = key%BUCKET;
        table.get(i).remove((Integer) key);
    }
    
    void search(int key){
        int i = key%BUCKET;
        Boolean isPresent = table.get(i).contains(key);
        System.out.println(isPresent);
    }
}

```

### Open addressing

In this technique, if collision occured, then we linearly go to the next slot where we can find the empty slot. Consider by doing this, we inserted element continuously to k slots (contiguously) and the cluster is formed. Now, if any new key is inserted in any of these k position, the cluster's size will increase by one. The probabily of increasing the size of cluster is equal to the size of cluster itself (k). If k is k+1, then the next key is inserted for any of those k positions, then collision will occur and the cluster will be increases as k+2. This will create a primary cluster


Inorder to avoid this primary cluster, we go to quadratic probing where we go to i<sup>2</sup>th position when we find a collision. This also leads to cluster ( secondary cluster) as all the elements that forms under same slots follows the same procedure. But the secondary cluster is not as bad as primary clusters. **But there is one more problem with quadratic probing. There is an possibility that quadratic probing won't find an empty slot even though, there is some empty slot. It's mathematically proven that quadratic probing will definitely find the empty slot if our load factor(α < 0.5) (half of the table will be free) and the value of m(size of table) in (n/m) is an prime number. Without those condition satisfied, quadratic probing may won't find empty slots even if they are present.** There is one more method which solves these problems. It's called [double hashing](#double-hashing)

On doing probing, we do not simply make the slot empty while deleting. It will lead to the problem while searching the inserting element. We have to mark the slot as deleted when we want to delete one element. 

### Double hashing

Cache performance of chaining is not good because when we traverse a Linked List, we are basically jumping from one node to another, all across the computer’s memory. For this reason, the CPU cannot cache the nodes which aren’t visited yet, this doesn’t help us. But with Open Addressing, data isn’t spread, so if the CPU detects that a segment of memory is constantly being accessed, it gets cached for quick access.

Like Chaining, the performance of hashing can be evaluated under the assumption that each key is equally likely to be hashed to any slot of the table (simple uniform hashing) Refer the video [here](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-Hashing/video/MTAxMA%3D%3D) for better understanding. It's recommended to watch videos inorder to get better idea for second hash function. 
```
m = Number of slots in the hash table

n = Number of keys to be inserted in the hash table

 Load factor (α) = n/m  ( < 1 )

Expected time to search/insert/delete < 1/(1 – α) 

So Search, Insert and Delete take (1/(1 – α)) time
```

### Implementation of Open Addressing

You can find the source code for implementation for open addressing in [here](https://onlinegdb.com/-Cm0LQh3b) (my version) and [here](https://ide.geeksforgeeks.org/OeTSY5boeF) (gfg version).

In those implementations, the empty node is marked as -1 and deleted node is marked as -2. But in real libraries implementations, all the keys are pointers and references to the original keys. So the empty node is represented using null pointer. The deleted node is represented using dummy node. Dummy node is a node that is declared intentionally for this purpose globally. This dummy node is fixed and the every time we check deleted node, we actually check this dummy node. 


##### Chaining vs Open addressing
We can go for open addressing if we know the number of keys in advance and we have lot much space available.Otherwise, then go for chaining which is a better version of collision handling when compared with open addressing.

```
TC on chaining = O(1+α)
TC on open addressing = O(1/1-α)
```

### Unordered set and Unordered maps in C++ STL
Refer those videos [here](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-Hashing/video/MTAxMw%3D%3D) and [here](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-Hashing/video/MTAxNA%3D%3D) and it's not neccessary.

### HashSet and HashMap in Java

```
HashSet<String> h = new HashSet<String>(); 

h.add("gfg"); 
h.add("courses"); 
h.add("ide"); 

System.out.println(h);

System.out.println(h.contains("ide"));

Iterator<String> i = h.iterator();

while(i.hasNext())
    System.out.print(i.next()+" ");

```
- `h.iterator()` will return the iterator for the hashset. 
- `i.hasNext()` will return true if next element is present or not
- `i.next()` will return the current element in the iterator

```
HashSet<String> h = new HashSet<String>(); 

h.add("gfg"); 
h.add("courses"); 
h.add("ide"); 

System.out.println(h.size());

h.remove("ide");
System.out.println(h.size());

for(String s: h)
    System.out.print(s+" ");

System.out.println("\n"+h.isEmpty());

```
- `h.size()` will return the size of the hashset
- `h.isEmpty()` will return the boolean whether the set is empty or not
- `h.add()` will add the item and upon successful insertion, it returns true
- `h.remove(item)` will remove the item from the hashset
- `h.clear()` will clear all the elements in the hashset
- `h.contains(item)` will search the element `item` in the set. Returns true if found and returns false if not found

##### HashMap in Java

```
// Create an empty hash map 
HashMap<String, Integer> m  = new HashMap<>(); 

// Add elements to the map 
m.put("gfg", 10); 
m.put("ide", 15); 
m.put("courses", 20); 

// Print size and content
System.out.println(m); 
System.out.println(m.size()); 

// Iterating over HashMap 
for(Map.Entry<String, Integer>e : m.entrySet())
    System.out.println(e.getKey() + " " + e.getValue());
```

```
// Create an empty hash map 
HashMap<String, Integer> m = new HashMap<>(); 

// Add elements to the map 
m.put("gfg", 10); 
m.put("ide", 15); 
m.put("courses", 20); 

// Check for a key
if (m.containsKey("ide")) 
    System.out.println("Yes");
else
    System.out.println("No");

// Remove key "ide"
// and returns the associated value 15
m.remove("ide");
System.out.println(m.size());
```

```
// Create an empty hash map 
HashMap<String, Integer> m = new HashMap<>(); 

// Add elements to the map 
m.put("gfg", 10); 
m.put("ide", 15); 
m.put("courses", 20); 

// Check for a Value
if (m.containsValue(15)) 
    System.out.println("Yes");
else
    System.out.println("No");

// Get value corresponding to passed key
// <"ide", 15>
System.out.println(m.get("ide"));

// The given key is absent
System.out.println(m.get("practice"));
```

### Problems on Hashing

1. [Count Distinct Elements](https://ide.geeksforgeeks.org/CooDfdjqJT)
2. [Frequencies of array elements](https://ide.geeksforgeeks.org/KRCCdWyrGE)
3. [Intersection of two unsorted arrays](https://ide.geeksforgeeks.org/online-java-compiler/8a4405a1-1b63-47c3-9e15-3fa256fdb949)
4. [Union of two unsorted arrays](https://ide.geeksforgeeks.org/locSRd1N1E)
5. [Pair with given sum in unsorted array](https://ide.geeksforgeeks.org/RCaWHWNMwb)
6. [Subarray with zero sum](https://ide.geeksforgeeks.org/TigCyNxtq8)
7. [Subarray with given sum](https://ide.geeksforgeeks.org/fcdfe123-9c4f-4086-91b9-2c7575e7bdf4)
8. [Longest subarray with given sum](https://ide.geeksforgeeks.org/2475dbd2-9249-4cab-bb6f-12af0651ff4e)
9. [Longest subarray with equal number of 0's and 1's](https://ide.geeksforgeeks.org/zGKWhsJMMw)
10. [Longest Consecutive subsequence](https://ide.geeksforgeeks.org/yg6Tn16iq9)
11. [Count Distinct element in every window](https://practice.geeksforgeeks.org/problems/count-distinct-elements-in-every-window/1)
12. [More than n/k occurences]()
