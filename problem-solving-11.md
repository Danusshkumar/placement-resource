> Problem Solving - 11

# LinkedList - II

## Doubly LinkedList in Java

```
class Main{
    public static void main(String[] args){
        Node head = new Node(10);
        Node temp1 = new Node(20);
        Node temp2 = new Node(30);
        head.next = temp1;
        temp1.prev = head;
        temp1.next = temp2;
        temp2.prev = temp1;
    }
}
```

## Advantages and Disadvantages of Doubly LinkedList

### Advantages

- Can be traversed in both the directions
- Delete a node in O(1) time with given reference or pointer to it.( we can copy the next node's data into current node and can delete next node but it's not the case in deleting the last node)
- Insert and delete before a given node is possible
- Insert and delete from both ends in O(1) time by maintaining tail. We can't delete the tail in O(1) in singly linkedlist.

### Disadvantages
- Extra space for `prev` pointer
- Code become more complex

>**Note:** Always note that insertion and delete is possible in the singly linkedlist only if the address of previous node is given


## Insert at begin in Doubly LinkedList

```
public static Node insertBegin(Node head, int data){
    Node temp = new Node(data);
    temp.next = head;
    if(head != null)
        head.prev = temp;
    return temp;
} // function call will be assigned to head
```

## Insert at end in Doubly LinkedList

```
public static Node insertEnd(Node head, int data){
    Node temp = new Node(data);
    if(head == null)
        return temp;
    Node curr = head;
    while(curr.next != null)
        curr = curr.next;
    curr.next = temp;
    temp.prev = curr;
    return head; 
}
```

## Reverse a Doubly LinkedList

```
public static Node reverse(Node head, int data){
    if(head == null || head.next == null) //when there is single node and no node
        return null;
    
    Node prev = null, curr = head;
    while(curr != null){
        prev = curr.prev;
        curr.prev = curr.next;
        curr.next = prev;
        // prev is a third variable for swapping next and prev
        curr = curr.prev; // curr = curr.next and now, our next is prev
    }
    return prev.prev; //prev is a second last node and prev.prev is the last node as now
    //prev node is the next node
}
```


## Delete Head of a Doubly LinkedList

```
public static Node delHead(Node head){
    if(head == null || head.next == null)
        return null;
    head = head.next;
    head.prev = null;
    return head;
}
```

## Delete Last of a Doubly LinkedList

```
public static Node delLast(Node head){
    if(head == null || head.next == null)
        return null;
    
    Node curr = head;
    while(curr.next.next != null)
        curr = curr.next;
    curr.next = null;
    /* or we can do like this (using the advantage of having Doubly LinkedList)
    while(curr.next != null)
        curr = curr.next;
    curr.prev.next = null;
    */
    return head;
}
```
Note that the last node still has its previous linked to the last node of our list but it doesn't matter at all and the last node will be collected by Garbage collector.


## Circular LinkedList in Java

```
public class Main{
    public static void main(String[] args){
        Node head = new Node(10);
        head.next = new Node(20);
        head.next.next = new Node(30);
        head.next.next.next = new Node(40);
        head.next.next.next.next = head;
    }
}
```

>**Note:** Empty circular LinkedList's head will be null. On circular LinkedList with only one node, the node's next will be itself.


## Advantages and Disadvantages of Circular LinkedList

- We can traverse whole LinkedList from anywhere
- Implementation of algorithm like Round robin
- we can insert at the beginning and end by just maintaining one tail reference/pointer.
- Disadvantage of this circular LinkedList is that implementation of operations become complex


## Traversal in Circular LinkedList

Method 1:
```
public static void printList(Node head){
    if(head == null)
        return;
    System.out.print(head.data + " ");
    for(Node curr = head.next;curr != head;curr = curr.next)
        System.out.print(curr.data + " ");
    
}
```

Method 2:
```
public static void printList(Node head){
    if(head == null)
        return;
    Node curr = head;
    do {
        System.out.print(curr.data + " ");
        curr = curr.next;
    } while(curr != head);
}
```

## Insert at beginning in Circular LinkedList

### Naive approach
```
Node insertBegin(Node head,int data){
    Node temp = new Node(data);
    if(head == null){
        temp.next = temp;
        return temp;
    }
    
    Node curr = head;
    while(curr.next != head){
        //found the last node
        temp.next = curr.next; //(or) temp.next = head;
        curr.next = temp;
    }
    return temp;
}
```

### Efficient approach

```
Node insertBegin(Node head, int data){
    Node temp = new Node(data);
    if(head == null){
        temp.next = temp;
        return temp;
    }
    temp.next = head.next;
    head.next = temp;
    //swapping data between second (new node) and head node
    int t = head.data;
    head.data = temp.data;
    temp.data = t;
    return head;
}
```

## Insert at end of the Circular LinkedList

### Naive approach
```
Node insertBegin(Node head,int data){
    Node temp = new Node(data);
    if(head == null){
        temp.next = temp;
        return temp;
    }
    
    Node curr = head;
    while(curr.next != head){
        //found the last node
        temp.next = head;
        curr.next = temp;
    }
    return temp;
}
```

### Efficient approach

```
Node insertBegin(Node head, int data){
    Node temp = new Node(data);
    if(head == null){
        temp.next = temp;
        return temp;
    }
    temp.next = head.next;
    head.next = temp;
    //swapping data between second (new node) and head node
    int t = head.data;
    head.data = temp.data;
    temp.data = t;
    return temp; // returning temp as a new head.
    // this return stmt is the only difference between insert at the beginning and
    //insert at the end in circular LinkedList
}
```

## Delete head of the Circular LinkedList

Naive approach
```
Node delHead(Node head){
    if(head == null || head.next == null) 
        return null;
    Node curr = head;
    while(curr.next != head)
        curr = curr.next;
    curr.next = head.next;
    return curr.next;
} // finding the last node and make next of last node to second node
```

Efficient approach
```
Node delHead(Node head){
    if(head == null || head.next == null)
        return null;
    head.data = head.next.data;
    head.next = head.next.next;
    return head;
}
//In this approach, we are copying the second node data to first node and we delete the
// first node. 
```
