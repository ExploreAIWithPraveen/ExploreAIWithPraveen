### **Appendix 5: The Linked List Data Structure 🔗**

### **👨‍🍳 The Stacker 5000\'s Next-of-Kin: The Caterer\'s Train**

After we conquered the challenges of queues and heaps, our restaurant\'s
efficiency was unmatched. Word of our systems spread, and a major
catering company, \"The Gourmet Express,\" asked for our help. Their
problem was simple but maddening: they had to prepare meals in a
specific order, but they were often interrupted by new, urgent orders
that needed to be inserted right in the middle of their production line.
Adding an order meant physically shifting every tray after it, causing a
domino effect of chaos. It was like trying to get in line at a packed
movie theater and forcing everyone behind you to take a step back.

\"We need a flexible system,\" their head caterer said. \"One where we
can add a new meal, a new \'link,\' anywhere we want, without having to
move everything else.\"

This was a job for a new kind of data structure. Instead of a rigid
array, we proposed a \"Caterer\'s Train.\" Each tray, or \"car,\" in
this train was linked to the one in front of it and the one behind it.
We started with a single tray, our \"engine\" or **head**. When a new
order came in, we\'d simply unhitch two cars, insert the new one, and
link it to its new neighbors. The orders were all connected, but they
didn\'t have to be physically next to each other in a continuous block
of memory.

To add a new meal: We would create a new tray and find the right place
to link it into our train. This is called insertion.

To remove a meal: We would simply unhitch a tray from the train, and
link its former neighbors to each other. This is called deletion.

This system had one core principle: **flexible connections**. Each
element, or **node**, only needed to know where the next element was. It
brought an elegant simplicity to their complex workflow, allowing them
to adapt to new requests without disruption.

### **🧠 The Core Concepts of a Linked List**

A **Linked List** is a linear data structure where elements are not
stored at contiguous memory locations. Instead, each element, called a
**node**, stores a reference (or pointer) to the next element in the
sequence.

This structure gives linked lists their incredible flexibility for
insertions and deletions. Unlike an array, you don\'t need to resize or
shift elements. You just need to update a few pointers.

There are several types of linked lists:

- **Singly Linked List**: Each node has a value and a next pointer,
  pointing to the next node in the sequence. The last node\'s next
  pointer is null.

- **Doubly Linked List**: Each node has a value, a next pointer, and a
  previous pointer, allowing for traversal in both directions.

- **Circular Linked List**: The last node\'s pointer points back to the
  first node, forming a loop.

The main operations of a Linked List are:

- **Insertion**: Adds a new node at a specific position (beginning, end,
  or middle).

- **Deletion**: Removes a node from a specific position.

- **Traversal**: Moves through the list from one node to the next.

Linked lists are a powerful data structure because their flexible,
non-contiguous nature makes them perfect for problems where the size of
the data is unpredictable or where frequent insertions and deletions are
required.

### **C# Templates: The Blueprints for a Linked List**

C# has a built-in LinkedList\<T\> class, but it\'s crucial to understand
the underlying structure. An efficient SinglyLinkedList implementation
involves a Node class and a head pointer.

C#

public class Node\<T\>

{

public T Value { get; set; }

public Node\<T\> Next { get; set; }

public Node(T value)

{

Value = value;

Next = null;

}

}

public class SinglyLinkedList\<T\>

