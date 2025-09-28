# **Chapter 2: The Two-Pointer Technique** 

Imagine you\'re the manager of a warehouse loading bay. You have a long
line of packages waiting to be loaded, and your truck\'s cargo space has
a very specific weight limit, say X. Your job is to find two packages
from the line whose combined weight equals X. If you\'re a beginner, you
might try a brute-force approach: you\'d pick up the first package and
compare its weight with every other package in the line. Then you\'d
move to the second package and repeat the process. This is incredibly
inefficient and time-consuming.

Now, imagine a smarter way. You station one worker at the very beginning
of the line (the **left pointer**) and another worker at the very end
(the **right pointer**). You tell them to meet in the middle, but with a
rule: at each step, they\'ll check the combined weight of their
packages. If the combined weight is too light, the person on the left
moves forward to a heavier package. If it\'s too heavy, the person on
the right moves back to a lighter one. This elegant system ensures they
find the correct pair much faster, without the need for endless
comparisons. This is the essence of the **two-pointer technique**.

### **1. Pointers Moving Towards Each Other 🤝**

This approach is the most direct and efficient way to solve our initial
loading bay problem. Imagine all the packages are **sorted by weight**,
from lightest to heaviest, along the line. You\'ve placed your two
workers, the **left pointer**, at the start of the line, and the **right
pointer**, at the very end.

**The Strategy**: The workers grab the packages at their respective ends
and check their combined weight.

- **If the combined weight is exactly X**, they\'ve found the solution.
  They can load these two packages and you\'re done.

- **If the combined weight is less than X**, they know they need more
  weight. Since the packages are sorted, the only way to increase the
  total is for the left worker to move one step to their right, picking
  up a slightly heavier package. The right worker stays put for now.

- **If the combined weight is more than X**, they need less weight. The
  right worker moves one step to their left, picking up a slightly
  lighter package. The left worker stays put.

They repeat this process, moving their pointers towards each other until
they find a pair or meet in the middle, at which point you know no such
pair exists. This method is incredibly efficient because at each step,
you eliminate one package from consideration, leading to a linear time
complexity of O(n).

### **2. Pointers Moving in the Same Direction 🏃‍♂️🏃‍♀️**

This approach is less intuitive for our initial problem but can be
adapted for a similar, though more complex, scenario. Imagine the
packages are on a long, single-file conveyor belt, but there are
multiple packages with the same weight. Your task is to find a
**contiguous block of packages** whose combined weight sums up to X.

**The Strategy**: You have two workers, a **slow pointer** and a **fast
pointer**, both starting at the beginning of the belt. They represent
the start and end of a \"window\" of packages. The fast pointer moves
forward, adding the weight of each new package to a running total. This
makes your \"window\" grow. As the window expands, the fast pointer
continuously checks if the total weight has reached or exceeded X. Once
the total weight hits or exceeds X, the slow pointer starts moving
forward. As it moves, it **subtracts** the weight of each package it
passes, shrinking the \"window\" from the left. This process continues,
with the fast pointer expanding the window and the slow pointer
shrinking it, always trying to find a window with a sum of exactly X.

This method is more complex but is powerful for finding contiguous
subarrays with a specific sum. It\'s essentially a variation of the
sliding window technique, where the two pointers define the window\'s
boundaries.

### **C# Templates: The Blueprints**

Here are the practical blueprints for these two patterns.

#### **Pointers Moving Towards Each Other**

This template is perfect for problems on sorted arrays.

C#

public int\[\] TwoSum(int\[\] nums, int target)

{

int left = 0;

int right = nums.Length - 1;

while (left \< right)

{

int currentSum = nums\[left\] + nums\[right\];

if (currentSum == target)

{

return new int\[\] { nums\[left\], nums\[right\] };

}

else if (currentSum \< target)

{

left++; // Need a larger sum, move left pointer right

}

else

{

right\--; // Need a smaller sum, move right pointer left

}

}

return new int\[0\]; // No solution found

}

#### **Pointers Moving in the Same Direction**

This template is often used for in-place array manipulation.

C#

public int RemoveDuplicates(int\[\] nums)

