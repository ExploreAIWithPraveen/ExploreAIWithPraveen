### **Appendix 2: The Queue Data Structure ☕**

### **👨‍🍳 The Stacker 5000\'s Cousin: The Service Window**

After our success with the Stacker 5000, Steve, my site leader, was
convinced that we could bring order to the entire restaurant. One
afternoon, he came to me with a new problem. \"Look,\" he said, pointing
to the barista station. \"We have the best coffee in the city, but we
can\'t keep up with the orders.\"

I looked over and saw a frantic scene. Baristas were shouting out names,
trying to hand drinks to customers in a chaotic jumble. Someone who
ordered a simple black coffee five minutes ago was still waiting, while
a latecomer who ordered a complicated latte had already walked away with
their drink.

\"It's just like the kitchen,\" I said, \"but the opposite. Here, the
first person to order should be the first person to get their coffee.\"

Steve\'s eyes lit up. \"Exactly! We need a system where we only serve
the people at the very front of the line, and new people can only join
at the very back.\"

This was our new challenge. We designated a \"service window\" at the
front of the counter and a clear \"start of the line\" spot at the back.
Every time a new customer placed an order, they would join the line at
the back. When a barista finished a drink, they would hand it to the
person at the front of the line, and that person would leave, allowing
the next person to move forward.

This system, which we called \"The Service Window,\" brought immediate
calm to the chaos. The first customer to place their order was always
the first to receive their drink.

To add a new customer to the line: We\'d place their order at the rear
of the line. This operation is called Enqueue.

To serve a customer: We\'d remove their order from the front of the
line. This operation is called Dequeue.

This system had one core principle: **First-In, First-Out (FIFO)**. The
first order we enqueued was always the first one we dequeued. It was
simple, fair, and perfectly solved our problem by bringing a sense of
order and predictability to our busiest moments.

### **🧠 The Core Concepts of a Queue**

A **Queue** is a linear data structure that operates on the **First-In,
First-Out (FIFO)** principle. Think of a line at a bank, a bus stop, or
a printer queue---the first item to enter is the first one to be
processed.

The main operations of a Queue are:

- **Enqueue**: Adds an element to the **rear** of the queue.

- **Dequeue**: Removes and returns the element from the **front** of the
  queue.

- **Peek** or **Front**: Returns the front element without removing it.

- **IsEmpty**: Checks if the queue contains any elements.

Queues are a powerful and elegant data structure because their simple,
constrained nature makes them perfect for problems that require items to
be processed in a specific, chronological order.

### **C# Templates: The Blueprints for a Queue**

For large datasets, using a List\<T\> for queue implementation is
inefficient because the RemoveAt(0) operation requires shifting all
subsequent elements, leading to a time complexity of O(n) for dequeuing.
A **doubly linked list** is a much more efficient underlying data
structure for a queue, as both Enqueue and Dequeue operations can be
performed in **O(1)** time.

C#

public class MyQueue\<T\>

