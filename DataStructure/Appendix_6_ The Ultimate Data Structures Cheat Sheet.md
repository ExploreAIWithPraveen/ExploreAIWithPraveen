### **Appendix 6: The Ultimate Data Structures Cheat Sheet 🥇**

### **👨‍🍳 The Grand Finale: The Master Chef\'s Toolkit**

After months of working with Steve, my understanding of the
restaurant\'s inner workings had become a masterclass in efficiency. We
had tackled every challenge, from the chaos of stacked dishes to the
complexities of prioritized orders and the flexibility of our caterer\'s
train.

One day, Steve handed me a brand-new apron. \"You\'ve earned this,\" he
said. \"You now have the knowledge to pick the right tool for any job,
no matter how big the kitchen gets. This is the master chef\'s
toolkit.\"

He explained that while each data structure was powerful in its own
right, the true skill lay in knowing which one was the most efficient
for a given task. Some problems looked simple but had hidden
complexities that only a specific data structure could solve elegantly.
This \"cheat sheet\" was our final project, a guide to choosing the best
tool for the job, especially when dealing with a massive number of
orders, ingredients, and customers.

We didn\'t just need a solution; we needed the *most efficient*
solution. This chapter is that guide, a final lesson in picking the
right data structure for the right problem, ensuring our kitchen can
handle anything, even a million-dollar catering order.

### **📚 The Comparative Study: Picking the Right Tool**

Each of the problems we\'ve encountered can be solved using different
data structures, but only one is the most efficient. This section
analyzes the exercises from our previous chapters, providing the optimal
solution and a brief explanation of why it\'s the best choice for large
datasets.

#### **1. Reversing a String 🔄**

- **Problem:** Given a string, reverse it.

- **Optimal Data Structure:** **Stack**

- **Why it\'s Efficient:** The LIFO (Last-In, First-Out) nature of a
  stack is a perfect match for string reversal. You push each character
  onto the stack and then pop them off. The first character pushed is
  the last one popped, effectively reversing the order. This is a
  simple, elegant, and highly efficient solution.

C#

using System.Collections.Generic;

using System.Text;

public class StringReverser

{

public string Reverse(string s)

{

Stack\<char\> stack = new Stack\<char\>();

foreach (char c in s)

{

stack.Push(c);

}

StringBuilder reversedString = new StringBuilder();

while (stack.Count \> 0)

{

reversedString.Append(stack.Pop());

}

return reversedString.ToString();

}

}

#### **2. Implementing a Queue using Stacks 🔄**

- **Problem:** Implement a FIFO queue data structure using two LIFO
  stacks.

- **Optimal Data Structure:** **Queue**

- **Why it\'s a Trick Question:** While this is a classic interview
  problem to test your understanding of data structures, the most
  efficient implementation of a queue is, well, a queue itself,
  specifically one built on a **doubly linked list** or a **circular
  array**. Using two stacks adds unnecessary complexity and overhead,
  making it less efficient for a real-world scenario with large
  datasets. The purpose of this problem is to show that a
  less-than-ideal tool can be forced to do a job, but it\'s not the best
  practice.

C#

using System.Collections.Generic;

public class EfficientQueue\<T\>

