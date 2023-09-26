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
input into the values that ranges from 0 to m - 1 where m is the size of our hashtable (array). Here Universe of keys include phone numbers that have 10 digits, strings, alphanumerical values, decimal values, etc.
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
 
Let's make the assumption that the hash functions and keys are given in such a way that hash function generates unique hash for all different keys. Under these assumption, 

```
m = no. of slots in the hash table
n = no. of keys to be inserted
Load factor (alpha) = n/m
Expected chain length = alpha
Expected search time = O(1 + alpha) (1 - for hash computation)
Expected insertion, deletion time = O(1 + alpha) (1 - for hash computation)

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


Inorder to avoid this primary cluster, we go to quadratic probing where we go to i<sup>2</sup>th position when we find a collision. This also leads to cluster ( secondary cluster) as all the elements that forms under same slots follows the same procedure. But the secondary cluster is not as bad as primary clusters. **But there is one more problem with quadratic probing. There is an possibility that quadratic probing won't find an empty slot even though, there is some empty slot. It's mathematically proven that quadratic probing will definitely find the empty slot if our load factor(alpha < 0.5) (half of the table will be free) and the value of m(size of table) in (n/m) is an prime number. Without those condition satisfied, quadratic probing may won't find empty slots even if they are present.** There is one more method which solves these problems. It's called [double hashing](#implementing-hashing-with-chaining)

On doing probing, we do not simply make the slot empty while deleting. It will lead to the problem while searching the inserting element. We have to mark the slot as deleted when we want to delete one element. 

### Double hashing
