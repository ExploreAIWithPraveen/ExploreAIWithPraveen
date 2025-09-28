### **Chapter 3: The Backtracking Technique 🗺️**

### **🔍 Project Jasper: A Real-Life Example**

I was working on a vision-aided research project in Europe with two
brilliant scientists, Aleena and Steve, along with our intern, Jiang.
Our team was a small but brilliant group, and as the lead researcher, I
was tasked with a unique challenge: naming our breakthrough invention.
We wanted a name that captured its essence---something that meant
\"third eye\" or \"blessing\"---while also including the letters from
our names: **Praveen, Aleena, Steve, and Jiang**. We decided to find a
single, powerful word that fit all the criteria.

To solve this, we first used a **sliding window** approach on our full
names to get all the unique letters we had to work with: P, R, A, V, E,
N, S, T, J, I, G. To encourage our intern, Jiang, we decided the name
should **start with his initial (J)**. And since I was the lead
inventor, the name had to **end with my initial (P)**.

With these strict rules, we turned to a powerful problem-solving
approach called **backtracking**. It\'s a method for finding a solution
by exploring every possible path, one step at a time. If a path leads to
a dead end, it \"undoes\" its last step to try a different option. This
\"trial and error\" with a systematic way of retreating is the essence
of the backtracking algorithm.

Here is how we used it to find the name for our project:

1.  **Start with a Goal:** Our goal was to find a single word that meant
    \"vision\" or \"enlightenment,\" started with J, ended with P, and
    contained other letters from our names.

2.  **Make a Choice:** The algorithm\'s first choice was easy: it had to
    start with J. Our word-in-progress was J.

3.  **Explore the Path:** Next, it tried adding an A to form JA. It then
    added an S, making JAS. The algorithm was building a path, and it
    continued to try the next available letters from our pool to see
    what words it could form.

