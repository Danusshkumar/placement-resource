> Problem Solving - 12

# LinkedList - III

## Delete Kth Node from Circular LinkedList

```
Node deleteKth(Node head,int k){
    if(head == null)
        return null;
    if(k == 1)
        return deleteHead(head); 
        // delete head is the function that is used to delete
        // the head node. Refer problem solving 11 to know about deleteHead
        
    for(int i = 1;i<k-1;i++)
        curr = curr.next;
    /* Or we can use 0 as index as we do in arrays
    for(int i = 0;i<k-2;i++)
        curr = curr.next;
    */
    curr.next = curr.next.next;
    return head;
}
```

## Circular Doubly LinkedList

- Circular doubly linkedlist with no element will be `null` as the head
- Circular doubly linkedlist with single element will point it's next as itself and its previous as itself
- We get all advantage of Circular LinkedList and Doubly LinkedList in this Circular Doubly LinkedList
- Implementation of round robin algorithm, josephus problem, etc.
- We can access the lastnode in constant time without maintaining the tail reference.

Insert at head:
```
public static Node insertHead(Node head,int data){
    Node temp = new Node(data);
    if(head == null){
        temp.prev = temp;
        temp.next = temp;
        return temp;
    }
    
    temp.prev = head.prev;
    temp.next = head;
    head.prev.next = temp;
    head.prev = temp;
    return temp; // return head will make it as insertEnd
}
```

## Sorted Insert in a Singly Linked List

```
public static Node sortedInsert(Node head,int data){
    Node temp = new Node(data);
    if(head == null)
        return temp;
    if(x < head.data){
        temp.next = head;
        return temp;
    }
    
    Node curr = head;
    while(curr.next != null && curr.next.data < data)
        curr = curr.next;
    temp.next = curr.next;
    curr.next = temp;
    return head;
}// Time complexity : θ(pos) where pos is the position
```

## Middle of linked list

Naive approach
```
void printMiddle(Node head){
    if(head == null)
        return;
    int count = 0;
    Node curr;
    for(curr = head;curr != null;curr = curr.next)
        count++;
    curr = head;
    for(int i = 0;i<count/2;i++)
        curr = curr.next;
    System.out.print(curr.data);
}
```

Efficient approach: Refer [this](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-LinkedList/video/NjI1) video for further clarification
```
void printMiddle(Node head){
    if(head == null)
        return;
    Node slow = head, fast = head;
    while(fast != null && fast.next != null){
        slow = slow.next;
        fast = fast.next.next;
    }
    System.out.print(slow.data);
}
```

## Nth node from end of the LinkedList

Naive approach
```
void nThNode(Node head){
    int len = 0;
    for(Node curr = head;curr != null;curr = curr.next)
        len++;
    if(len < n)
        return;
    curr = head;
    for(int i = 1;i<len-n+1;i++)
        curr = curr.next;
    System.out.print(curr.data);
}
```

Efficient approach
```
void nThNode(Node head){
    Node first = head, second = head;
    for(int i = 0;i<n;i++){
        if(first == null)
            return;
        first = first.next;
    }
    
    while(first != null){
        first = first.next;
        second = second.next;
    }
    System.out.print(second.data);  
}
```

## Reverse the LinkedList (Iterative)

Naive approach
```

```

Algorithm of efficient approach
```
Copy first node in prevNode
Go to next node
copy next node to nextNode
Link current node to prevNode (next node broken) and make current node as prevNode
Go to next node using nextNode
Go to step 3 and repeat
```

```
Node reverseList(Node head){
    Node curr = head;
    Node prevNode = null;
    Node nextNode = null;
    while(curr != null){
        nextNode = curr.next; // saving next node
        curr.next = prevNode; // linking previous node
        prevNode = curr; // saving current node
        curr = nextNode; // moving to next node
    }
    return prevNode; //previous is our new head and curr is null
}
```

## Reverse the LinkedList (Recursive Method - 1)