{

private LinkedList\<T\> items = new LinkedList\<T\>();

// Time Complexity: O(1)

public void Enqueue(T item)

{

items.AddLast(item);

}

// Time Complexity: O(1)

public T Dequeue()

{

if (items.Count == 0)

{

throw new InvalidOperationException(\"Queue is empty.\");

}

T item = items.First.Value;

items.RemoveFirst();

return item;

}

}

#### **3. Task Scheduler ⏳**

- **Problem:** You have a list of tasks with priorities. Implement a
  task scheduler that processes tasks based on their priority.

- **Optimal Data Structure:** **Priority Queue (Heap)**

- **Why it\'s Efficient:** A **Max-Heap** is the most efficient way to
  implement a priority queue. It provides O(log n) time complexity for
  both Enqueue (inserting a task) and Dequeue (processing the highest
  priority task). This is far superior to an unsorted list (O(n) for
  finding the max) or a sorted list (O(n) for insertion).

C#

using System;

using System.Collections.Generic;

public class MaxHeap\<T\> where T : IComparable\<T\>

{

private List\<T\> items = new List\<T\>();

// Time Complexity: O(log n)

public void Insert(T item)

{

items.Add(item);

int currentIndex = items.Count - 1;

while (currentIndex \> 0)

{

int parentIndex = (currentIndex - 1) / 2;

if (items\[currentIndex\].CompareTo(items\[parentIndex\]) \<= 0)

{

break;

}

T temp = items\[currentIndex\];

items\[currentIndex\] = items\[parentIndex\];

items\[parentIndex\] = temp;

currentIndex = parentIndex;

}

}

// Time Complexity: O(log n)

public T ExtractMax()

{

if (items.Count == 0)

{

throw new InvalidOperationException(\"Heap is empty.\");

}

T maxItem = items\[0\];

int lastIndex = items.Count - 1;

items\[0\] = items\[lastIndex\];

items.RemoveAt(lastIndex);

HeapifyDown(0);

return maxItem;

}

private void HeapifyDown(int index)

{

int largest = index;

int leftChild = 2 \* index + 1;

int rightChild = 2 \* index + 2;

if (leftChild \< items.Count &&
items\[leftChild\].CompareTo(items\[largest\]) \> 0)

{

largest = leftChild;

}

if (rightChild \< items.Count &&
items\[rightChild\].CompareTo(items\[largest\]) \> 0)

{

largest = rightChild;

}

if (largest != index)

{

T temp = items\[index\];

items\[index\] = items\[largest\];

items\[largest\] = temp;

HeapifyDown(largest);

}

}

}

#### **4. Fixed-Size Message Buffer ✉️**

- **Problem:** Implement a message buffer that can hold a fixed number
  of messages. When the buffer is full and a new message arrives, the
  oldest message should be overwritten.

- **Optimal Data Structure:** **Circular Queue**

- **Why it\'s Efficient:** A circular queue implemented with a
  fixed-size array provides the most efficient solution. Both Enqueue
  and Dequeue operations are performed in **O(1)** time. This is perfect
  for a fixed-size buffer, as it eliminates the need to shift elements,
  which would be a costly O(n) operation in a standard array-based
  queue.

C#

using System;

public class CircularQueue\<T\>

{

private T\[\] items;

private int front;

private int rear;

private int count;

private int capacity;

public CircularQueue(int capacity)

{

this.capacity = capacity;

items = new T\[capacity\];

front = 0;

rear = -1;

count = 0;

}

// Time Complexity: O(1)

public void Enqueue(T item)

{

if (IsFull())

{

throw new InvalidOperationException(\"Queue is full.\");

}

rear = (rear + 1) % capacity;

items\[rear\] = item;

count++;

}

// Time Complexity: O(1)

public T Dequeue()

{

if (IsEmpty())

{

throw new InvalidOperationException(\"Queue is empty.\");

}

T item = items\[front\];

front = (front + 1) % capacity;

count\--;

return item;

}

public bool IsEmpty()

{

return count == 0;

}

public bool IsFull()

{

return count == capacity;

}

}

#### **5. Counting Nodes in a Linked List 🔢**

- **Problem:** Given the head of a singly linked list, return the number
  of nodes in the list.

- **Optimal Data Structure:** **Singly Linked List**

- **Why it\'s a Foundational Problem:** The problem itself is a test of
  traversing a linked list. The most efficient way to count the nodes is
  to traverse the list from the head to the tail, a process that takes
  **O(n)** time. An array-based list would have a constant-time Count
  property, but the purpose of this exercise is to understand the
  fundamental traversal of a linked list.

C#

using System;

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

public class ListCounter

{

// Time Complexity: O(n)

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

#### **6. Adding to the Front of a Doubly Linked List ➡️**

- **Problem:** Implement a method to add a new node to the beginning of
  a doubly linked list.

- **Optimal Data Structure:** **Doubly Linked List**

- **Why it\'s Efficient:** Adding to the front of a **doubly linked
  list** is an **O(1)** operation. Unlike a singly linked list where you
  might have to find the previous node (if you were adding to the end),
  the head pointer gives you direct access. The Previous pointer in the
  doubly linked list makes updating the original head\'s pointer to the
  new node a simple, constant-time step.

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

// Time Complexity: O(1)

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

}

#### **7. Checking if a Circular List is Empty ∅**

- **Problem:** Implement a method that checks if a circular linked list
  is empty.

- **Optimal Data Structure:** **Circular Linked List**

- **Why it\'s Efficient:** A **circular linked list** provides a
  constant-time **O(1)** solution to this problem. You simply check if
  the head pointer is null. This is the most efficient way, as there\'s
  no need to traverse the list.

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

public class CircularLinkedList\<T\>

{

private Node\<T\> head;

// Time Complexity: O(1)

public bool IsEmpty()

{

return head == null;

}

}