{

private Node\<T\> head;

public SinglyLinkedList()

{

head = null;

}

// Inserts a new node at the beginning of the list.

// Time Complexity: O(1)

public void AddFirst(T value)

{

Node\<T\> newNode = new Node\<T\>(value);

newNode.Next = head;

head = newNode;

}

// Deletes the first node in the list.

// Time Complexity: O(1)

public void RemoveFirst()

{

if (head == null)

{

throw new InvalidOperationException(\"List is empty.\");

}

head = head.Next;

}

// Finds the first node with the specified value.

// Time Complexity: O(n)

public Node\<T\> Find(T value)

{

Node\<T\> current = head;

while (current != null)

{

if (current.Value.Equals(value))

{

return current;

}

current = current.Next;

}

return null;

}

}

### **💻 Do-It-Yourself Exercises: Singly Linked List**

#### **Beginner**

Solved Problem: Count Nodes in a Linked List

Problem: Given the head of a singly linked list, return the number of
nodes in the list.

Solution:

The most intuitive way to solve this is to traverse the list from the
head, incrementing a counter until you reach the end (a null node).

C#

public class ListCounter

{

public int CountNodes(Node\<int\> head)

{

int count = 0;

Node\<int\> current = head;

while (current != null)

{

count++;

current = current.Next;

}

return count;

}

}

Reverse a Linked List: Given the head of a singly linked list, reverse
the list and return the new head.

Hint: You\'ll need to keep track of three pointers: current, previous,
and next.

#### **Intermediate**

Detect a Cycle: Given the head of a linked list, determine if the list
has a cycle.

Hint: Use two pointers, one moving faster than the other. If they ever
meet, a cycle exists. This is known as Floyd\'s Tortoise and Hare
algorithm.

#### **Expert**

Merge Two Sorted Linked Lists: Given the heads of two sorted linked
lists, merge them into a single sorted list.

Hint: This can be done recursively or iteratively. In the iterative
approach, you\'ll need to manage pointers to the current nodes of both
lists and the tail of the new merged list.

### **🍴 A New Tool: The Doubly Linked List**

The \"Caterer\'s Train\" worked beautifully, but the chefs ran into a
new problem. They would occasionally need to grab an ingredient from the
tray *behind* them. With a singly linked list, this meant they had to go
all the way back to the start of the train and traverse through every
tray again to find the one they needed. It was like a one-way street;
there was no way to reverse.

To solve this, Steve proposed a \"Two-Way Caterer\'s Train,\" a **Doubly
Linked List**. In this version, each node not only had a pointer to the
*next* tray but also to the *previous* one. This allowed the chefs to
move forward and backward through the line with equal ease.

The operations for a Doubly Linked List are similar to a singly linked
list, but they are often more efficient for certain tasks. For example,
adding or removing a node from the middle is much faster since you can
access the previous node directly without a full traversal.

- **Node**: Each node contains a value, a next pointer, and a previous
  pointer.

- **Insertion**: When a new node is inserted, both its next and previous
  pointers, as well as the pointers of its neighbors, must be updated.

- **Deletion**: Removing a node involves linking its previous node
  directly to its next node.

This simple addition brought a new level of flexibility to the
caterer\'s operation, turning a one-way street into a two-way highway.

### **C# Templates: The Blueprints for a Doubly Linked List**

A DoublyLinkedList requires a more complex Node class that includes a
Previous pointer. It also needs to manage a head and a tail pointer for
efficient access to both ends of the list.

C#

public class DoublyNode\<T\>

{

public T Value { get; set; }

public DoublyNode\<T\> Next { get; set; }

public DoublyNode\<T\> Previous { get; set; }

public DoublyNode(T value)

{

Value = value;

Next = null;

Previous = null;

}

}

public class DoublyLinkedList\<T\>

{

private DoublyNode\<T\> head;

private DoublyNode\<T\> tail;

// Adds a new node to the end of the list.

// Time Complexity: O(1)

public void AddLast(T value)

{

DoublyNode\<T\> newNode = new DoublyNode\<T\>(value);

if (head == null)

{

head = newNode;

tail = newNode;

}

else

{

tail.Next = newNode;

newNode.Previous = tail;

tail = newNode;

}

}

// Removes a specified node from the list.

// Time Complexity: O(1) if the node is provided, O(n) to find it

public void Remove(DoublyNode\<T\> nodeToRemove)

{

if (nodeToRemove.Previous != null)

{

nodeToRemove.Previous.Next = nodeToRemove.Next;

}

else

{

head = nodeToRemove.Next;

}

if (nodeToRemove.Next != null)

{

nodeToRemove.Next.Previous = nodeToRemove.Previous;

}

else

{

tail = nodeToRemove.Previous;

}

}

}

### **💻 Do-It-Yourself Exercises: Doubly Linked List**

#### **Beginner**

Solved Problem: Add to the Front of a Doubly Linked List

Problem: Implement a method to add a new node to the beginning of a
doubly linked list.

Solution:

Adding a new node to the front of a doubly linked list is a constant
time operation (O(1)). We simply create the new node, set its Next
pointer to the current head, update the old head\'s Previous pointer to
the new node, and finally, update the list\'s head to point to the new
node. We must also handle the case where the list is empty.

C#

public void AddFirst(T value)

{

DoublyNode\<T\> newNode = new DoublyNode\<T\>(value);

if (head == null)

{

head = newNode;

tail = newNode;

}

else

{

newNode.Next = head;

head.Previous = newNode;

head = newNode;

}

}

Find and Remove a Node: Implement a method that finds a node with a
given value and removes it.

Hint: Traverse the list. When you find the node, you\'ll need to update
the next pointer of its previous node and the previous pointer of its
next node.

#### **Intermediate**

Reverse a Doubly Linked List: Implement a function to reverse a doubly
linked list.

Hint: You can reverse the list by swapping the next and previous
pointers for each node during a single traversal.

#### **Expert**

LRU Cache Implementation: Implement a Least Recently Used (LRU) cache.

Hint: An LRU cache is often implemented using a hash map for fast
lookups and a doubly linked list to track the order of usage, allowing
for O(1) time complexity for insertion and removal.

### **🔄 A Continuous Cycle: The Circular Linked List**

Just when we thought we had solved every possible problem, The Gourmet
Express started a new project: a conveyor belt of food trays for a
buffet-style event. The trays would move in a continuous loop, coming
back to the start after a full revolution. The head caterer needed a way
to model this \"never-ending\" line of food.

This was a perfect use case for a **Circular Linked List**. Unlike a
standard linked list, the last node\'s next pointer points back to the
first node, creating a continuous loop. There\'s no null at the end, and
no distinct \"end\" to the list.

This structure is ideal for applications where you need to cycle through
items, such as a **round-robin** task scheduler in an operating system,
or a music playlist that loops endlessly.

- **Node**: The structure is the same as a singly linked list.

- **Circular Property**: The next pointer of the last node points to the
  head. This makes next of the last node to be a pointer to the head,
  creating a loop.

- **Insertion/Deletion**: Operations are similar to a singly linked
  list, but you must be careful to handle the circular connection,
  especially when adding or removing the first or last node.

### **C# Templates: The Blueprints for a Circular Linked List**

A CircularLinkedList can be implemented using a singly linked list with
one key modification: the next pointer of the tail node points to the
head node.

C#

public class CircularLinkedList\<T\>

{

private Node\<T\> head;

// Inserts a new node at the end of the circular list.

// Time Complexity: O(n)

public void AddLast(T value)

{

Node\<T\> newNode = new Node\<T\>(value);

if (head == null)

{

head = newNode;

newNode.Next = head; // Point back to itself

}

else

{

Node\<T\> current = head;

while (current.Next != head)

{

current = current.Next;

}

current.Next = newNode;

newNode.Next = head;

}

}

// Removes a node with a specific value.

// Time Complexity: O(n)

public void Remove(T value)

{

if (head == null) return;

if (head.Value.Equals(value) && head.Next == head)

{

head = null;

return;

}

Node\<T\> current = head;

Node\<T\> previous = null;

do

{

if (current.Value.Equals(value))

{

if (previous != null)

{

previous.Next = current.Next;

if (current == head)

{

// Update head if the removed node was the head

head = current.Next;

}

}

else

{

// If removing the head, find the last node and update its next pointer

Node\<T\> last = head;

while (last.Next != head)

{

last = last.Next;

}

head = current.Next;

last.Next = head;

}

return;

}

previous = current;

current = current.Next;

} while (current != head);

}

}

### **💻 Do-It-Yourself Exercises: Circular Linked List**

#### **Beginner**

Solved Problem: Check if a Circular List is Empty

Problem: Implement a method that checks if a circular linked list is
empty.

Solution:

A circular linked list is empty if its head pointer is null. A simple
check is all that\'s required.

C#

public bool IsEmpty()

{

return head == null;

}

Traverse and Print: Implement a method that traverses the circular
linked list and prints the value of each node.

Hint: Use a do-while loop to ensure you iterate at least once and stop
when you return to the head.

#### **Intermediate**

Split a Circular Linked List: Given a circular linked list, split it
into two halves.

Hint: Use two pointers, one moving twice as fast as the other, to find
the middle of the list.

#### **Expert**

Josephus Problem: Implement a solution to the Josephus Problem using a
circular linked list.

Hint: The problem describes a group of people in a circle where every
kth person is eliminated until only one remains. A circular linked list
is the ideal data structure to simulate this scenario.
