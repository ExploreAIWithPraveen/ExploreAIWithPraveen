# **Chapter 1: The Sliding Window Technique 🖼️**

Imagine you\'re on a train, looking out a window. You want to capture
the best three-second video clip of the passing scenery. You can\'t just
stare at the whole landscape at once; you focus on a small \"window\" of
what\'s currently visible. As the train moves, your window of view
slides along, revealing new scenery on one side and letting the old
scenery disappear on the other. You're not starting over with a new view
every time; you\'re just incrementally updating your current one.
That\'s the core idea behind the **sliding window** algorithm. It's an
elegant, efficient way to solve problems on a continuous stream of data
without having to re-process everything from scratch.

This powerful technique primarily applies to **contiguous subsequences**
of arrays and strings. It turns a slow, laborious brute-force approach
(like re-recording every three-second clip from the start) into a swift,
linear scan.

## **The Two Main Patterns**

Just as your train window might be a fixed size or you might adjust it,
there are two main types of sliding windows.

### **1. The Fixed-Size Window 📏**

Think of this like a **cruise ship cabin window**. The size is fixed and
it doesn\'t change. You are tasked with finding the section of the ocean
where the temperature is highest over a 7-day period. Instead of
calculating the average temperature for every possible 7-day period from
the beginning of the trip, you use a sliding window. You calculate the
sum for the first 7 days. Then, on day 8, you simply subtract the
temperature from day 1 and add the temperature from day 8 to your
running total. This is a brilliant shortcut, allowing you to update your
sum in a single step rather than re-adding all seven numbers. This makes
the entire process incredibly fast.

### **2. The Dynamic-Sized Window 🔍**

Now, imagine you\'re a photographer with a zoom lens. Your goal is to
find the **longest possible shot that captures a specific set of
objects** (say, a mountain, a river, and a forest) from your moving
train. The size of your shot (the window) isn\'t fixed. You start by
expanding your view (the right pointer) until you see all three objects.
Once you have them, you don\'t need a wider shot. You start zooming in
(moving the left pointer) to find the smallest possible view that still
contains all three. As you move, you might see a new object that allows
you to expand again. This constant expansion and shrinking to find the
optimal window is the essence of the dynamic-sized sliding window.

## **C# Templates**

Here are the practical blueprints for these two patterns.

### **Fixed-Size Window Template (Efficient)**

This template is like using a well-oiled machine. It gets the job done
with minimal effort.

C#

public int MaxSumSubarray(int\[\] nums, int k)

{

int currentSum = 0;

int maxSum = 0;

// Calculate sum of the first window

for (int i = 0; i \< k; i++)

{

currentSum += nums\[i\];

}

maxSum = currentSum;

// Slide the window with O(1) updates

for (int i = k; i \< nums.Length; i++)

{

currentSum += nums\[i\] - nums\[i - k\];

maxSum = Math.Max(maxSum, currentSum);

}

return maxSum;

}

### **Dynamic-Sized Window Template**

This template is like a flexible toolkit, adapting its size to fit the
problem\'s needs.

C#

public int LongestSubstringWithKDistinct(string s, int k)

{

Dictionary\<char, int\> charFreq = new Dictionary\<char, int\>();

int left = 0;

int maxLength = 0;

// Expand the window

for (int right = 0; right \< s.Length; right++)

{

char rightChar = s\[right\];

if (charFreq.ContainsKey(rightChar))

charFreq\[rightChar\]++;

else

charFreq\[rightChar\] = 1;

// Shrink the window if condition is violated

while (charFreq.Count \> k)

{

char leftChar = s\[left\];

charFreq\[leftChar\]\--;

if (charFreq\[leftChar\] == 0)

charFreq.Remove(leftChar);

left++;

}

// Update the result

maxLength = Math.Max(maxLength, right - left + 1);

}

return maxLength;

}

## **Debug Section: Common Pitfalls 🚧**

### **1. The \"Looks-Like-A-Sliding-Window\" Deception**