4.  **Backtrack and Undo:** This is the most crucial step. Imagine the
    algorithm, having built JAS, tries to add an I (from Jiang\'s name).
    The word becomes JASI. The algorithm has a list of valid words (like
    a dictionary), and it immediately knows that \"JASI\" is not a word,
    nor is it the beginning of any known word related to our goal. It
    has hit a dead end.\
    Instead of starting over, it **backs up**. It **erases** the I it
    just added, and the word-in-progress is restored to JAS.\
    Now, from JAS, it tries a different available letter from the pool,
    which is P. It adds P to get JASP. The algorithm checks its
    dictionary and sees that \"JASP\" is the beginning of a word
    (\"JASPER\"). It knows it\'s on a promising path and continues
    forward.

After tirelessly backtracking through thousands of possible
combinations, our algorithm finally found a name that worked:
**JASPER**.

It was a perfect discovery. The name\'s very origin is from the Greek
word iaspis, which means \"spotted stone,\" a perfect metaphor for the
detailed vision our invention provides. It also contained all the
letters from our names---**J**iang, **A**leena, **S**teve, and
**P**raveen---and most importantly, it fit our specific rules of
starting with J and ending with P. The word was meaningful, powerful,
and a great name for our invention. We named it **Project Jasper**.

### **The Backtracking Steps 👣**

Every backtracking problem follows a simple set of rules.

1.  **Choose**: You pick one of the available options.

2.  **Explore**: You move forward with your choice. You use a recursive
    call to move to the next step of the problem. This is like going
    deeper into the maze.

3.  **Backtrack**: You undo your choice. After exploring a path, you
    must \"undo\" your last choice so you can try a different one. This
    is the crucial step that allows backtracking to find all possible
    solutions.

### **C# Templates: The Blueprints**

Here is a general C# template for backtracking that follows the
\"Choose, Explore, Backtrack\" pattern. The variable k represents the
**target size** or **length of the solution you are trying to find** and
must be passed as a parameter.

C#

public void Backtrack(List\<int\> currentCombination, int start, int n,
int k)

{

// 1. Base Case: If the solution is complete

if (currentCombination.Count == k)

{

// Add a copy of the solution to your results

results.Add(new List\<int\>(currentCombination));

return;

}

// 2. Iterate through choices

for (int i = start; i \<= n; i++)

{

// 3. Choose: Make a choice

currentCombination.Add(i);

// 4. Explore: Recurse with the new choice

Backtrack(currentCombination, i + 1, n, k);

// 5. Backtrack: Undo the choice to explore other options

currentCombination.RemoveAt(currentCombination.Count - 1);

}

}

### **Debug Section: Common Pitfalls 🚧**

- **Forgetting to Backtrack**: The most common and critical error in
  backtracking is forgetting to \"undo\" the choice after the recursive
  call. Without this step, your solution state will be incorrect for
  subsequent recursive calls, and you will not explore all possible
  paths correctly.

- **Incorrect Base Case**: If your base case (the condition to stop the
  recursion) is wrong, you might miss valid solutions or include invalid
  ones. The base case should be a precise check for a complete solution.

- **Improper Pruning**: While pruning is a great optimization, incorrect
  pruning conditions can lead to missing valid solutions. Make sure your
  pruning logic is sound and doesn\'t discard a path that could
  eventually lead to a correct answer.

### **Key Takeaways 🔑**

- Backtracking is a **systematic, recursive approach** for solving
  problems by exploring all possible solutions.

- The core pattern is **\"Choose, Explore, and Backtrack,\"** which
  allows you to try all paths from a decision point.

- **Pruning** is a vital optimization that helps to stop exploring a
  path early if it\'s determined to be a dead end.

- Backtracking is often used for problems that involve permutations,
  combinations, and finding all solutions to a given puzzle.

### **Do-It-Yourself Exercises 💻**

### **Basic Level**

1.  **Generate Parentheses**: Given n pairs of parentheses, write a
    function to generate all combinations of well-formed parentheses.

    - **Hint**: At each step, you have two choices: add a ( or add a ).
      The constraints are that you can\'t add ) unless you have an open
      ( available, and you can\'t have more than n pairs.

2.  **Permutations**: Given an array nums of distinct integers, return
    all the possible permutations.

    - **Hint**: At each step, choose an element that hasn\'t been used
      yet.

3.  **Combinations**: Given two integers n and k, return all possible
    combinations of k numbers out of n.

    - **Hint**: At each step, choose a number to include in your
      combination. To avoid duplicates, make sure you only choose
      numbers greater than the one you just chose.

### **Intermediate Level**

1.  **Subsets**: Given an integer array nums of unique elements, return
    all possible subsets (the power set).

    - **Hint**: For each element, you have two choices: either include
      it in your subset or don\'t.

2.  **Letter Combinations of a Phone Number**: Given a string containing
    digits from 2-9 inclusive, return all possible letter combinations
    that the number could represent.

    - **Hint**: Use a mapping of digits to letters. Recursively explore
      the combinations for each digit in the input string.

3.  **Combination Sum**: Given an array of distinct integers candidates
    and a target integer target, return a list of all unique
    combinations where the candidate numbers sum to target.

    - **Hint**: At each step, you can either include the current
      candidate number or move on to the next. A candidate can be used
      multiple times.

### **Expert Level**

1.  **N-Queens**: The n-queens puzzle is the problem of placing n queens
    on an n x n chessboard such that no two queens attack each other.
    Return all distinct solutions.

    - **Hint**: Use a backtracking function that places a queen one row
      at a time. The pruning condition is to check if the current
      position is safe from all previously placed queens (same column,
      same diagonals).

2.  **Sudoku Solver**: Write a program to solve a Sudoku puzzle by
    filling the empty cells.

    - **Hint**: At each empty cell, try placing a digit from 1 to 9. The
      pruning conditions are the Sudoku rules: a number can only appear
      once in a row, column, and 3x3 box.

3.  **Palindrome Partitioning**: Given a string s, partition s such that
    every substring of the partition is a palindrome. Return all
    possible palindrome partitioning of s.

    - **Hint**: At each position in the string, check all possible
      partitions. For each partition, check if the substring is a
      palindrome. If it is, recursively call the function on the rest of
      the string.