{

if (nums.Length == 0) return 0;

int slow = 0;

for (int fast = 1; fast \< nums.Length; fast++)

{

// If the fast pointer finds a new unique element

if (nums\[fast\] != nums\[slow\])

{

slow++;

nums\[slow\] = nums\[fast\]; // Overwrite the duplicate

}

}

return slow + 1; // Return the new length

}

### **Debug Section: Common Pitfalls 🚧**

- **Forgetting the Sorted Condition**: The two-pointer technique moving
  towards each other is only guaranteed to work on **sorted arrays**. If
  the array is unsorted, moving a pointer based on a sum will not be
  reliable. You\'d have to sort the array first, which adds an O(nlogn)
  step.

- **Incorrect Pointer Movement**: The logic for moving the pointers is
  crucial. If you move the wrong pointer or move both at the wrong time,
  your solution will be incorrect.

- **Infinite Loops**: When using pointers moving in the same direction,
  be careful with the conditions for updating both pointers. If your
  loop condition is incorrect or you don\'t advance a pointer, you could
  end up in an infinite loop.

### **Key Takeaways 🔑**

- The two-pointer technique is a method for efficiently traversing
  arrays or lists, typically in linear time.

- The two primary patterns are **pointers moving towards each other**
  (ideal for sorted arrays) and **pointers moving in the same
  direction** (ideal for linked lists or in-place array manipulation).

- The technique\'s efficiency comes from eliminating the need for nested
  loops, reducing time complexity from O(n2) to a much more efficient
  **O(n)**.

### **Recap: Two Pointers and Sliding Window**

The **\"Pointers Moving in the Same Direction\"** is a broader category
that encompasses the dynamic sliding window approach. It\'s not a
different technique but rather a parent pattern.

- In the general **\"Same Direction\"** pattern, the pointers might have
  completely different roles (e.g., one for reading, one for writing) or
  simply move at different rates to find a structural property. They
  don\'t necessarily define a contiguous \"window.\"

- The **dynamic sliding window** is a **specific application** of this
  broader pattern, where the two pointers **exclusively define the
  boundaries of a contiguous subarray or substring**. The entire
  algorithm revolves around expanding and shrinking this specific window
  to satisfy a condition. Therefore, while a dynamic sliding window is a
  two-pointer technique, not all \"same direction\" two-pointer problems
  are sliding window problems. The sliding window is a more specialized
  and constrained version.

### **Do-It-Yourself Exercises 💻**

#### **Basic Level**

1.  **Two Sum II - Input Array is Sorted**: Given a **1-indexed** array
    of integers numbers that is already **sorted** in non-decreasing
    order, find two numbers that add up to a specific target number.

2.  **Valid Palindrome**: Given a string s, return true if it is a
    palindrome, or false otherwise. Consider only alphanumeric
    characters and ignoring cases.

3.  **Reverse String**: Write a function that reverses a string. The
    input string is given as an array of characters char\[\]. You must
    do this by modifying the input array in-place with O(1) extra
    memory.

#### **Intermediate Level**

1.  **3Sum**: Given an integer array nums, return all the triplets
    \[nums\[i\], nums\[j\], nums\[k\]\] such that i != j, i != k, and j
    != k, and nums\[i\] + nums\[j\] + nums\[k\] == 0.

2.  **Remove Duplicates from Sorted Array**: Given a sorted array nums,
    remove the duplicates in-place such that each unique element appears
    only once.

3.  **Find the Duplicate Number**: Given an array of integers nums
    containing n + 1 integers where each integer is in the range \[1,
    n\] inclusive. There is only one repeated number in nums. Find this
    repeated number.

#### **Expert Level**

1.  **Trapping Rain Water**: Given n non-negative integers representing
    an elevation map where the width of each bar is 1, compute how much
    water it can trap after raining.

2.  **Container With Most Water**: Given n non-negative integers a1, a2,
    \..., an where each represents a point at coordinate (i, ai). n
    vertical lines are drawn such that the two endpoints of line i is at
    (i, ai) and (i, 0). Find two lines that together with the x-axis
    form a container, such that the container contains the most water.

3.  **Sort Colors**: Given an array nums with n objects colored red,
    white, or blue, sort them in-place so that objects of the same color
    are adjacent, with the colors in the order red, white, and blue. Use
    the integers 0, 1, and 2 to represent t[^1^]{.mark}he color red,
    white, and blue, respectively.
