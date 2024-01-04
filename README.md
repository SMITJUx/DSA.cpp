# C++ STL Toolbox

## Containers

### Sequence

\***\*Note: You may use a `std::list` if you need to keep iterators stability doing operations like insertion and deletion.\*\***

#### Vector

A `std::vector` is a sequence container that encapsulates dynamic sized arrays. The storage of the vector is handled automatically,
vectors usually occupy more space than static arrays. Also, the STL proves a specialization of `std::vector<bool>` which is space efficiently optimized.

|         Operation         | Time Complexity |
|:-------------------------:|:---------------:|
|          Access           |     $O(1)$      |
|          Insert           |     $O(n)$      |
| Insert (i = v.size() - 1) |     $O(1)$      |
|          Delete           |     $O(n)$      |
| Delete (i = v.size() - 1) |     $O(1)$      |

```c++
#include <vector>

int main() {
    std::vector<int> v({1, 2, 3, 4});

    std::size_t size   = v.size();    // Number of elements
    int         last   = v.back();    // Last element
    int         first  = v.front();   // First element
    int         second = v.at(1);     // Second element
    int*        data   = v.data();    // Access the underlying continuous storage
    bool        empty  = v.empty();   // Checks if the sequence is empty or not

    v.push_back(5);                 // Adds the element 5 at the end
    v.insert(v.begin() + 1, 10);    // Adds the element 10 at the index 1
    v.erase(v.begin() + 1);         // Removes the element at the index 1
    v.emplace(v.begin() + 1);       // Constructs an element at the index 1
    v.erase(v.begin() + 1);         // Removes the element at the index 1
    v.emplace_back();               // Constructs an element at the end
    v.pop_back();                   // Removes the last element
    v.clear();                      // Clear the vector by setting the size to 0

    return 0;
}
```

#### List

A `std::list` is a container that supports constant time insertion and removal of elements from anywhere in the container.
But it doesn't support a random access.

|         Operation         | Time Complexity |
|:-------------------------:|:---------------:|
|          Access           |     $O(n)$      |
|          Insert           |     $O(1)$      |
|          Delete           |     $O(1)$      |

```c++
#include <list>

int main() {
    std::list<int> li({1, 2, 3, 4});

    std::size_t size  = li.size();    // Number of elements
    int         last  = li.back();    // Last element
    int         first = li.front();   // First element
    bool        empty = li.empty();   // Checks if the sequence is empty or not

    li.push_front(0);                      // Adds the element 0 at the beginning
    li.push_back(5);                       // Adds the element 5 at the end
    li.insert(std::next(li.begin()), 10);  // Adds the element 10 as the second element
    li.erase(std::next(li.begin()));       // Removes the second element
    li.emplace(std::next(li.begin()));     // Constructs an element and add it as the second element
    li.erase(std::next(li.begin()));       // Removes the second element1
    li.emplace_back();                     // Constructs an element and add it at end
    li.emplace_front();                    // Constructs an element and add it at the beginning
    li.pop_back();                         // Removes the last element
    li.pop_front();                        // Removes the first element
    li.clear();                            // Removes all elements

    return 0;
}
```

#### Deque

```c++
#include <deque>

int main() {
    std::deque<int> li({1, 2, 3, 4});

    std::size_t size   = li.size();     // Number of elements
    int         last   = li.back();     // Last element
    int         first  = li.front();    // First element
    int         second = li[1];         // Second element
    int         third  = li.at(2);      // Thirds element access with bounds checking, throw std::out_of_range
    bool        empty  = li.empty();    // Checks if the sequence is empty or not

    li.push_front(0);                // Adds the element 0 at the beginning
    li.push_back(5);                 // Adds the element 5 at the end
    li.insert(li.begin() + 1, 10);   // Adds the element 10 at the index 1
    li.erase(li.begin() + 1);        // Removes the element at the index 1
    li.emplace_back();               // Constructs an element and add it at the end
    li.emplace_front();              // Constructs an element and add it at the beginning
    li.pop_back();                   // Removes the last element
    li.pop_front();                  // Removes the first element
    li.clear();                      // Removes all elements

    return 0;
}
```

### Associative

#### set & unordered_set

