# Appendix 1 : The Stack Data Structure 

## The Stacker 5000: A Real-Life Example

Living alone in a foreign country, not having any friend to talk to, I
often found ways to keep myself occupied, exploring the city or hopping
on trains. One day, I decided to do some free service as a waiter at a
small, bustling local restaurant. The work was frantic but fulfilling,
and it gave me a sense of community I hadn\'t found anywhere else.

One evening, as I was balancing a tray of appetizers, I looked up to see
a familiar face walking through the door. It was Steve, my site leader
from my day job. He was just as dumbfounded to see me as I was to see
him. We stood there, frozen, staring at each other in a moment of sheer
disbelief. The silence was broken by a crash from the kitchen---a
thunderous sound of collapsing and breaking plates.

\"Looks like they need some help back there,\" Steve said, gesturing to
the chaos. He walked over to the kitchen entrance, and I followed. We
found a small crew trying to salvage a mountain of shattered ceramics.

I explained the problem to Steve. \"This is our biggest bottleneck,\" I
said. \"The clean dishes get piled up, and when the cooks need one, they
grab it from the middle, and the whole thing comes crashing down.\"

\"This is a classic problem,\" Steve said, his engineering mind
instantly at work. \"You need a special container with a simple rule:
only one opening on top. You can only put a dish on the top, and you can
only take a dish from the very top.\"

This simple rule brought immediate order to the chaos. We implemented
this new system, and our workflow was completely transformed.

To put a dish on the stack: We would place it on the top of the pile.
This operation is called Push.

To take a dish from the stack: We would remove the top-most dish. This
operation is called Pop.

This system had one core principle: **Last-In, First-Out (LIFO)**. The
last dish we pushed onto the stack was always the first one we popped
off. It was simple, efficient, and perfectly solved our problem by
preventing the chaos of mixed-up dishes and broken plates. We called our
new system \"The Stacker 5000.\"

As we walked out of the kitchen, Steve clapped me on the shoulder, a wry
smile on his face. \"Let me know in case you need a raise to sustain
yourself so that you don\'t work here.\"

This kitchen scenario is a perfect analogy for a fundamental data
structure in computer science: the Stack.

## The Core Concepts of a Stack

A **Stack** is a linear data structure that operates on the **Last-In,
First-Out (LIFO)** principle. Think of a stack of books or a pile of
trays in a cafeteria---you can only add to or remove from the top.

The main operations of a Stack are:

- **Push:** Adds an element to the top of the stack.

- **Pop:** Removes and returns the top element of the stack.

- **Peek** or **Top:** Returns the top element without removing it.

- **IsEmpty:** Checks if the stack contains any elements.

A Stack is a powerful and elegant data structure because its simple,
constrained nature makes it perfect for problems that require a specific
order of operations.

## C# Templates: The Blueprints

C# has a built-in Stack\<T\> class, but it\'s useful to understand how a
basic Stack could be implemented. A simple implementation can use a
List\<T\> to manage the elements, with Add and RemoveAt operations.

C#

public class MyStack\<T\>

{

private List\<T\> items = new List\<T\>();

// Pushes an item to the top of the stack

public void Push(T item)

{

items.Add(item);

}

// Removes and returns the item at the top of the stack

public T Pop()

{

if (IsEmpty())

{

throw new InvalidOperationException(\"Stack is empty.\");

}

T item = items\[items.Count - 1\];

items.RemoveAt(items.Count - 1);

return item;

}

// Returns the item at the top of the stack without removing it

public T Peek()

{

if (IsEmpty())

{

throw new InvalidOperationException(\"Stack is empty.\");

}

return items\[items.Count - 1\];

}

// Checks if the stack is empty

public bool IsEmpty()

{

return items.Count == 0;

}

}

##  Debug Section: Common Pitfalls

- **Stack Overflow:** This is a classic programming error where a
  program recursively calls a function too many times, filling up the
  call stack and causing an error. It\'s a real-world example of a stack
  getting too big.

- **Popping an Empty Stack:** Trying to call the Pop() or Peek() method
  on an empty stack will result in an error. Always check IsEmpty()
  before trying to access or remove an element.

- **Misunderstanding LIFO:** Forgetting the LIFO principle can lead to
  logical errors in your program. If you need a First-In, First-Out
  (FIFO) order, you should use a Queue data structure instead.

##  Key Takeaways

- A Stack is a **Last-In, First-Out (LIFO)** data structure.

- Its primary operations are **Push**, **Pop**, **Peek**, and
  **IsEmpty**.

- Stacks are used when the order of operations must be reversed, such as
  in undo mechanisms, function calls, or expression evaluation.

## Do-It-Yourself Exercises

### Beginner

Solved Problem: Reverse a String

Problem: Write a function to reverse a string using a stack.

Solution:

This is a perfect example of how a stack\'s LIFO property can be used.
We simply iterate through the original string, pushing each character
onto a stack. Then, we pop each character from the stack, and because of
the LIFO principle, the characters will come out in the reverse order.

C#

public class StringReverser

{

public string Reverse(string s)

{

// Use the built-in C# Stack for simplicity

Stack\<char\> stack = new Stack\<char\>();

// 1. Push all characters from the string onto the stack

foreach (char c in s)

{

stack.Push(c);

}

// 2. Pop the characters to build the reversed string

string reversedString = \"\";

while (stack.Count \> 0)

{

reversedString += stack.Pop();

}

return reversedString;

}

}

- **Valid Parentheses:** Given a string containing just the characters
  (, ), {, }, \[, and \], determine if the input string is valid.

  - **Hint:** Use a stack to keep track of open brackets. When a closing
    bracket is encountered, pop the stack and check if it matches the
    corresponding opening bracket.

### Intermediate

- **Implement a Queue using Stacks:** A common interview question is to
  implement a FIFO queue data structure using two LIFO stacks.

  - **Hint:** Use one stack for pushing elements and another for
    popping.

- **Daily Temperatures:** Given a list of daily temperatures, return a
  list such that for each day, you tell how many days you have to wait
  until a warmer temperature. If there is no future day for which this
  is possible, put 0.

  - **Hint:** Use a stack to store the indices of the temperatures
    you\'ve seen.

### Expert

- **Evaluate Reverse Polish Notation:** Evaluate the value of an
  arithmetic expression in Reverse Polish Notation (RPN).

  - **Hint:** Use a stack to hold numbers. When you encounter an
    operator, pop two numbers, perform the operation, and push the
    result back onto the stack.
