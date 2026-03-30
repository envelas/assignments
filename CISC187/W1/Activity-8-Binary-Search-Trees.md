# Binary Search Trees
## Tasks

#### 1. Imagine you were to take an empty binary search tree and insert the following sequence of numbers in this order: [1, 5, 9, 2, 4, 10, 6, 3, 8]. Draw a diagram showing what the binary search tree would look like. Remember, the numbers are being inserted in the order presented here. 
https://viewer.diagrams.net/?tags=%7B%7D&lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1&title=binarysearchtreeedv.drawio.png&dark=auto#R%3Cmxfile%3E%3Cdiagram%20name%3D%22Page-1%22%20id%3D%22ewHoNPfVpjgycsB6Fb7K%22%3E7Zldb5swFIZ%2FTS4rATYJXK5p105TtUrRNGl3FrjgisTIOF%2F79TO1%2BbBpk4bMVpXuJsIv5gDPe44%2FyATMl7s7hsr8gaa4mAReupuAm0kQxEEofmthL4UQTqWQMZJKye%2BEBfmDlegpdU1SXGkdOaUFJ6UuJnS1wgnXNMQY3erdnmih37VEGR4IiwQVQ%2FUXSXku1Sj0Ov0ekyxv7ux76swSNZ2VUOUopdueBG4nYM4o5fJouZvjombXcJHXfX3jbPtgDK%2F4ey6oOLonz9GP79%2Be%2BcPvq58RfsyuXomipIrvGwYijsAtGtfbnHC8KFFSn9kKw4WW82UhWr44RFUpPXgiOyxuey1DbVCx1nFuMON415PUI99husSc7UWXvEc1Ugi3PQeUpIK0lFWaAdVEyv6sDdwREgcK0gnAAsfAQkvAgKcD860RA46JRZaIQYMYDGwRg46JAUvE%2FJkrYqFjYlNbVQmNYcxaVU4dEwsc5VgAbRGbOSYW28qx2BWxyDGxZs34z5GFnquyjB0jg5aIBaErYr6avXA6WMgfZLhKv9TbA9FKClRVJNHRMbpepTWzG%2B81bscZNQAYLhAnG%2F3ZeuDCA2DUHR4pES%2FSsTUKuN1yNCEqumYJVlf1dwRGIOAbgcyRgCOWYT4I9OJT%2B9pnWAdPsO7lnY4vzC%2FEYmNWa2e5Uy0OpkcGe9sWhx%2FOYvnGxyf6D5IKIDIcHJsKEBiBzNW47VSYXvhALR4T7XsdyppkdaDIzcW%2B%2FgFHHMiIb1xt2NkO5ucOEcD1EDH7nxd6oUbn5AU07Ry7Ohgsel3nRXTheTG0zvyIObakzU9Vzq2LP5t15oINjq06c1KA5sbJsnVNCn4e6wbFEo%2BtOqN8YfPx%2FmzrRLP7n0h27%2F5sA7d%2FAQ%3D%3D%3C%2Fdiagram%3E%3C%2Fmxfile%3E
#### 2. If a well-balanced binary search tree contains 1,000 values, what is the maximum number of steps it would take to search for a value within it?
The maximum number af steps would be 10 which is the highest level of the tree. This value also equals log(1000) which corresponds to the time complexity of the worst-case scenario (O(logN)).
#### 3. Write an algorithm that finds the greatest value within a binary search tree.
```C++
#include <iostream>

struct Node {
    int value;
    Node* left;
    Node* right;
};

int findMax(Node* root) {
    // If tree is empty
    if (root == nullptr) {
        return -1; 
    }
    
    Node* current = root;
    // Keep traversing the right nodes
    while (current->right != nullptr) {
        current = current->right;
    }
    
    return current->value;
}

```
In this case, the value we are looking for is the value located at the deepest right hand node. Only traversal of the right hand nodes is required.

#### 4. Write a code in C++ using the same array mentioned in #1 and implement a binary search tree. Only insertion operation is required. 
```C++
#include <iostream>
#include <vector>

struct Node {
    int data;
    Node* left;
    Node* right;

    Node(int val) : data(val), left(nullptr), right(nullptr) {}
};

// Insertion operation function
Node* insert(Node* root, int val) {
    if (root == nullptr) {
        return new Node(val);
    }

    if (val < root->data) {
        root->left = insert(root->left, val);
    } else {
        root->right = insert(root->right, val);
    }

    return root;
}

int main() {
    std::vector<int> values = {1, 5, 9, 2, 4, 10, 6, 3, 8};
    Node* root = nullptr;

    for (int val : values) {
        root = insert(root, val);
    }
    
    return 0;
}
```
