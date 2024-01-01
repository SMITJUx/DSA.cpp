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
    v.pop_back();                   // Remove the last element
    v.clear();                      // Clear the vector by setting the size to 0

    return 0;
}
```