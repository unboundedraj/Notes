---
title: Data Structures and Algorithms
date: 2026-10-15
tags: [ascii, gk, sorting, bit operators, time complexity, space complexity]
pinned: true
---

## Approximate Range for numerical variables

In competitive programming, use:

- `int` for values up to around (10^9).
- `long long` for values up to around (10^18)

## ASCII Values

- **Uppercase letters (A - Z):** 65 to 90
  - 'A' = 65
  - 'Z' = 90
- **Lowercase letters (a - z):** 97 to 122
  - 'a' = 97
  - 'z' = 122
- **Note:** The gap between the uppercase and lowercase ranges (ASCII 91 to 96) contains symbols like `[`, `\`, `]`, `^`, `_`, and \`\`\`. The lowercase value of any letter is always exactly 32 greater than its uppercase counterpart (e.g., 'A' is 65, 'a' is 65 + 32 = 97).

---

> #Note that the newline "\\n" works faster than endl, because endl always causes a flush operation.  
> #8 bits = 1 byte  
> #Note that e is a scientific way to write 10 to the power something and it works in programming languages as well e.g.: 1e24 is (1 multiplied by 10 to the power 24)

> Use the below functions to find the minimum and maximum elements in vectors  
> Note that it returns the pointer and we are dereferencing it to find the actual value  
> The `min()` and `max()` functions work directly on two values.  
> You cannot directly write `min(v)` or `max(v)`.  
> Instead, use `min_element()` and `max_element()` from the `<algorithm>` library.
>
> ```
>     int mn = *min_element(v.begin(), v.end());
>     int mx = *max_element(v.begin(), v.end());
> //Both min_element() and max_element() take O(n) time, where n is the number of elements.
> ```

## Time Complexity

**Time Complexity** measures how the runtime of an algorithm scales as the input size (N) grows. It does not measure absolute seconds, as that depends on hardware; instead, it counts the total number of fundamental operations executed.

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
> - **O(N^2) Quadratic:** Every element interacts with every other element. Usually causes a "Time Limit Exceeded" (TLE) error on LeetCode for inputs larger than 10^4.  
> *Examples:* Double nested loops, Bubble Sort, Selection Sort.
> - **O(2^N) Exponential:** The runtime doubles with every single addition to the input.  
> *Examples:* Unoptimized branching recursion (like naive Fibonacci), generating all subsets of a set.

# Range based for loops in C++

Range-based loops provide an easier way to traverse containers like vectors, arrays, maps, etc., without using indices or iterators.

### 1. Without Reference (`&`)

```
for (int value : v) {
    cout << value << " ";
}
```

- A **copy** of each element is stored in `value`.
- Any modification affects only the copy, not the original vector.

```
for (int value : v) {
    value++;  // Original vector remains unchanged
}
```

### 2. With Reference (`&`)

```
for (int &value : v) {
    value++;
}
```

- `value` becomes a reference to the actual element.
- Changes directly affect the original vector.
- No unnecessary copying takes place.

### 3. With Constant Reference

```
for (const int &value : v) {
    cout << value << " ";
}
```

- Avoids copying.
- Does not allow modification of original elements.

**Quick comparison:**


| Syntax             | Meaning                |
| ------------------ | ---------------------- |
| `int value`        | Copy                   |
| `int &value`       | Reference (modifiable) |
| `const int &value` | Reference (read-only)  |


---

## Traversing maps in C++

A map stores elements as key-value pairs.

- `first` → Key
- `second` → Value

### 1. Range-Based Loop

```
for (auto &itr : mp) {
    cout << itr.first << " " << itr.second;
}
```

- `auto` automatically determines the data type.
- `&` avoids copying and allows modification of values.
- `itr.first` accesses the key.
- `itr.second` accesses the value.

**Example:**

```
for (auto &itr : mp) {
    itr.second++;  // Modifies original map
}
```

**Note:** Map keys are immutable, but values can be modified.

### 2. Accessing Pairs Using Iterators

When an iterator points to a pair, we can access its members using:

```
itr->first   // Key
itr->second  // Value
```

This is equivalent to:

```
(*itr).first
(*itr).second
```

**Example:**

```
for (auto itr = mp.begin(); itr != mp.end(); itr++) {
    cout << itr->first << " " << itr->second;
}
```

# Standard Template Library

---

Here's a table that might come in very handy to understand the syntax and complexities of common functions that are associated with different data structures and might just be what you need:


| Function                    | Description                                                           | Data Structure &amp; Time Complexity                | Example &amp; Output                                                                                          |
| --------------------------- | --------------------------------------------------------------------- | --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| std::find                   | Finds first occurrence of a value in a range                          | string **(Time Complexity = O(N))**                 | `string s="hello"; cout<<(find(s.begin(),s.end(),'l')-s.begin());` Output: 2                                  |
| std::find                   | Finds first occurrence of a value in a range                          | array **(Time Complexity = O(N))**                  | `array<int,3> a={1,2,3}; cout<<(find(a.begin(),a.end(),3)-a.begin());` Output: 2                              |
| std::find                   | Finds first occurrence of a value in a range                          | vector **(Time Complexity = O(N))**                 | `vector<int> v={1,2,3,2}; cout<<(find(v.begin(),v.end(),2)!=v.end()?"Found":"Not Found");` Output: Found      |
| find() member               | Iterator to a key, or end() if missing                                | map **(Time Complexity = O(log N))**                | `map<int,int> mp; mp[5]=10; cout<<(mp.find(5)!=mp.end()?"Found":"Missing");` Output: Found                    |
| find() member               | Iterator to a key, or end() if missing                                | unordered\_map **(Time Complexity = O(1) average)** | `unordered_map<int,int> um={{3,30}}; cout<<um.find(3)->second;` Output: 30                                    |
| find() member               | Iterator to a key, or end() if missing                                | set **(Time Complexity = O(log N))**                | `set<int> s={1,2}; cout<<(s.find(2)!=s.end()?"Found":"Missing");` Output: Found                               |
| std::count                  | Counts occurrences of a value in a range                              | string **(Time Complexity = O(N))**                 | `string s="banana"; cout<<count(s.begin(),s.end(),'a');` Output: 3                                            |
| std::count                  | Counts occurrences of a value in a range                              | array **(Time Complexity = O(N))**                  | `array<int,4> a={1,1,2,1}; cout<<count(a.begin(),a.end(),1);` Output: 3                                       |
| std::count                  | Counts occurrences of a value in a range                              | vector **(Time Complexity = O(N))**                 | `vector<int> v={1,2,2,3,2}; cout<<count(v.begin(),v.end(),2);` Output: 3                                      |
| count() member              | Returns number of elements matching a key (0 or 1)                    | map **(Time Complexity = O(log N))**                | `map<int,int> mp={{1,10}}; cout<<mp.count(1);` Output: 1                                                      |
| count() member              | Returns number of elements matching a key (0 or 1)                    | unordered\_map **(Time Complexity = O(1) average)** | `unordered_map<int,int> um={{1,10}}; cout<<um.count(1);` Output: 1                                            |
| count() member              | Returns number of elements matching a key (0 or 1)                    | set **(Time Complexity = O(log N))**                | `set<int> s={1,2,3}; cout<<s.count(2);` Output: 1                                                             |
| std::binary\_search         | Checks if a value exists in a sorted range (returns bool)             | string **(Time Complexity = O(log N))**             | `string s="abcxyz"; cout<<binary_search(s.begin(),s.end(),'c');` Output: 1                                    |
| std::binary\_search         | Checks if a value exists in a sorted range (returns bool)             | array **(Time Complexity = O(log N))**              | `array<int,4> a={1,3,5,7}; cout<<binary_search(a.begin(),a.end(),4);` Output: 0                               |
| std::binary\_search         | Checks if a value exists in a sorted range (returns bool)             | vector **(Time Complexity = O(log N))**             | `vector<int> v={1,3,5,7}; cout<<(binary_search(v.begin(),v.end(),5)?"Yes":"No");` Output: Yes                 |
| std::lower\_bound           | Iterator to first element greater than or equal to the value          | string **(Time Complexity = O(log N))**             | `string s="acegik"; cout<<*lower_bound(s.begin(),s.end(),'d');` Output: e                                     |
| std::lower\_bound           | Iterator to first element greater than or equal to the value          | array **(Time Complexity = O(log N))**              | `array<int,4> a={1,3,5,7}; cout<<*lower_bound(a.begin(),a.end(),3);` Output: 3                                |
| std::lower\_bound           | Iterator to first element greater than or equal to the value          | vector **(Time Complexity = O(log N))**             | `vector<int> v={1,3,5,7}; cout<<*lower_bound(v.begin(),v.end(),4);` Output: 5                                 |
| lower\_bound() member       | Iterator to first element with key greater than or equal to key       | map **(Time Complexity = O(log N))**                | `map<int,string> mp={{1,"a"},{5,"b"}}; cout<<mp.lower_bound(3)->second;` Output: b                            |
| lower\_bound() member       | Iterator to first element greater than or equal to key                | set **(Time Complexity = O(log N))**                | `set<int> s={1,3,5,7}; cout<<*s.lower_bound(4);` Output: 5                                                    |
| std::upper\_bound           | Iterator to first element strictly greater than the value             | string **(Time Complexity = O(log N))**             | `string s="acegik"; cout<<*upper_bound(s.begin(),s.end(),'e');` Output: g                                     |
| std::upper\_bound           | Iterator to first element strictly greater than the value             | array **(Time Complexity = O(log N))**              | `array<int,4> a={1,3,5,7}; cout<<*upper_bound(a.begin(),a.end(),1);` Output: 3                                |
| std::upper\_bound           | Iterator to first element strictly greater than the value             | vector **(Time Complexity = O(log N))**             | `vector<int> v={1,3,5,7}; cout<<*upper_bound(v.begin(),v.end(),5);` Output: 7                                 |
| upper\_bound() member       | Iterator to first element with key strictly greater than key          | map **(Time Complexity = O(log N))**                | `map<int,string> mp={{1,"a"},{5,"b"}}; cout<<mp.upper_bound(1)->second;` Output: b                            |
| upper\_bound() member       | Iterator to first element strictly greater than key                   | set **(Time Complexity = O(log N))**                | `set<int> s={1,3,5,7}; cout<<*s.upper_bound(5);` Output: 7                                                    |
| std::find\_if               | Finds first element satisfying a predicate                            | string **(Time Complexity = O(N))**                 | `string s="abCd"; cout<<*find_if(s.begin(),s.end(),[](char c){return isupper(c);});` Output: C                |
| std::find\_if               | Finds first element satisfying a predicate                            | array **(Time Complexity = O(N))**                  | `array<int,3> a={1,5,8}; cout<<*find_if(a.begin(),a.end(),[](int x){return x>4;});` Output: 5                 |
| std::find\_if               | Finds first element satisfying a predicate                            | vector **(Time Complexity = O(N))**                 | `vector<int> v={1,3,4,7}; cout<<*find_if(v.begin(),v.end(),[](int x){return x%2==0;});` Output: 4             |
| std::min\_element           | Iterator to smallest element in a range                               | string **(Time Complexity = O(N))**                 | `string s="hello"; cout<<*min_element(s.begin(),s.end());` Output: e                                          |
| std::min\_element           | Iterator to smallest element in a range                               | array **(Time Complexity = O(N))**                  | `array<int,3> a={5,2,9}; cout<<*min_element(a.begin(),a.end());` Output: 2                                    |
| std::min\_element           | Iterator to smallest element in a range                               | vector **(Time Complexity = O(N))**                 | `vector<int> v={4,1,8,3}; cout<<*min_element(v.begin(),v.end());` Output: 1                                   |
| std::min\_element (index)   | Index of smallest element (subtract begin)                            | vector **(Time Complexity = O(N))**                 | `vector<int> v={4,1,8,3}; cout<<(min_element(v.begin(),v.end())-v.begin());` Output: 1                        |
| std::max\_element           | Iterator to largest element in a range                                | string **(Time Complexity = O(N))**                 | `string s="hello"; cout<<*max_element(s.begin(),s.end());` Output: o                                          |
| std::max\_element           | Iterator to largest element in a range                                | array **(Time Complexity = O(N))**                  | `array<int,3> a={5,2,9}; cout<<*max_element(a.begin(),a.end());` Output: 9                                    |
| std::max\_element           | Iterator to largest element in a range                                | vector **(Time Complexity = O(N))**                 | `vector<int> v={4,1,8,3}; cout<<*max_element(v.begin(),v.end());` Output: 8                                   |
| std::sort                   | Sorts a range in ascending order (introsort)                          | string **(Time Complexity = O(N log N))**           | `string s="dcba"; sort(s.begin(),s.end()); cout<<s;` Output: abcd                                             |
| std::sort                   | Sorts a range in ascending order (introsort)                          | array **(Time Complexity = O(N log N))**            | `array<int,3> a={3,1,2}; sort(a.begin(),a.end()); cout<<a[0];` Output: 1                                      |
| std::sort                   | Sorts a range in ascending order (introsort)                          | vector **(Time Complexity = O(N log N))**           | `vector<int> v={4,1,3}; sort(v.begin(),v.end()); cout<<v[0]<<" "<<v[2];` Output: 1 4                          |
| std::sort (descending)      | Sorts a range in descending order using a comparator                  | vector **(Time Complexity = O(N log N))**           | `vector<int> v={4,1,3}; sort(v.begin(),v.end(),greater<int>()); cout<<v[0];` Output: 4                        |
| std::sort (pairs)           | Sorts pairs by first, then second                                     | vector **(Time Complexity = O(N log N))**           | `vector<pair<int,int>> v={{2,1},{1,5}}; sort(v.begin(),v.end()); cout<<v[0].first;` Output: 1                 |
| std::reverse                | Reverses a range in place                                             | string **(Time Complexity = O(N))**                 | `string s="abc"; reverse(s.begin(),s.end()); cout<<s;` Output: cba                                            |
| std::reverse                | Reverses a range in place                                             | array **(Time Complexity = O(N))**                  | `array<int,3> a={1,2,3}; reverse(a.begin(),a.end()); cout<<a[0];` Output: 3                                   |
| std::reverse                | Reverses a range in place                                             | vector **(Time Complexity = O(N))**                 | `vector<int> v={1,2,3}; reverse(v.begin(),v.end()); cout<<v[0];` Output: 3                                    |
| std::rotate                 | Left-rotates so the middle iterator becomes the first element         | string **(Time Complexity = O(N))**                 | `string s="abcd"; rotate(s.begin(),s.begin()+1,s.end()); cout<<s;` Output: bcda                               |
| std::rotate                 | Left-rotates so the middle iterator becomes the first element         | array **(Time Complexity = O(N))**                  | `array<int,3> a={1,2,3}; rotate(a.begin(),a.begin()+2,a.end()); cout<<a[0];` Output: 3                        |
| std::rotate                 | Left-rotates so the middle iterator becomes the first element         | vector **(Time Complexity = O(N))**                 | `vector<int> v={1,2,3,4}; rotate(v.begin(),v.begin()+1,v.end()); cout<<v[0];` Output: 2                       |
| std::is\_sorted             | Checks if a range is in non-decreasing order                          | string **(Time Complexity = O(N))**                 | `string s="abc"; cout<<is_sorted(s.begin(),s.end());` Output: 1                                               |
| std::is\_sorted             | Checks if a range is in non-decreasing order                          | array **(Time Complexity = O(N))**                  | `array<int,3> a={3,1,2}; cout<<is_sorted(a.begin(),a.end());` Output: 0                                       |
| std::is\_sorted             | Checks if a range is in non-decreasing order                          | vector **(Time Complexity = O(N))**                 | `vector<int> v={1,2,3}; cout<<(is_sorted(v.begin(),v.end())?"Sorted":"No");` Output: Sorted                   |
| size()                      | Number of characters                                                  | string **(Time Complexity = O(1))**                 | `string s="hello"; cout<<s.size();` Output: 5                                                                 |
| size()                      | Number of elements (fixed at compile time)                            | array **(Time Complexity = O(1))**                  | `array<int,3> a={1,2,3}; cout<<a.size();` Output: 3                                                           |
| size()                      | Number of elements stored                                             | vector **(Time Complexity = O(1))**                 | `vector<int> v={1,2,3}; cout<<v.size();` Output: 3                                                            |
| size()                      | Number of key-value pairs                                             | map **(Time Complexity = O(1))**                    | `map<int,int> mp={{1,1},{2,2}}; cout<<mp.size();` Output: 2                                                   |
| size()                      | Number of key-value pairs                                             | unordered\_map **(Time Complexity = O(1))**         | `unordered_map<int,int> um={{1,1}}; cout<<um.size();` Output: 1                                               |
| size()                      | Number of unique elements                                             | set **(Time Complexity = O(1))**                    | `set<int> s={1,2,2}; cout<<s.size();` Output: 2                                                               |
| size()                      | Number of elements stored                                             | stack **(Time Complexity = O(1))**                  | `stack<int> st; st.push(1); cout<<st.size();` Output: 1                                                       |
| size()                      | Number of elements stored                                             | queue **(Time Complexity = O(1))**                  | `queue<int> q; q.push(1); q.push(2); cout<<q.size();` Output: 2                                               |
| empty()                     | True if string has no characters                                      | string **(Time Complexity = O(1))**                 | `string s="a"; cout<<s.empty();` Output: 0                                                                    |
| empty()                     | True if container has no elements                                     | array **(Time Complexity = O(1))**                  | `array<int,3> a={1,2,3}; cout<<a.empty();` Output: 0                                                          |
| empty()                     | True if container has no elements                                     | vector **(Time Complexity = O(1))**                 | `vector<int> v; cout<<v.empty();` Output: 1                                                                   |
| empty()                     | True if container has no elements                                     | map **(Time Complexity = O(1))**                    | `map<int,int> mp; cout<<mp.empty();` Output: 1                                                                |
| empty()                     | True if container has no elements                                     | unordered\_map **(Time Complexity = O(1))**         | `unordered_map<int,int> um; cout<<um.empty();` Output: 1                                                      |
| empty()                     | True if container has no elements                                     | set **(Time Complexity = O(1))**                    | `set<int> s; cout<<s.empty();` Output: 1                                                                      |
| empty()                     | True if container has no elements                                     | stack **(Time Complexity = O(1))**                  | `stack<int> s; cout<<(s.empty()?"Yes":"No");` Output: Yes                                                     |
| empty()                     | True if container has no elements                                     | queue **(Time Complexity = O(1))**                  | `queue<int> q; q.push(1); cout<<q.empty();` Output: 0                                                         |
| insert()                    | Inserts text at an index                                              | string **(Time Complexity = O(N))**                 | `string s="ac"; s.insert(1,"b"); cout<<s;` Output: abc                                                        |
| insert()                    | Inserts value at an iterator position                                 | vector **(Time Complexity = O(N))**                 | `vector<int> v={1,3}; v.insert(v.begin()+1,2); cout<<v[1];` Output: 2                                         |
| insert()                    | Inserts a key-value pair                                              | map **(Time Complexity = O(log N))**                | `map<int,int> mp; mp.insert({1,10}); cout<<mp[1];` Output: 10                                                 |
| insert()                    | Inserts a key-value pair                                              | unordered\_map **(Time Complexity = O(1) average)** | `unordered_map<int,int> um; um.insert({2,20}); cout<<um[2];` Output: 20                                       |
| insert()                    | Inserts a unique key                                                  | set **(Time Complexity = O(log N))**                | `set<int> st; st.insert(10); cout<<st.count(10);` Output: 1                                                   |
| push\_back()                | Appends a character at the end                                        | string **(Time Complexity = O(1) amortized)**       | `string s="ab"; s.push_back('c'); cout<<s;` Output: abc                                                       |
| push\_back()                | Appends an element at the end                                         | vector **(Time Complexity = O(1) amortized)**       | `vector<int> v; v.push_back(5); cout<<v[0];` Output: 5                                                        |
| pop\_back()                 | Removes the last character                                            | string **(Time Complexity = O(1))**                 | `string s="abc"; s.pop_back(); cout<<s;` Output: ab                                                           |
| pop\_back()                 | Removes the last element                                              | vector **(Time Complexity = O(1))**                 | `vector<int> v={1,2}; v.pop_back(); cout<<v.size();` Output: 1                                                |
| push()                      | Pushes an element on top (LIFO)                                       | stack **(Time Complexity = O(1))**                  | `stack<int> s; s.push(1); s.push(2); cout<<s.top();` Output: 2                                                |
| push()                      | Adds an element at the back (FIFO)                                    | queue **(Time Complexity = O(1))**                  | `queue<int> q; q.push(10); q.push(20); cout<<q.back();` Output: 20                                            |
| pop()                       | Removes the top element                                               | stack **(Time Complexity = O(1))**                  | `stack<int> s; s.push(1); s.push(2); s.pop(); cout<<s.top();` Output: 1                                       |
| pop()                       | Removes the front element                                             | queue **(Time Complexity = O(1))**                  | `queue<int> q; q.push(10); q.push(20); q.pop(); cout<<q.front();` Output: 20                                  |
| erase()                     | Removes characters by index and count                                 | string **(Time Complexity = O(N))**                 | `string s="abc"; s.erase(1,1); cout<<s;` Output: ac                                                           |
| erase()                     | Removes element at an iterator                                        | vector **(Time Complexity = O(N))**                 | `vector<int> v={1,2,3}; v.erase(v.begin()+1); cout<<v[1];` Output: 3                                          |
| erase()                     | Removes a key and its value                                           | map **(Time Complexity = O(log N))**                | `map<int,int> mp={{1,1},{2,2}}; mp.erase(1); cout<<mp.size();` Output: 1                                      |
| erase()                     | Removes a key and its value                                           | unordered\_map **(Time Complexity = O(1) average)** | `unordered_map<int,int> um={{1,1}}; um.erase(1); cout<<um.size();` Output: 0                                  |
| erase()                     | Removes a key                                                         | set **(Time Complexity = O(log N))**                | `set<int> st={1,2}; st.erase(1); cout<<st.size();` Output: 1                                                  |
| clear()                     | Removes all characters                                                | string **(Time Complexity = O(N))**                 | `string s="abc"; s.clear(); cout<<s.size();` Output: 0                                                        |
| clear()                     | Removes all elements                                                  | vector **(Time Complexity = O(N))**                 | `vector<int> v={1,2}; v.clear(); cout<<v.empty();` Output: 1                                                  |
| clear()                     | Removes all key-value pairs                                           | map **(Time Complexity = O(N))**                    | `map<int,int> mp={{1,1}}; mp.clear(); cout<<mp.size();` Output: 0                                             |
| clear()                     | Removes all key-value pairs                                           | unordered\_map **(Time Complexity = O(N))**         | `unordered_map<int,int> um={{1,1}}; um.clear(); cout<<um.empty();` Output: 1                                  |
| clear()                     | Removes all elements                                                  | set **(Time Complexity = O(N))**                    | `set<int> s={1,2}; s.clear(); cout<<s.size();` Output: 0                                                      |
| front()                     | Reference to the first character                                      | string **(Time Complexity = O(1))**                 | `string s="hello"; cout<<s.front();` Output: h                                                                |
| front()                     | Reference to the first element                                        | array **(Time Complexity = O(1))**                  | `array<int,2> a={10,20}; cout<<a.front();` Output: 10                                                         |
| front()                     | Reference to the first element                                        | vector **(Time Complexity = O(1))**                 | `vector<int> v={10,20}; cout<<v.front();` Output: 10                                                          |
| front()                     | Reference to the oldest element                                       | queue **(Time Complexity = O(1))**                  | `queue<int> q; q.push(10); q.push(20); cout<<q.front();` Output: 10                                           |
| back()                      | Reference to the last character                                       | string **(Time Complexity = O(1))**                 | `string s="hello"; cout<<s.back();` Output: o                                                                 |
| back()                      | Reference to the last element                                         | array **(Time Complexity = O(1))**                  | `array<int,2> a={10,20}; cout<<a.back();` Output: 20                                                          |
| back()                      | Reference to the last element                                         | vector **(Time Complexity = O(1))**                 | `vector<int> v={10,20}; cout<<v.back();` Output: 20                                                           |
| back()                      | Reference to the newest element                                       | queue **(Time Complexity = O(1))**                  | `queue<int> q; q.push(10); q.push(20); cout<<q.back();` Output: 20                                            |
| top()                       | Reference to the top element                                          | stack **(Time Complexity = O(1))**                  | `stack<int> s; s.push(42); cout<<s.top();` Output: 42                                                         |
| at()                        | Character at index with bounds checking                               | string **(Time Complexity = O(1))**                 | `string s="abc"; cout<<s.at(2);` Output: c                                                                    |
| at()                        | Element at index or key with bounds checking (throws out\_of\_range)  | array **(Time Complexity = O(1))**                  | `array<int,2> a={10,20}; cout<<a.at(0);` Output: 10                                                           |
| at()                        | Element at index or key with bounds checking (throws out\_of\_range)  | vector **(Time Complexity = O(1))**                 | `vector<int> v={10,20}; cout<<v.at(1);` Output: 20                                                            |
| at()                        | Value for a key (throws if the key is missing)                        | map **(Time Complexity = O(log N))**                | `map<string,int> mp={{"a",5}}; cout<<mp.at("a");` Output: 5                                                   |
| at()                        | Value for a key (throws if the key is missing)                        | unordered\_map **(Time Complexity = O(1) average)** | `unordered_map<string,int> um={{"a",5}}; cout<<um.at("a");` Output: 5                                         |
| swap()                      | Exchanges contents of two containers                                  | string **(Time Complexity = O(1))**                 | `string a="x", b="y"; a.swap(b); cout<<a;` Output: y                                                          |
| swap()                      | Exchanges contents of two arrays (element-wise)                       | array **(Time Complexity = O(N))**                  | `array<int,1> a={1}, b={2}; a.swap(b); cout<<a[0];` Output: 2                                                 |
| swap()                      | Exchanges contents of two containers                                  | vector **(Time Complexity = O(1))**                 | `vector<int> a={1}, b={2}; a.swap(b); cout<<a[0];` Output: 2                                                  |
| swap()                      | Exchanges contents of two containers                                  | map **(Time Complexity = O(1))**                    | `map<int,int> a={{1,1}}, b; a.swap(b); cout<<a.size();` Output: 0                                             |
| swap()                      | Exchanges contents of two containers                                  | unordered\_map **(Time Complexity = O(1))**         | `unordered_map<int,int> a={{1,1}}, b; a.swap(b); cout<<a.size();` Output: 0                                   |
| swap()                      | Exchanges contents of two containers                                  | set **(Time Complexity = O(1))**                    | `set<int> a={1}, b={2}; a.swap(b); cout<<*a.begin();` Output: 2                                               |
| swap()                      | Exchanges contents of two containers                                  | stack **(Time Complexity = O(1))**                  | `stack<int> a, b; b.push(9); a.swap(b); cout<<a.top();` Output: 9                                             |
| swap()                      | Exchanges contents of two containers                                  | queue **(Time Complexity = O(1))**                  | `queue<int> a, b; b.push(9); a.swap(b); cout<<a.front();` Output: 9                                           |
| std::equal                  | Compares two ranges element by element                                | string **(Time Complexity = O(N))**                 | `string a="abc", b="abc"; cout<<equal(a.begin(),a.end(),b.begin());` Output: 1                                |
| std::equal                  | Compares two ranges element by element                                | array **(Time Complexity = O(N))**                  | `array<int,2> a={1,2}, b={1,3}; cout<<equal(a.begin(),a.end(),b.begin());` Output: 0                          |
| std::equal                  | Compares two ranges element by element                                | vector **(Time Complexity = O(N))**                 | `vector<int> a={1,2}, b={1,2}; cout<<(equal(a.begin(),a.end(),b.begin())?"Equal":"Diff");` Output: Equal      |
| std::accumulate             | Sums elements starting from an initial value (numeric header)         | array **(Time Complexity = O(N))**                  | `array<int,3> a={1,2,3}; cout<<accumulate(a.begin(),a.end(),0);` Output: 6                                    |
| std::accumulate             | Sums elements starting from an initial value (numeric header)         | vector **(Time Complexity = O(N))**                 | `vector<int> v={1,2,3}; cout<<accumulate(v.begin(),v.end(),0);` Output: 6                                     |
| std::accumulate (long long) | Sums into long long to avoid overflow                                 | vector **(Time Complexity = O(N))**                 | `vector<int> v={2000000000,2000000000}; cout<<accumulate(v.begin(),v.end(),0LL);` Output: 4000000000          |
| std::accumulate (product)   | Product using multiplies (functional header)                          | vector **(Time Complexity = O(N))**                 | `vector<int> v={2,3,4}; cout<<accumulate(v.begin(),v.end(),1,multiplies<int>());` Output: 24                  |
| std::accumulate             | Sums elements starting from an initial value (numeric header)         | set **(Time Complexity = O(N))**                    | `set<int> s={1,2,3}; cout<<accumulate(s.begin(),s.end(),0);` Output: 6                                        |
| mp\[key\]                   | Accesses or inserts a key (default-initializes the value if missing)  | map **(Time Complexity = O(log N))**                | `map<string,int> mp; mp["score"]=95; cout<<mp["score"];` Output: 95                                           |
| mp\[key\]                   | Accesses or inserts a key (default-initializes the value if missing)  | unordered\_map **(Time Complexity = O(1) average)** | `unordered_map<string,int> um; um["a"]++; cout<<um["a"];` Output: 1                                           |
| contains()                  | Checks if a key exists (C++20)                                        | map **(Time Complexity = O(log N))**                | `map<int,int> mp={{1,1}}; cout<<mp.contains(5);` Output: 0                                                    |
| contains()                  | Checks if a key exists (C++20)                                        | unordered\_map **(Time Complexity = O(1) average)** | `unordered_map<int,int> um={{1,1}}; cout<<um.contains(1);` Output: 1                                          |
| contains()                  | Checks if a key exists (C++20)                                        | set **(Time Complexity = O(log N))**                | `set<int> s={1,2}; cout<<(s.contains(2)?"Yes":"No");` Output: Yes                                             |
| std::for\_each              | Applies a function to every element in a range                        | string **(Time Complexity = O(N))**                 | `string s="ab"; for_each(s.begin(),s.end(),[](char c){cout<<c<<" ";});` Output: a b                           |
| std::for\_each              | Applies a function to every element in a range                        | array **(Time Complexity = O(N))**                  | `array<int,2> a={3,4}; for_each(a.begin(),a.end(),[](int x){cout<<x<<" ";});` Output: 3 4                     |
| std::for\_each              | Applies a function to every element in a range                        | vector **(Time Complexity = O(N))**                 | `vector<int> v={1,2}; for_each(v.begin(),v.end(),[](int x){cout<<x<<" ";});` Output: 1 2                      |
| std::for\_each              | Applies a function to every element in a range                        | set **(Time Complexity = O(N))**                    | `set<int> s={5,6}; for_each(s.begin(),s.end(),[](int x){cout<<x<<" ";});` Output: 5 6                         |
| std::copy                   | Copies a range into a destination                                     | string **(Time Complexity = O(N))**                 | `string s="ab", d(2,'x'); copy(s.begin(),s.end(),d.begin()); cout<<d;` Output: ab                             |
| std::copy                   | Copies a range into a destination                                     | array **(Time Complexity = O(N))**                  | `array<int,2> s={1,2}, d; copy(s.begin(),s.end(),d.begin()); cout<<d[0];` Output: 1                           |
| std::copy                   | Copies a range into a destination                                     | vector **(Time Complexity = O(N))**                 | `vector<int> s={1,2}, d(2); copy(s.begin(),s.end(),d.begin()); cout<<d[1];` Output: 2                         |
| std::copy                   | Copies a range into a destination                                     | set **(Time Complexity = O(N))**                    | `set<int> s={1,2}; vector<int> d(2); copy(s.begin(),s.end(),d.begin()); cout<<d[1];` Output: 2                |
| std::find\_if               | Finds first element satisfying a predicate                            | set **(Time Complexity = O(N))**                    | `set<int> s={1,5,8}; cout<<*find_if(s.begin(),s.end(),[](int x){return x>4;});` Output: 5                     |
| std::min\_element           | Iterator to smallest element in a range                               | set **(Time Complexity = O(N))**                    | `set<int> s={5,2,9}; cout<<*min_element(s.begin(),s.end());` Output: 2                                        |
| std::max\_element           | Iterator to largest element in a range                                | set **(Time Complexity = O(N))**                    | `set<int> s={5,2,9}; cout<<*max_element(s.begin(),s.end());` Output: 9                                        |
| std::is\_sorted             | Checks if a range is in non-decreasing order (a set is always sorted) | set **(Time Complexity = O(N))**                    | `set<int> s={3,1,2}; cout<<is_sorted(s.begin(),s.end());` Output: 1                                           |
| std::equal                  | Compares two ranges element by element                                | set **(Time Complexity = O(N))**                    | `set<int> a={1,2}, b={1,2}; cout<<equal(a.begin(),a.end(),b.begin());` Output: 1                              |
| std::count\_if              | Counts elements satisfying a predicate                                | string **(Time Complexity = O(N))**                 | `string s="aBcD"; cout<<count_if(s.begin(),s.end(),[](char c){return isupper(c);});` Output: 2                |
| std::count\_if              | Counts elements satisfying a predicate                                | array **(Time Complexity = O(N))**                  | `array<int,4> a={1,2,3,4}; cout<<count_if(a.begin(),a.end(),[](int x){return x%2==0;});` Output: 2            |
| std::count\_if              | Counts elements satisfying a predicate                                | vector **(Time Complexity = O(N))**                 | `vector<int> v={1,5,8,10}; cout<<count_if(v.begin(),v.end(),[](int x){return x>4;});` Output: 3               |
| std::all\_of                | True if every element satisfies a predicate                           | vector **(Time Complexity = O(N))**                 | `vector<int> v={2,4,6}; cout<<all_of(v.begin(),v.end(),[](int x){return x%2==0;});` Output: 1                 |
| std::any\_of                | True if at least one element satisfies a predicate                    | vector **(Time Complexity = O(N))**                 | `vector<int> v={1,3,4}; cout<<any_of(v.begin(),v.end(),[](int x){return x%2==0;});` Output: 1                 |
| std::none\_of               | True if no element satisfies a predicate                              | vector **(Time Complexity = O(N))**                 | `vector<int> v={1,3,5}; cout<<none_of(v.begin(),v.end(),[](int x){return x%2==0;});` Output: 1                |
| std::fill                   | Assigns a value to every element in a range                           | string **(Time Complexity = O(N))**                 | `string s="abc"; fill(s.begin(),s.end(),'x'); cout<<s;` Output: xxx                                           |
| std::fill                   | Assigns a value to every element in a range                           | array **(Time Complexity = O(N))**                  | `array<int,3> a; fill(a.begin(),a.end(),7); cout<<a[2];` Output: 7                                            |
| std::fill                   | Assigns a value to every element in a range                           | vector **(Time Complexity = O(N))**                 | `vector<int> v(3); fill(v.begin(),v.end(),7); cout<<v[0];` Output: 7                                          |
| std::iota                   | Fills a range with increasing values (numeric header)                 | vector **(Time Complexity = O(N))**                 | `vector<int> v(3); iota(v.begin(),v.end(),1); cout<<v[2];` Output: 3                                          |
| std::transform              | Applies a function to each element and stores the result              | vector **(Time Complexity = O(N))**                 | `vector<int> v={1,2,3}; transform(v.begin(),v.end(),v.begin(),[](int x){return x*2;}); cout<<v[2];` Output: 6 |
| std::unique (with erase)    | Removes consecutive duplicates (sort first to remove all duplicates)  | string **(Time Complexity = O(N))**                 | `string s="aabbc"; s.erase(unique(s.begin(),s.end()),s.end()); cout<<s;` Output: abc                          |
| std::unique (with erase)    | Removes consecutive duplicates (sort first to remove all duplicates)  | vector **(Time Complexity = O(N))**                 | `vector<int> v={1,1,2,2,3}; v.erase(unique(v.begin(),v.end()),v.end()); cout<<v.size();` Output: 3            |
| std::remove (erase-remove)  | Removes all elements equal to a value                                 | vector **(Time Complexity = O(N))**                 | `vector<int> v={1,2,3,2}; v.erase(remove(v.begin(),v.end(),2),v.end()); cout<<v.size();` Output: 2            |
| std::next\_permutation      | Rearranges to the next lexicographic permutation                      | string **(Time Complexity = O(N))**                 | `string s="abc"; next_permutation(s.begin(),s.end()); cout<<s;` Output: acb                                   |
| emplace\_back()             | Constructs an element in place at the end                             | vector **(Time Complexity = O(1) amortized)**       | `vector<pair<int,int>> v; v.emplace_back(1,2); cout<<v[0].second;` Output: 2                                  |
| resize()                    | Changes the number of elements (new ones are default-initialized)     | vector **(Time Complexity = O(N))**                 | `vector<int> v={1,2}; v.resize(4); cout<<v.size();` Output: 4                                                 |
| find() member               | Iterator to a key, or end() if missing                                | unordered\_set **(Time Complexity = O(1) average)** | `unordered_set<int> us={1,2}; cout<<(us.find(2)!=us.end()?"Found":"Missing");` Output: Found                  |
| count() member              | Returns number of elements matching a key (0 or 1)                    | unordered\_set **(Time Complexity = O(1) average)** | `unordered_set<int> us={1,2}; cout<<us.count(2);` Output: 1                                                   |
| insert()                    | Inserts a unique key                                                  | unordered\_set **(Time Complexity = O(1) average)** | `unordered_set<int> us; us.insert(5); cout<<us.count(5);` Output: 1                                           |
| erase()                     | Removes a key                                                         | unordered\_set **(Time Complexity = O(1) average)** | `unordered_set<int> us={1,2}; us.erase(1); cout<<us.size();` Output: 1                                        |
| size()                      | Number of unique elements                                             | unordered\_set **(Time Complexity = O(1))**         | `unordered_set<int> us={1,2,2}; cout<<us.size();` Output: 2                                                   |
| empty()                     | True if container has no elements                                     | unordered\_set **(Time Complexity = O(1))**         | `unordered_set<int> us; cout<<us.empty();` Output: 1                                                          |
| clear()                     | Removes all elements                                                  | unordered\_set **(Time Complexity = O(N))**         | `unordered_set<int> us={1,2}; us.clear(); cout<<us.size();` Output: 0                                         |
| contains()                  | Checks if a key exists (C++20)                                        | unordered\_set **(Time Complexity = O(1) average)** | `unordered_set<int> us={1,2}; cout<<us.contains(3);` Output: 0                                                |
| swap()                      | Exchanges contents of two containers                                  | unordered\_set **(Time Complexity = O(1))**         | `unordered_set<int> a={1}, b={2}; a.swap(b); cout<<*a.begin();` Output: 2                                     |
| push\_back()                | Appends an element at the back                                        | deque **(Time Complexity = O(1))**                  | `deque<int> d; d.push_back(5); cout<<d.back();` Output: 5                                                     |
| push\_front()               | Inserts an element at the front                                       | deque **(Time Complexity = O(1))**                  | `deque<int> d; d.push_back(2); d.push_front(1); cout<<d.front();` Output: 1                                   |
| pop\_back()                 | Removes the last element                                              | deque **(Time Complexity = O(1))**                  | `deque<int> d={1,2}; d.pop_back(); cout<<d.back();` Output: 1                                                 |
| pop\_front()                | Removes the first element                                             | deque **(Time Complexity = O(1))**                  | `deque<int> d={1,2}; d.pop_front(); cout<<d.front();` Output: 2                                               |
| d\[i\]                      | Element at index (no bounds checking)                                 | deque **(Time Complexity = O(1))**                  | `deque<int> d={10,20,30}; cout<<d[1];` Output: 20                                                             |
| size()                      | Number of elements stored                                             | deque **(Time Complexity = O(1))**                  | `deque<int> d={1,2,3}; cout<<d.size();` Output: 3                                                             |
| empty()                     | True if container has no elements                                     | deque **(Time Complexity = O(1))**                  | `deque<int> d; cout<<d.empty();` Output: 1                                                                    |
| push()                      | Inserts an element and restores heap order (max-heap by default)      | priority\_queue **(Time Complexity = O(log N))**    | `priority_queue<int> pq; pq.push(3); pq.push(9); cout<<pq.top();` Output: 9                                   |
| top()                       | Reference to the highest-priority element                             | priority\_queue **(Time Complexity = O(1))**        | `priority_queue<int> pq; pq.push(4); pq.push(7); cout<<pq.top();` Output: 7                                   |
| pop()                       | Removes the highest-priority element                                  | priority\_queue **(Time Complexity = O(log N))**    | `priority_queue<int> pq; pq.push(3); pq.push(9); pq.pop(); cout<<pq.top();` Output: 3                         |
| push() (min-heap)           | Min-heap using greater comparator                                     | priority\_queue **(Time Complexity = O(log N))**    | `priority_queue<int,vector<int>,greater<int>> pq; pq.push(5); pq.push(2); cout<<pq.top();` Output: 2          |
| size()                      | Number of elements stored                                             | priority\_queue **(Time Complexity = O(1))**        | `priority_queue<int> pq; pq.push(1); pq.push(2); cout<<pq.size();` Output: 2                                  |
| empty()                     | True if container has no elements                                     | priority\_queue **(Time Complexity = O(1))**        | `priority_queue<int> pq; cout<<pq.empty();` Output: 1                                                         |


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
| Check a bit                   | `a & (1 << k)` — Checks whether the (k)-th bit is set; a nonzero result means it is set.        |     |
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
