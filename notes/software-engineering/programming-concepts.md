---
title: Data Structures and Algorithms
date: 2026-10-15
tags: [ascii, gk, sorting, bit operators, time complexity, space complexity]
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

**Big O Notation (O)** is the mathematical standard used to express these complexities. It strictly defines the **worst-case scenario** (the upper bound).

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

# Sorting Algorithms

---

## 1. Bubble Sort

Compares adjacent elements and swaps them if they are in the wrong order. Repeats until sorted. In each iteration the max element bubbles to the end of the array.

- Easy to understand, but slow for large arrays.
- Worst time: `O(n²)`

```cpp
void bubbleSort(vector<int>& a) {
    int n = a.size();

    for (int i = 0; i < n - 1; i++) {
        bool swapped = false;

        for (int j = 0; j < n - 1 - i; j++) {
            if (a[j] > a[j + 1]) {
                swap(a[j], a[j + 1]);
                swapped = true;
            }
        }

        if (!swapped) break;
    }
}
```

## 2. Selection Sort

Finds the smallest element and puts it at the beginning. Repeats for the remaining elements.

- Uses fewer swaps.
- Time: `O(n²)` 

```cpp
void selectionSort(vector<int>& a) {
    int n = a.size();

    for (int i = 0; i < n - 1; i++) {
        int minIndex = i;

        for (int j = i + 1; j < n; j++) {
            if (a[j] < a[minIndex])
                minIndex = j;
        }

        swap(a[i], a[minIndex]);
    }
}
```

## 3. Insertion Sort

Takes one element at a time and inserts it into the correct position in the already-sorted part.

- Good for small or nearly sorted arrays.
- Worst time: `O(n²)`

```cpp
void insertionSort(vector<int>& a) {
    int n = a.size();

    for (int i = 1; i < n; i++) {
        int key = a[i];
        int j = i - 1;

        while (j >= 0 && a[j] > key) {
            a[j + 1] = a[j];
            j--;
        }

        a[j + 1] = key;
    }
}
```

## 4. Merge Sort

Divides the array into smaller parts, sorts them, and merges them back together.

- Reliable and efficient.
- Time: `O(n log n)` 

```cpp
void merge(vector<int>& a, int l, int m, int r) {
    vector<int> temp;
    int i = l, j = m + 1;

    while (i <= m && j <= r) {
        if (a[i] <= a[j])
            temp.push_back(a[i++]);
        else
            temp.push_back(a[j++]);
    }

    while (i <= m) temp.push_back(a[i++]);
    while (j <= r) temp.push_back(a[j++]);

    for (int k = 0; k < temp.size(); k++)
        a[l + k] = temp[k];
}

void mergeSort(vector<int>& a, int l, int r) {
    if (l >= r) return;

    int m = l + (r - l) / 2;

    mergeSort(a, l, m);
    mergeSort(a, m + 1, r);
    merge(a, l, m, r);
}

// Call: mergeSort(a, 0, a.size() - 1);
```

## 5.Quick Sort

Picks a pivot, places smaller elements on one side and larger elements on the other, then sorts both sides.

- Usually very fast in practice.
- Worst time: `O(n²)`

```cpp
int partition(vector<int>& a, int low, int high) {
    int pivot = a[high];
    int i = low - 1;

    for (int j = low; j < high; j++) {
        if (a[j] <= pivot) {
            i++;
            swap(a[i], a[j]);
        }
    }

    swap(a[i + 1], a[high]);
    return i + 1;
}

void quickSort(vector<int>& a, int low, int high) {
    if (low >= high) return;

    int p = partition(a, low, high);

    quickSort(a, low, p - 1);
    quickSort(a, p + 1, high);
}

// Call: quickSort(a, 0, a.size() - 1);
```

## Bitwise AND (`&`)

Bitwise AND (`&`) in C++ compares the corresponding bits of two integers and returns `1` only when both bits are `1`; otherwise, it returns `0`. It is commonly used in DSA for checking bits, clearing bits, identifying common set bits, and working with bit masks.


| Property                      | Description                                                                                     |     |
| ----------------------------- | ----------------------------------------------------------------------------------------------- | --- |
| AND with zero                 | `a & 0 = 0` — The result is always `0`.                                                         |     |
| AND with itself               | `a & a = a` — The number remains unchanged.                                                     |     |
| AND with all ones             | `a & -1 = a` — For standard C++ integer types, `-1` has all bits set to `1`.                    |     |
| Commutative                   | `a & b = b & a` — Operand order does not matter.                                                |     |
| Associative                   | `(a & b) & c = a & (b & c)` — Grouping does not matter.                                         |     |
| Check a bit                   | `a & (1 << k)` — Checks whether the \\(k\\)-th bit is set; a nonzero result means it is set.    |     |
| Clear the rightmost set bit   | `a & (a - 1)` — Changes the rightmost `1` bit to `0`.                                           |     |
| Isolate the rightmost set bit | `a & -a` — Keeps only the rightmost set bit for ordinary integer values where negation is safe. |     |
| Check power of two            | `a > 0 && (a & (a - 1)) == 0` — True when `a` is a power of two.                                |     |


## Bitwise OR (`|`)

Bitwise OR (`|`) in C++ compares the corresponding bits of two integers and returns `1` when at least one bit is `1`; it returns `0` only when both bits are `0`. It is commonly used in DSA to set bits, combine bit masks, and enable specific flags.


| Property         | Description                                                                 |     |
| ---------------- | --------------------------------------------------------------------------- | --- |
| OR with zero     | `a | 0 = a` — The number remains unchanged.                                 |     |
| OR with itself   | `a | a = a` — The number remains unchanged.                                 |     |
| OR with all ones | `a | -1 = -1` — For standard C++ integer types, all result bits become `1`. |     |
| Commutative      | `a | b = b | a` — Operand order does not matter.                            |     |
| Associative      | `(a | b) | c = a | (b | c)` — Grouping does not matter.                     |     |
| Set a bit        | `a | (1 << k)` — Sets the (k)-th bit to `1`, leaving other bits unchanged.  |     |
| Combine set bits | `a | b` — Combines the set bits of both numbers.                            |     |
| Idempotent       | `a | a = a` — Repeating the same OR operation does not change the result.   |     |


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
