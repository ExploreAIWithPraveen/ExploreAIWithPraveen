### **Appendix 3: The Heap Data Structure 🏆**

### **👨‍🍳 The Stacker 5000\'s Next-of-Kin: The Expedited Orders**

After the success of the Service Window, our café was busier than ever.
But with success came a new, more complex problem. Customers weren\'t
just showing up; they were placing orders with varying levels of
importance. We had a large online ordering system that handled
everything from a regular coffee order to a catering request for a large
corporate meeting. Steve and I realized that simply serving the first
order that came in wasn\'t working. The catering order, which took a
long time to prepare, was getting stuck behind dozens of single-coffee
requests.

\"The time-based system is failing us,\" Steve said, frustrated. \"We
need to serve the most important orders first, regardless of when they
were placed. The big catering order needs to jump to the front of the
line.\"

This was our next challenge. We needed a system that prioritized tasks
based on their value, not their arrival time. We couldn\'t just have a
single line anymore. We needed to know at a glance which order was the
most important.

Our solution was a new system we called \"The Expedited Orders.\" We
created a visual display board that showed all pending orders. Whenever
a new order came in, we would find its place among the others based on
its size and importance. The biggest, most valuable orders would always
be at the top, ready to be prepared first.

To add a new order: We would place the new order on the display board
and then re-sort the board to ensure the most important order was always
at the top. This operation is called insert.

To process an order: We would always take the most important order from
the top of the board. This operation is called extract max (or extract
min if we were serving the smallest orders first).

This system had one core principle: **priority-based order**. The order
we processed was always the one with the highest (or lowest) priority.
This elegant solution brought a new level of efficiency, ensuring our
most critical tasks were always handled first.

### **🧠 The Core Concepts of a Heap**

A **Heap** is a specialized tree-based data structure that satisfies the
**heap property**. It\'s not just a collection of items; it\'s a
collection organized based on a specific rule. The most common type is a
**Binary Heap**, which is a complete binary tree.

The key property that defines a heap is:

- **Max-Heap**: For any given node C, if P is a parent node of C, then
  the value of P is greater than or equal to the value of C. The largest
  element is always at the root.

- **Min-Heap**: For any given node C, if P is a parent node of C, then
  the value of P is less than or equal to the value of C. The smallest
  element is always at the root.

Heaps are highly efficient for finding the minimum or maximum element,
making them perfect for implementing a **Priority Queue**. Unlike a
simple sorted list where adding an element can be slow, heaps use a
clever structure to keep things organized quickly.

The main operations of a Heap are:

- **Insert**: Adds a new element to the heap while maintaining the heap
  property.

- **Extract Max/Min**: Removes and returns the root element (the largest
  or smallest) from the heap.

- **Peek Max/Min**: Returns the root element without removing it.

Heaps are a powerful and elegant data structure because their simple,
constrained nature makes them perfect for problems that require items to
be prioritized.

### **C# Templates: The Blueprints for a Heap**

The most common way to implement a binary heap is using a **dynamic
array** or List\<T\>. This provides a compact, cache-friendly structure
where parent and child nodes can be calculated using simple arithmetic
without the overhead of pointers. For a **Max-Heap**:

- Parent of a node at index i is at (i - 1) / 2.

- Children of a node at index i are at 2 \* i + 1 and 2 \* i + 2.

This allows both Insert and Extract operations to be highly efficient
with a time complexity of **O(log n)**.

C#

public class MaxHeap\<T\> where T : IComparable\<T\>

{

private List\<T\> items;

public MaxHeap()

{

items = new List\<T\>();

}

// Inserts an item into the heap.

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

// Swap if child is greater than parent

T temp = items\[currentIndex\];

items\[currentIndex\] = items\[parentIndex\];

items\[parentIndex\] = temp;

currentIndex = parentIndex;

}

}

// Removes and returns the maximum item from the heap.

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

// Helper method to maintain the heap property after extraction.

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

public T PeekMax()

{

if (items.Count == 0)

{

throw new InvalidOperationException(\"Heap is empty.\");

}

return items\[0\];

}

}

### **💻 Do-It-Yourself Exercises: Heap**

#### **Beginner**

Solved Problem: Find the Kth Largest Element

Problem: Given a list of numbers and an integer k, find the kth largest
element.

Solution:

A heap is the perfect tool for this. We can use a Max-Heap to
efficiently find the largest element. We simply insert all elements into
the heap and then ExtractMax k times. The element we get on the kth
extraction is the answer.

C#

public class KthLargestFinder

{

public int FindKthLargest(int\[\] nums, int k)

{

MaxHeap\<int\> heap = new MaxHeap\<int\>();

foreach (int num in nums)

{

heap.Insert(num);

}

int kthLargest = 0;

for (int i = 0; i \< k; i++)

{

kthLargest = heap.ExtractMax();

}

return kthLargest;

}

}

Heap Sort: Implement the Heap Sort algorithm.

Hint: Build a max-heap from the input array. Then, repeatedly extract
the max element and place it at the end of the sorted portion of the
array.

#### **Intermediate**

Merge K Sorted Lists: Given k sorted linked lists, merge them into one
sorted linked list.

Hint: Use a Min-Heap to keep track of the smallest elements from each
list.

#### **Expert**

Skyline Problem: Given a list of buildings, compute the skyline of the
city.

Hint: This is a complex problem that can be solved efficiently using a
combination of events and a max-heap to track the heights of buildings.