```c++
#include <set>

int main() {
    std::set<int, std::less<>> s({1, 2, 3, 4});  // The comparator can be passed as a template argument

    std::size_t size    = s.size();         // Number of elements
    int         count   = s.count(1);       // Returns the number of element with this key
    auto        it      = s.find(1);        // Returns an iterator to the key
    bool        contain = s.contains(1);    // Checks if the set contains the key
    bool        empty   = s.empty();        // Checks if the set is empty or not
    auto lowerBound     = s.lower_bound(2); // Returns an iterator to the first element not less than the key (>=)
    auto upperBound     = s.upper_bound(2); // Returns an iterator to the first element greater than the key (>)

    s.insert(5);               // Inserts the key 5;
    s.erase(5);                // Deletes the key 5
    s.emplace();               // Constructs an element
    s.merge(std::set({6, 7})); // Merges the keys from the rvalue with s (note: it will modify both set)
    s.clear();                 // Deletes the set content

    return 0;
}
```

#### map & unordered_map

```c++
#include <map>

int main() {
    std::map<int, int, std::less<>> m = { // The comparator can be passed as a template argument
            {1, 1},
            {2, 2},
            {3, 3}
    };

    std::size_t size  = m.size();               // Number of pairs
    bool        empty = m.empty();              // Checks if the map is empty or not
    int         x     = m[3];                   // Returns a reference to the value mapped to the key 3, performing an insertion if the key is not found!
    int         y     = m.at(3);                // Access the value mapped to the key 3, can return std::out_of_range
    int         count = m.count(1);             // Returns the number of element matching the key
    auto        it    = m.find(1);              // Returns an iterator to the specific key
    bool        contains = m.contains(1);       // Checks if the map contains the key
    auto        lowerBound = m.lower_bound(2);  // Returns an iterator to the first element not less than the key (>=)
    auto        upperBound = m.upper_bound(2);  // Returns an iterator to the first element greater than the key (>)

    auto p1 = m.insert({5, 5});             // Inserts a pair in the map and returns a pair containing an iterator to the value and a boolean set to true if there was an insertion
    if (p1.second) m.erase(p1.first);       // Deletes the added pair {5, 5}
    auto p2 = m.insert_or_assign(5, 5);     // Inserts or assigns the value to the key and return a pair with a bool set to true for insertion or false for assignment
    m.erase(p1.first);                      // Deletes the added pair {5, 5}
    m.merge(std::map<int, int>({{6, 6}}));  // Merges the keys from the rvalue with m (note: it will modify both set)
    m.clear();                              // Deletes the map content

    return 0;
}
```

### Adaptors

```c++

```

#### stack

```c++

```

#### queue

```c++

```

#### priority_queue

```c++

```

## Iterators

```c++
#include <vector>

int main() {
    std::vector<int> v({1, 2, 3, 4});

    auto l  = v.begin();  // Returns an iterator to the beginning
    auto r  = v.end();    // Returns an iterator to the end
    auto rl = v.rbegin(); // Returns a reverse iterator to the beginning
    auto rr = v.rend();   // Returns a reverse iterator to the end

    return 0;
}
```

## Algorithms

### Non-Modifying Sequence Operations

#### Batch Operations

```c++
#include <algorithm>
#include <vector>

int main() {
    std::vector<int> v({1, 2, 3, 4});

    std::for_each(v.begin(), v.end(), [](int& x) -> void {  // Applies a unary function on each element
        x *= 2;
    });
    std::for_each_n(v.begin(), 3, [](int& x) -> void {      // Applies a unary function on the first n elements
        x *= 2
    });

    return 0;
}
```

#### Search Operations

