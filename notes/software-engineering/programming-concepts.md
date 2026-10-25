---
title: Data Structures and Algorithms
date: 2026-10-15
tags: [ascii, gk]
pinned: true
---

## ASCII Values

- **Uppercase letters (A - Z):** 65 to 90
  - 'A' = 65
  - 'Z' = 90
- **Lowercase letters (a - z):** 97 to 122
  - 'a' = 97
  - 'z' = 122
- **Note:** The gap between the uppercase and lowercase ranges (ASCII 91 to 96) contains symbols like `[`, `\`, `]`, `^`, `_`, and \`\`\`. The lowercase value of any letter is always exactly 32 greater than its uppercase counterpart (e.g., 'A' is 65, 'a' is 65 + 32 = 97).

---

## Time Complexity

**Time Complexity** measures how the runtime of an algorithm scales as the input size ($N$) grows. It does not measure absolute seconds, as that depends on hardware; instead, it counts the total number of fundamental operations executed.

## Space Complexity

**Space Complexity** measures how the memory footprint of an algorithm scales with the input size. In problem-solving, this usually refers to **auxiliary space**—the temporary, extra memory your algorithm allocates (like hash maps, dynamic arrays, or the recursion call stack), excluding the memory needed to store the initial input.

**Big O Notation ($O$)** is the mathematical standard used to express these complexities. It strictly defines the **worst-case scenario** (the upper bound).

When calculating Big O, you drop constants and lower-order terms. For example, if an algorithm takes O(2N^2 + 50N + 5), it simplifies to O(N^2). As N approaches infinity, the constants and the 50N become statistically irrelevant; the N^2 term is the bottleneck that dictates system failure.

> **The Essential Big O Hierarchy (Fastest to Slowest):**
>
> - **O(1) Constant:** Execution time or space remains exactly the same regardless of input size.  
> *Examples:* Accessing an array by index, math formulas, pushing to a stack.
> - **O(log N) Logarithmic:** The algorithm repeatedly halves the search space. It is incredibly efficient, taking very few extra steps even if the dataset expands by millions.  
> *Examples:* Binary Search, finding an item in a balanced Binary Search Tree.
> - **O(N) Linear:** Execution scales at a 1:1 ratio with the input.  
> *Examples:* Iterating through a standard array with a single `for` loop, Two Pointers.
> - **O(N log N) Linearithmic:** The baseline for optimal comparison-based algorithms.  
> *Examples:* Standard library sorting (like C++ `std::sort` or Java `Arrays.sort()`), Merge Sort.
> - **O(N^2) Quadratic:** Every element interacts with every other element. Usually causes a "Time Limit Exceeded" (TLE) error on LeetCode for inputs larger than $10^4$.  
> *Examples:* Double nested loops, Bubble Sort, Selection Sort.
> - **O(2^N) Exponential:** The runtime doubles with every single addition to the input.  
> *Examples:* Unoptimized branching recursion (like naive Fibonacci), generating all subsets of a set.

## XOR(^) operator

XOR (`^`) in C++ is a bitwise operator that compares corresponding bits of two integers and returns `1` if the bits are different and `0` if they are the same. It is commonly used in bit manipulation and DSA problems because of its cancellation properties, which help find unique or missing numbers efficiently.


| Property              | Description                                                                                                      |     |
| --------------------- | ---------------------------------------------------------------------------------------------------------------- | --- |
| XOR with zero         | `a ^ 0 = a` — XOR with `0` leaves the number unchanged.                                                          |     |
| XOR with itself       | `a ^ a = 0` — A number XORed with itself becomes `0`.                                                            |     |
| Commutative           | `a ^ b = b ^ a` — The order of operands does not matter.                                                         |     |
| Associative           | `(a ^ b) ^ c = a ^ (b ^ c)` — Grouping does not matter.                                                          |     |
| Cancellation          | `a ^ b ^ a = b` — Identical pairs cancel each other.                                                             |     |
| Even/odd occurrences  | An even number of occurrences of a value cancel to `0`; an odd number leave one occurrence.                      |     |
| Bit toggling          | XOR with a bit mask flips bits where the mask has `1` and leaves bits where it has `0` unchanged.                |     |
| Find a unique number  | XOR all array elements when every number appears twice except one; duplicates cancel, leaving the unique number. |     |
| Find a missing number | XOR the expected numbers and array elements; matching values cancel, leaving the missing number.                 |     |
| Swap two numbers      | XOR can swap two integers without a temporary variable, though `std::swap()` is generally clearer and safer.     |     |