```
Node reverseList(Node head){
    if(head == null || head.next == null)
        return head;
    Node res_head = reverseList(head.next);
    Node res_tail = head.next;
    res_tail.next = head;
    head.next = null;
    return res_head;
} // last n-1 node will be reversed and the nth node will be joined with it
```
Refer [this](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-LinkedList/video/NjI4) video for complete explanation


## Reverse the LinkedList (Recursive Method - 2)

```
Node reverseList(Node prev,Node curr){
    if(curr == null)
        return prev;
    Node next = curr.next;
    curr.next = prev;
    return reverseList(curr,next);
} //first n - 1 node will be reversed and the nth node will be joined with it
// we assumed that the function is called this way reverseList(head,null);
```
Refer [this](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-LinkedList/video/MTQ1MQ%3D%3D) video for complete explanation


## Remove duplicates from the sorted LinkedList

```
public ListNode deleteDuplicates(ListNode head) {
    if(head == null || head.next == null)
        return head;
    
    ListNode curr = head;
    while(curr != null && curr.next != null){
        if(curr.val == curr.next.val)
            curr.next = curr.next.next; // omitting middle node
        else
            curr = curr.next;
    }
    return head;
}
```

>**Note:** On traversing K nodes, and count for k nodes, count as it is from 0 to k - 1 or 1 to k. On reverse also do 0 to k - 1(i < k) because, we have also taken into account the modification of firstNode.next to null. While traversing for deletion, we have to traverse 0 to k-2 times or 1 to k-1 (i<k-1) because, we have to access k-1th node to delete kth node.

## Reverse a linked list in groups of size k