```c++
#include <algorithm>
#include <vector>

int main() {
    std::vector<int> v({1, 2, 3, 4});
    std::vector<int> w({1, 2});

    auto it1  = std::find(v.begin(), v.end(), 2);                                // Returns an iterator to the first element that match the value
    auto it2  = std::find_if(v.begin(), v.end(), [](const int& x) -> bool {      // Returns an iterator to the first element for which the predicate is true
        return x % 2 == 0;
    });
    auto it3  = std::find_if_not(v.begin(), v.end(), [](const int& x) -> bool {  // Returns an iterator to the first element for which the predicate is false
        return x % 2 == 0;
    });
    auto it4  = std::find_end(v.begin(), v.end(), w.begin(), w.end());           // Return an iterator to the last occurrence of the sequence w in v
    auto it5  = std::find_end(v.begin(), v.end(), w.begin(), w.end(), [](const int& a, const int& b) -> bool { // Return an iterator to the last occurrence of the sequence w in v
        a == b - 10;
    });
    auto it6  = std::find_first_of(v.begin(), v.end(), w.begin(), w.end());      // Returns an iterator to the first element from w find in v
    auto it7  = std::mismatch(v.begin(), v.end(), w.begin(), w.end());           // Returns an iterator to the first position where v and w differ
    auto it8  = std::search(v.begin(), v.end(), w.begin(), w.end());             // Returns an iterator to the first occurrence of w in v
    auto it9  = std::search_n(v.begin(), v.end(), 3, 1);                         // Returns an iterator to the first occurrence of 1 that appears 3 times consecutively
    auto it10 = std::adjacent_find(v.begin(), v.end());                          // Returns an iterator to the first pair of equal adjacent elements
    auto it11 = std::adjacent_find(v.begin(), v.end(), [](const int& a, const int& b) -> bool { // Returns an iterator to the first pair of equal adjacent elements using the binary function
        return a == b - 10;
    });

    bool b1 = std::all_of(v.begin(), v.end(), [](const int& x) -> bool {        // Checks if all elements verify the unary function
        return x % 2 == 0;
    });
    bool b2 = std::any_of(v.begin(), v.end(), [](const int& x) -> bool {        // Checks if at least one element verify the unary function
        return x % 2 == 0;
    });
    bool b3 = std::none_of(v.begin(), v.end(), [](const int& x) -> bool {       // Checks if none of the element verify the unary function
        return x % 2 == 0;
    });

    long c1 = std::count(v.begin(), v.end(), 3);                                // Counts the number of 3 in v
    long c2 = std::count_if(v.begin(), v.end(), [](const int& x) -> bool {      // Counts the number of element that verify the unary function
        return x % 2 == 0;
    });

    bool eq = std::equal(v.begin(), v.end(), w.begin(), w.end());               // Checks if two sequence are equal

    return 0;
}
```

### Modifying Sequence Operations

#### Copy Operations

```c++
#include <algorithm>
#include <vector>

int main() {
    std::vector<int> v({1, 2, 3, 4});
    std::vector<int> w(v.size());

    auto it1 = std::copy(v.begin(), v.end(), w.begin());                             // Copies v in w, if source and destination overlaps it is UB
    auto it2 = std::copy_if(v.begin(), v.end(), w.begin(), [](const int& x)-> bool { // Copies from v in w if the unary function is true
        return x % 2 == 0;
    });
    auto it3 = std::copy_n(v.begin(), 3, w.begin());                                 // Copies the first n element from v to w

    return 0;
}
```

#### Transform Operations

```c++
#include <algorithm>
#include <vector>

int main() {
    std::vector<int> v({1, 2, 3, 4});
    std::vector<int> w(v.size()));

    std::transform(v.begin(), v.end(), w.begin(), [](int& x) -> int {   // Applies the unary function and store the result in w
        return x *= 2;
    });
    std::replace(v.begin(), v.end(), 1, 10);                            // Replaces 1 with 10
    std::replace_if(v.begin(), v.end(), [](const int& x) -> bool {      // Replaces all even numbers by 10
        return x % 2 == 0;
    }, 10);
    std::replace_copy(v.begin(), v.end(), w.begin(), 1, 10);            // Copies and replaces in w
    std::replace_copy_if(v.begin(), v.end(), w.begin(), [](const int& x) -> bool { // Copies and replaces in w if unary predicate is true
        return x % 2 == 0;
    }, 10);

    return 0;
}
```

#### Removing Operations

```c++
#include <algorithm>
#include <vector>

int main() {
    std::vector<int> v({1, 2, 3, 4});
    std::vector<int> w(v.size()));

    auto it1 = std::remove(v.begin(), v.end(), 3);                           // Removes all the 3 and returns an iterator pointing to the start of the new sub-range
    auto it2 = std::remove_if(v.begin(), v.end(), [](const int& x) -> bool { // Removes all the element verifying the unary predicate and returns an iterator pointing to the start of the new sub-range
        return x % 2 == 0;
    });
    auto it3 = std::unique(v.begin(), v.end());                              // Removes consecutive duplicate elements and returns an iterator pointer to the start of the new sub-range

    return 0;
}
```