Sometimes, a problem\'s wording can be misleading. Be cautious! The
sliding window is only for problems on **contiguous** elements. If a
problem allows you to pick and choose non-adjacent elements (e.g.,
\"find the maximum sum of three numbers in an array\"), it\'s not a
sliding window problem. It\'s often a job for sorting, dynamic
programming, or other techniques.

### **2. The \"Shrinking\" Blind Spot**

This is the most common mistake in dynamic window problems. You\'ll
correctly expand the window, but when the condition is violated, you
forget to shrink it from the left. This leads to the window growing
infinitely and producing an incorrect, or even a time-out, result.

### **3. Edge Case Neglect**

What happens with an empty array or an array smaller than k? What if all
numbers are negative? Always think about these edge cases. A robust
sliding window solution must handle these gracefully.

## **Key Takeaways 🔑**

- The sliding window is an **optimization** technique, not a standalone
  algorithm. It\'s designed to make other algorithms more efficient.

- The core idea is to **reuse previous computations** by incrementally
  updating your window\'s state, saving you from redundant work.

- It is most effective on problems involving **contiguous subarrays or
  substrings**. If elements can be non-adjacent, look for a different
  approach.

- **Shrinking** the window is a critical step that is unique to the
  dynamic-sized window pattern.

- While the naive brute-force approach has a time complexity of
  \$O(n\\\*k)\$, the sliding window reduces it to a powerful **O(n)**.

## **Do-It-Yourself Exercises 💻**

### **Basic Level: Fixed-Size Window**

1.  **Maximum Average Subarray I:** Given an array nums and k, find the
    contiguous subarray whose length is equal to k that has the maximum
    average value.

    - **Hint:** The average is simply the sum divided by k. Since k is
      fixed, you only need to find the maximum sum of a k-sized window.

2.  **Count Subarrays with Sum Equal to K:** Given an array nums and an
    integer k, return the number of subarrays with a sum equal to k.

    - **Hint:** Use a fixed-size window. Track the sum of the current
      window and check if it equals k at each step.

3.  **Find the First Negative Integer in Every Window of Size K:** Given
    an array A and a window size K, find the first negative integer in
    each window.

    - **Hint:** You can use an auxiliary data structure like a queue to
      store the negative numbers within the current window.

### **Intermediate Level: Dynamic-Sized Window**

1.  **Longest Substring Without Repeating Characters:** Given a string
    s, find the length of the longest substring without repeating
    characters.

    - **Hint:** Expand the window with a right pointer. Use a dictionary
      or a hash set to track character frequencies. If a character is a
      repeat, shrink the window from the left until the repeat is gone.

2.  **Shortest Subarray with Sum at Least K:** Given an array A and an
    integer K, find the length of the shortest, non-empty, contiguous
    subarray with a sum of at least K.

    - **Hint:** This is a tricky one. The basic dynamic window template
      with two pointers works here, but it\'s not always the most
      optimal. A more advanced solution often involves a deque
      (double-ended queue) to maintain prefix sums, which can find the
      shortest valid window faster.

3.  **Find All Anagrams in a String:** Given two strings s and p, return
    the start indices of all of p\'s anagrams in s.

    - **Hint:** Anagrams have the same character counts. This is a
      fixed-size window problem where the window size is p.Length. Use
      frequency arrays to compare the current window in s with the
      character counts of p.

### **Expert Level: Advanced Applications**

1.  **Minimum Window Substring:** Given two strings s and t, find the
    minimum window substring of s which contains all the characters of
    t.

    - **Hint:** A quintessential dynamic window problem. Use a hash map
      to store t\'s characters and their required counts. Expand the
      window until all of t\'s characters are \"covered.\" Then, start
      shrinking from the left to find the minimum possible length.

2.  **Longest Substring with At Most Two Distinct Characters:** Given a
    string s, find the length of the longest substring that contains at
    most two distinct characters.

    - **Hint:** This is a specific case of the dynamic window template
      where the condition is fixed at k=2. The logic of expanding and
      shrinking remains identical.

3.  **Maximum Sum of Two Non-Overlapping Subarrays:** Given an array
    nums and two lengths, firstLen and secondLen, find the maximum sum
    of two non-overlapping subarrays with these lengths.

    - **Hint:** This problem requires a two-pass approach. First, you
      can pre-compute the maximum sum of firstLen and secondLen
      subarrays ending at each index. Then, you can iterate through the
      array to find the best combination of these pre-calculated values.
