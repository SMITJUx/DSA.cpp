# C++ STL Toolbox

## Containers

### Sequence

#### Vector

```c++
#include <vector>

int main() {
    std::vector<int> v({1, 2, 3, 4});

    std::size_t size   = v.size();    // Number of elements
    int         last   = v.back();    // Last element
    int         first  = v.front();   // First element
    int         second = v.at(1);     // Second element
    int*        data   = v.data();    // Access the underlying continuous storage
    bool        empty  = v.empty();   // Check if the sequence is empty or not

    v.push_back(5);                 // Add the element 5 at the end
    v.insert(v.begin() + 1, 10);    // Add the element 10 at the index 1
    v.erase(v.begin() + 1);         // Remove the element at the index 1
    v.emplace(v.begin() + 1);       // Construct an element at the index 1
    v.erase(v.begin() + 1);         // Remove the element at the index 1
    v.emplace_back();               // Construct an element at the end
    v.pop_back();                   // Remove the last element
    v.clear();                      // Clear the vector by setting the size to 0

    return 0;
}
```

#### List

```c++
#include <list>

int main() {
    std::list<int> li({1, 2, 3, 4});

    std::size_t size  = li.size();    // Number of elements
    int         last  = li.back();    // Last element
    int         first = li.front();   // First element
    bool        empty = li.empty();   // Check if the sequence is empty or not

    li.push_front(0);                      // Add the element 0 at the beginning
    li.push_back(5);                       // Add the element 5 at the end
    li.insert(std::next(li.begin()), 10);  // Add the element 10 as the second element
    li.erase(std::next(li.begin()));       // Remove the second element
    li.emplace(std::next(li.begin()));     // Construct an element and add it as the second element
    li.erase(std::next(li.begin()));       // Remove the second element1
    li.emplace_back();                     // Construct an element and add it at end
    li.emplace_front();                    // Construct an element and add it at the beginning
    li.pop_back();                         // Remove the last element
    li.pop_front();                        // Remove the first element
    li.clear();                            // Remove all elements

    return 0;
}
```