#### Order-Changing Operations

```c++
#include <algorithm>
#include <vector>

int main() {
    std::vector<int> v({1, 2, 3, 4});
    std::vector<int> w(v.size()));

    std::reverse(v.begin(), v.end());                               // Reverses v
    std::reverse_copy(v.begin(), v.end(), w.begin());               // Copies v into w and reverse w
    std::rotate(v.begin(), v.begin() + 1, v.end());                 // Rotates so the second element goes at the end of v
    std::rotate_copy(v.begin(), v.begin() + 1, v.end(), w.begin()); // Copies v into and rotate w

    return 0;
}
```

### Sorting Operations

#### Sort Operations

```c++
#include <algorithm>
#include <vector>

int main() {
    std::vector<int> v({1, 2, 3, 4});
    std::vector<int> w(v.size());

    std::sort(v.begin(), v.end());
    std::stable_sort(v.begin(), v.end());
    std::partial_sort(v.begin(), v.begin() + 2, v.end());
    std::partial_sort_copy(v.begin(), v.end(), w.begin(), w.end());

    bool b1  = std::is_sorted(v.begin(), v.end());
    auto it1 = std::is_sorted_until(v.begin(), v.end());

    return 0;
}
```

#### Binary Search Operations

```c++
#include <algorithm>
#include <vector>

int main() {
    std::vector<int> v({1, 2, 3, 4});

    auto it1 = std::lower_bound(v.begin(), v.end(), 1);     // Returns an iterator to the first not less than the value (>=)
    auto it2 = std::upper_bound(v.begin(), v.end(), 1);     // Returns an iterator to the first greater than the value (>)
    auto it3 = std::equal_range(v.begin(), v.end(), 1);     // Returns an iterator to the first range of values 1

    bool b1 = std::binary_search(v.begin(), v.end(), 1);    // Determines if an element is in the container
    bool b2 = std::binary_search(v.begin(), v.end(), 1, [](const int& a, const int& b) { // Determines if an element is in the container with custom comparator
        return a == b - 10;
    });

    return 0;
}
```

#### Min & Max Operations

```c++
#include <algorithm>
#include <vector>

int main() {
    std::vector<int> v({1, 2, 3, 4});

    int m1 = std::max(1, 2);
    int m2 = std::max(1, 2, [](const int& a, const int& b) -> bool {
        return a % b;
    });

    auto it1 = std::max_element(v.begin(), v.end());
    auto it2 = std::min_element(v.begin(), v.end());
    auto it3 = std::minmax_element(v.begin(), v.end());

    return 0;
}
```

#### Set Operations

```c++
#include <algorithm>
#include <set>
#include <vector>

int main() {
    std::set<int> s1({1, 2, 3, 4});
    std::set<int> s2({1, 2, 5, 6});
    std::vector<int> v;

    bool b = std::includes(s1.begin(), s1.end(), s2.begin(), s2.end());

    std::merge(s1.begin(), s1.end(), s2.begin(), s2.end(), std::back_inserter(v));
    v.clear();
    std::set_union(s1.begin(), s1.end(), s2.begin(), s2.end(), std::back_inserter(v));
    v.clear();
    std::set_intersection(s1.begin(), s1.end(), s2.begin(), s2.end(), std::back_inserter(v));
    v.clear();
    std::set_difference(s1.begin(), s1.end(), s2.begin(), s2.end(), std::back_inserter(v));

    return 0;
}
```

## Lambda

### Capture Close

```c++
#include <iostream>

int main() {
    int x   = 10;
    int y   = 20;
    auto f1 = []() -> void {};                                         // Doesn't capture external variables
    auto f2 = [x, y]() -> void { std::cout << x << y << std::endl; };  // Captures x and y by copy
    auto f3 = [&x, &y]() -> void { std::swap(x, y); };                 // Captures x and y by reference
    auto f4 = [=]() -> void { std::cout << x << y << std::endl; };     // Captures all external variables
    auto f5 = [&]() -> void { std::swap(x, y); };                      // Captures all external variables by reference
    auto f6 = [=, &y]() -> void { std::cout << x << y << std::endl; }; // Capture all external variables by copies except y by reference

    return 0;
}
```