Refer [here](https://ide.geeksforgeeks.org/eRENkIyfW9) for iterative solution

Refer [here](https://ide.geeksforgeeks.org/fRSAiru1t3) for recursive solution


## Detect Loop

#### Algorithms
```
Algorithm 1:
We are traversing the LinkedList and while traversing we are checking whether curr.next
node is already present or not. while primary traversing occurs, we are using secondary
pointer that traverses from head pointer to the curr node and all the nodes that the
secondary pointer traversed are compared with curr.next for whether curr.next occured
previously or not.
This solution clearly has quadratic time complexity

Algorithm 2:
In this algorithm, we are changing the structure of the node. we are adding extra
parameter visited to the node structure. By traversal we are marking currNode as 
visited(boolean value to true) and if the node is already marked as visited, then 
there is a cycle. At that point, we break and return true (cycle exists)

Algorithm 3:
A dummyNode was created. we store the curr.next into nextNode and linked current node
to dummyNode (curr.next = dummyNode). we are doing this for everyNode as we traverse 
by the linkedList. If we reach the starting point of the loop, it'll linked to 
dummyNode and we'll finally reach the dummyNode. we will reach NULL if there is no 
loop. By this way, we can detect the loop. But this way would destroy the LinkedList
structure and the List can't be reconstructed.

Algorithm 4:
A set of node was created. While traversing the nodes are added to set. If we found,
current node present in the set, it was caught by traversal previously and added to 
set. Thus, loop exists. 
```

## Detect loop using floyd cycle detection

```
public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        while(fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;

            if(slow == fast){
                slow = head;
                while(slow != fast){
                    slow = slow.next;
                    fast = fast.next;
                }
                return slow;
            }
        }
        return null;
    }
}
```
Floyd's cycle detection algorithm was used here. Reach [here](https://youtube.com/watch?v=PvrxZaH_eZ4&list=LL&index=5&t=2s) to learn about floyd's cycle detection algorithm

## Delete node with only pointer given to it

Refer [this](https://leetcode.com/problems/delete-node-in-a-linked-list) LeetCode submission

## Segregate Even and Odd Nodes

```
// es - even start, ee - even end, os - odd start, oe - odd end
class Solution{
    Node divide(int N, Node head){
        Node es = null, ee = null, os = null, oe = null;
        
        for(Node curr = head;curr != null; curr = curr.next){
            int x = curr.data;
            if(x%2 == 0){
                if(es == null)
                    es = ee = curr;
                else{
                    ee.next = curr;
                    ee = ee.next;
                }
            }
            else{
                if(os == null)
                    os = oe = curr;
                else{
                    oe.next = curr;
                    oe = oe.next;
                }
            }
        }
        if(os == null || es == null)
                return head;
        
        ee.next = os;
        oe.next = null;
        return es;
    }
}
```
Reach out [here](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-LinkedList/video/NzAyNw%3D%3D) to understand the solution

## Intersection Point of two linked list

### Using HashSet

```
static int getIntersection(Node head1, Node head2)  { 
    HashSet<Node> s=new HashSet<>();
    Node curr=head1;
    while(curr!=null){
        s.add(curr);
        curr=curr.next;
    }
    curr=head2;
    while(curr!=null){
        if(s.contains(curr))
            return curr.data;
        curr=curr.next;
    }
    return -1;
} 
```

### Without using HashSet

Refer [this](https://leetcode.com/problems/intersection-of-two-linked-lists/) LeetCode submitted solution

## Pairwise Swap Nodes of linked list

```
class Solution {
    public ListNode swapPairs(ListNode head) {
        if(head == null || head.next == null)
            return head;
        ListNode curr = head.next.next;
        ListNode prevNode = head;
        head = head.next;
        head.next = prevNode;

        while(curr != null && curr.next != null){
            prevNode.next = curr.next;
            prevNode = curr;

            ListNode nextNode = curr.next.next;
            curr.next.next = curr;
            curr = nextNode;
        }
        prevNode.next = curr;
        return head;
    }
}
```

In this solution, we are manipulating with four pointers. In each iteration we do connect, `prev` with `curr.next` and `curr.next` with `curr` and `curr` with the element next to `curr.next`. Everytime we update `prev` and `curr` and the loop continues. Finally we manually connect the `prev` to `curr`. Note that the first pair itself explicitly handled as we want the head of this list (secondNode) 

LeetCode solution [here](https://leetcode.com/problems/swap-nodes-in-pairs/)

Can't able to understand ? Reach out the explanation in [this](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-LinkedList/video/NzAyOQ%3D%3D) video


## Clone a linked list with Random Pointer

### Super simple easy implementation using HashMap

```
class Solution {
    public Node copyRandomList(Node head) {
        HashMap<Node,Node> map = new HashMap<>();

        for(Node curr = head;curr != null; curr = curr.next)
            map.put(curr,new Node(curr.val));
        
        for(Node curr = head;curr != null;curr = curr.next){
            Node clone = map.get(curr);
            clone.next = map.get(curr.next);
            clone.random = map.get(curr.random);
        }
        
        return map.get(head);
    }
}
```

### Efficient approach that didn't use HashMap
```

class Solution {
    // see remaining submission for better implementation
    public Node copyRandomList(Node head) {
        if(head == null)
            return null;
        
        Node curr = head;
        while(curr != null){
            Node newNode = new Node(curr.val);
            Node nextNode = curr.next;
            curr.next = newNode;
            newNode.next = nextNode;
            curr = nextNode;
        }//insertion new nodes in between original nodes

        curr = head;
        while( curr != null){
            Node randomPoint = curr.random;
            curr.next.random = (randomPoint != null) ? randomPoint.next : null;
            curr = curr.next.next;
        }

        Node cloneHead = head.next;
        Node clone = cloneHead;
        for(Node current = head;current != null;current = current.next){
            current.next = current.next.next;
            clone.next = (clone.next != null) ? clone.next.next : null;
            clone = clone.next;
        }
        // we are preserving original list as it is required.

        return cloneHead;
    }
}
```
Explanation [here](https://practice.geeksforgeeks.org/batch/dsa-4/track/DSASP-LinkedList/video/MTU5MzU%3D)

for Further topics, **LRU Cache Design, Merge two sorted linkedlists and Palindrome LinkedList**, refer the course itself.