{

private LinkedList\<T\> items = new LinkedList\<T\>();

// Adds an item to the end of the queue.

// Time Complexity: O(1)

public void Enqueue(T item)

{

items.AddLast(item);

}

// Removes and returns the item at the front of the queue.

// Time Complexity: O(1)

public T Dequeue()

{

if (IsEmpty())

{

throw new InvalidOperationException(\"Queue is empty.\");

}

T item = items.First.Value;

items.RemoveFirst();

return item;

}

// Returns the item at the front of the queue without removing it.

// Time Complexity: O(1)

public T Peek()

{

if (IsEmpty())

{

throw new InvalidOperationException(\"Queue is empty.\");

}

return items.First.Value;

}

// Checks if the queue is empty.

// Time Complexity: O(1)

public bool IsEmpty()

{

return items.Count == 0;

}

}

### **💻 Do-It-Yourself Exercises: Queue**

#### **Beginner**

Solved Problem: Ticket Counter

Problem: Simulate a simple ticket counter. Customers arrive in order,
and the counter serves them one by one. Write a function that takes a
list of customer names and processes them in a queue, printing a message
for each customer served.

Solution:

This is a perfect example of a queue\'s FIFO property. We simply enqueue
each customer, then dequeue and serve them one by one.

C#

public class TicketCounter

{

public void ProcessCustomers(List\<string\> customers)

{

// Use the built-in C# Queue for simplicity

Queue\<string\> queue = new Queue\<string\>();

// 1. Enqueue all customers

foreach (string customer in customers)

{

queue.Enqueue(customer);

Console.WriteLine(\$\"Customer {customer} joined the queue.\");

}

Console.WriteLine(\"\\nProcessing customers:\");

// 2. Dequeue customers one by one

while (queue.Count \> 0)

{

string currentCustomer = queue.Dequeue();

Console.WriteLine(\$\"Serving customer: {currentCustomer}\");

}

}

}

**Valid Parentheses**: A common problem for stacks, but let\'s
re-imagine it for queues. Write a function that determines if the input
string of parentheses () is valid. Hint: Use a queue to store opening
parentheses and then dequeue to match.

#### **Intermediate**

Implement a Stack using Queues: A common interview question is to
implement a LIFO stack data structure using two FIFO queues.

Hint: Use one queue for pushing elements and another for popping.

Breadth-First Search (BFS): A classic graph traversal algorithm. Given a
starting node in a graph, write a function to traverse and print all
reachable nodes using a queue.

Hint: Use a queue to store the nodes you need to visit.

#### **Expert**

Level Order Traversal of a Binary Tree: A more complex version of BFS.
Given the root of a binary tree, return the nodes in level-order
traversal.

Hint: Use a queue to keep track of nodes at the current level.

### **☕ A Twist on the Line: The Priority Queue**

Our Service Window worked great until a regular customer, a doctor named
Dr. Anya Sharma, burst in one day in a panic. \"I need my coffee now! I
have an emergency surgery in five minutes!\"

Steve looked at the long line of customers, then back at Dr. Sharma. The
first-in, first-out rule suddenly seemed rigid and impractical. Some
tasks just matter more than others.

This is where a **Priority Queue** comes in. Instead of just a single
line, we created a system with different queues based on a customer\'s
urgency. A doctor with an emergency would get priority over someone who
was just waiting for a leisurely afternoon coffee.

A Priority Queue is a special type of queue where each element has an
associated **priority**. The highest-priority element is always the one
that gets dequeued first, regardless of when it was enqueued.

Think of an emergency room: a patient with a life-threatening injury is
seen before someone with a minor cut, even if the person with the cut
arrived first. The highest-priority patient is treated first.

The operations are similar, but with a crucial difference:

- **Enqueue**: We add an element along with its priority. The queue then
  reorders itself.

- **Dequeue**: We always remove the element with the highest priority.

This system is perfect for situations where simple chronological order
isn\'t enough, like in operating systems for scheduling high-priority
tasks, or in network routers for prioritizing critical data packets.

### **C# Templates: The Blueprints for a Priority Queue**

For large datasets, a simple sorted list for a priority queue is
inefficient as Enqueue has a time complexity of O(n) due to sorting. The
most efficient way to implement a priority queue is with a **binary
heap**. This structure ensures that Enqueue has an average time
complexity of **O(log n)** and Dequeue has a time complexity of **O(log
n)**.

C#

public class MyPriorityQueue\<T\>

{

private List\<(T item, int priority)\> heap = new List\<(T, int)\>();

// Adds an item to the queue, maintaining heap property.

// Time Complexity: O(log n)

public void Enqueue(T item, int priority)

{

heap.Add((item, priority));

int childIndex = heap.Count - 1;

while (childIndex \> 0)

{

int parentIndex = (childIndex - 1) / 2;

if (heap\[parentIndex\].priority \>= heap\[childIndex\].priority)

{

break;

}

// Swap parent and child

(T item, int priority) temp = heap\[childIndex\];

heap\[childIndex\] = heap\[parentIndex\];

heap\[parentIndex\] = temp;

childIndex = parentIndex;

}

}

// Removes and returns the highest-priority item.

// Time Complexity: O(log n)

public T Dequeue()

{

if (IsEmpty())

{

throw new InvalidOperationException(\"Priority Queue is empty.\");

}

T item = heap\[0\].item;

heap\[0\] = heap\[heap.Count - 1\];

heap.RemoveAt(heap.Count - 1);

int parentIndex = 0;

while (true)

{

int leftChildIndex = 2 \* parentIndex + 1;

int rightChildIndex = 2 \* parentIndex + 2;

int largestIndex = parentIndex;

if (leftChildIndex \< heap.Count && heap\[leftChildIndex\].priority \>
heap\[largestIndex\].priority)

{

largestIndex = leftChildIndex;

}

if (rightChildIndex \< heap.Count && heap\[rightChildIndex\].priority \>
heap\[largestIndex\].priority)

{

largestIndex = rightChildIndex;

}

if (largestIndex == parentIndex)

{

break;

}

// Swap parent and largest child

(T item, int priority) temp = heap\[parentIndex\];

heap\[parentIndex\] = heap\[largestIndex\];

heap\[largestIndex\] = temp;

parentIndex = largestIndex;

}

return item;

}

public T Peek()

{

if (IsEmpty())

{

throw new InvalidOperationException(\"Priority Queue is empty.\");

}

return heap\[0\].item;

}

public bool IsEmpty()

{

return heap.Count == 0;

}

}

### **💻 Do-It-Yourself Exercises: Priority Queue**

#### **Beginner**

Solved Problem: Task Scheduler

Problem: You have a list of tasks with priorities (1 being highest
priority). Implement a task scheduler that processes tasks based on
their priority.

Solution:

A priority queue is a perfect fit for this. We enqueue tasks with their
priority and the queue ensures we always dequeue the highest-priority
task first.

C#

public class TaskScheduler

{

public void ScheduleTasks()

{

// Using the simplified Priority Queue from above

MyPriorityQueue\<string\> taskQueue = new MyPriorityQueue\<string\>();

taskQueue.Enqueue(\"Finish report\", 3);

taskQueue.Enqueue(\"Fix critical bug\", 1);

taskQueue.Enqueue(\"Write a new feature\", 2);

taskQueue.Enqueue(\"Send meeting minutes\", 3);

Console.WriteLine(\"Processing tasks based on priority:\");

while (!taskQueue.IsEmpty())

{

string task = taskQueue.Dequeue();

Console.WriteLine(\$\"Processing task: {task}\");

}

}

}

#### **Intermediate**

Weighted Dijkstra\'s Algorithm: Use a priority queue to implement
Dijkstra\'s algorithm for finding the shortest path in a weighted graph.

Hint: The priority queue will store nodes to visit, with the priority
being the current shortest distance from the source.

#### **Expert**

Median of a Data Stream: Given a stream of integers, implement a class
that calculates the median of the numbers added so far.

Hint: Use two heaps (a max-heap and a min-heap) to keep track of the
lower half and upper half of the numbers. A priority queue can be used
to implement a heap.

### **🔄 The Ever-Moving Line: The Circular Queue**

As our café grew more popular, we started to run into a new problem with
our \"Service Window\" system. We were using a simple array to represent
the line, and every time someone was served (**dequeued**), we had to
shift everyone else forward. As the line got longer, this became a huge
waste of time and energy. It was like a game of musical chairs where
everyone had to move up one spot every time someone left.

Steve noticed this bottleneck. \"We\'re wasting all this space at the
front of the line,\" he said, \"and making the baristas wait for the
whole line to shift forward. We need a way for the line to wrap around
and reuse that space.\"

The solution was a **Circular Queue**. Instead of a straight line, we
imagined our array as a circle. When the **rear** of the queue reached
the end of the array, it would simply wrap back around to the beginning,
as long as there was space available from a previous dequeue operation.

This made a massive difference. Now, both enqueue and dequeue operations
could be performed in a single, constant step, no matter how long the
line was. We had eliminated the need to shift everyone forward, making
our system incredibly efficient.

The **Circular Queue** is an optimized version of a linear queue,
typically implemented with a fixed-size array. Its key features are:

- **Fixed Size**: It\'s constrained to a maximum number of elements.

- **Reusability**: It efficiently reuses empty space created by dequeue
  operations.

This data structure is perfect for applications with a fixed buffer
size, such as CPU scheduling in operating systems where tasks are cycled
through in a **round-robin** fashion. The clock on a wall is another
perfect example: when the hand reaches 12, it doesn\'t stop, it just
wraps around to 1 and keeps going.

### **C# Templates: The Blueprints for a Circular Queue**

The circular queue implementation using a fixed-size array is already
highly efficient for large datasets, as both Enqueue and Dequeue
operations have a **time complexity of O(1)**. The use of the modulo
operator eliminates the need for expensive data shifting.

C#

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

public T Peek()

{

if (IsEmpty())

{

throw new InvalidOperationException(\"Queue is empty.\");

}

return items\[front\];

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

### **💻 Do-It-Yourself Exercises: Circular Queue**

#### **Beginner**

Solved Problem: Fixed-Size Message Buffer

Problem: Implement a message buffer that can hold a fixed number of
messages. When the buffer is full and a new message arrives, the oldest
message should be overwritten.

Solution:

This is a classic use case for a circular queue. When the queue is full,
we simply dequeue the oldest message and enqueue the new one,
effectively overwriting the front element.

C#

public class MessageBuffer

{

private CircularQueue\<string\> buffer;

public MessageBuffer(int size)

{

buffer = new CircularQueue\<string\>(size);

}

public void AddMessage(string message)

{

if (buffer.IsFull())

{

Console.WriteLine(\"Buffer is full, overwriting oldest message\...\");

buffer.Dequeue(); // Remove the oldest message

}

buffer.Enqueue(message);

Console.WriteLine(\$\"Added new message: {message}\");

}

}

#### **Intermediate**

Round-Robin Task Scheduler: Simulate a CPU scheduler that uses a
round-robin algorithm to process tasks. Each task gets a fixed time
slice before the next task is processed.

Hint: Use a circular queue to hold the tasks.

#### **Expert**

LRU Cache Implementation: Implement a Least Recently Used (LRU) cache,
which is a data structure that stores a limited number of items,
discarding the least recently used items when new items are added.

Hint: This problem is often solved with a combination of a hash map and
a doubly linked list, which can be thought of as a special type of
circular structure.
