# Tasks
## How many steps would it take to perform a linear search for the number 8 in the ordered array, [2, 4, 6, 8, 10, 12, 13]?
A linear search on this array would take 4 steps, the algorithm would begin in the beginning of the array and would analyze each subsequent index of the array until the expected value is found.

## How many steps would binary search take for the previous example?
A binary search on this array would take just one step since it would start in the middle of the array and the value that is being searched for is located perfectly in the middle of the array.

## What is the maximum number of steps it would take to perform a binary search on an array of size 100,000?
The maximum number of steps would require a worst-case scenario in which the value that is being searched for is either in the beginning or end of the array. Since binary search begins in the middle of the array and proceeds to omit half of the array with each step, this would take log(100,000) (log base 2) steps which is approximately 17 steps.

## Write a C++ program that implements both linear search and binary search algorithms using an array of 100,000 elements. The program should record and report the number of steps (comparisons) performed during each search operation. In addition, analyze and justify the observed behavior by providing a theoretical explanation using Big-O notation, demonstrating why linear search exhibits O(N) complexity and binary search exhibits O(logN) complexity.
```C++
#include <iostream>
#include <vector>
#include <algorithm>

//Function for linear search
int linearSearch(const vector<int>& v, int key) {
  int comparisons = 0;
  for (int i = 0; i < v.size(); i++) {
    comparisons++;
    if (v[i] == key)
      return comparisons;
  }
  return comparisons; //value not found, will return 0
}

//Function for binary search
int binarySearch(const vector<int>& v, int key) {
    int comparisons = 0;
    int low = 0;
    int high = v.size() - 1;

    while (low <= high) {
      comparisons++;
      int mid = low + (high - low) / 2;

      if (v[mid] == key) {
        return comparisons;
      }

      if (v[mid] < key) {
        low = mid + 1;
      } else {
        high = mid - 1;
        }
    }
  return comparisons;
}


int main() {
  vector<int> data(100000);

  int key;
  cout << "Enter a number to search for: ";
    cin >> key;

  int linearSteps = linearSearch(data, key);
  int binarySteps = binarySearch(data, key);

  cout << "Linear Search Steps: " << linearSteps << endl;
  cout << "Binary Search Steps: " << binarySteps << endl;

  return 0;
}
```

## Write pseudocode for a randomized search algorithm that searches for a given key by randomly selecting indices without repetition. Use a dataset of 100,000 distinct elements, stored in a vector. Each element may be examined at most once during the search. Analyze and state the best-case, average-case, and worst-case time complexities of this algorithm using Big-O notation.

## Then, implement the algorithm in C++, using only the following standard headers: <vector> for data storage, <random> for random index generation, and <iostream> for input and output. The implementation should track and report the number of comparisons performed during the search.

## Finally, compare and contrast the randomized search algorithm with linear search and binary search in terms of time complexity, data requirements (such as ordering), and practical efficiency. Discuss scenarios in which each approach may be preferred, highlighting the advantages and limitations of randomized search relative to linear and binary search.
