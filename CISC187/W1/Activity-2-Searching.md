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

ALGORITHM randomizedSearch(data, key)
    data: A vector of 100,000 distinct elements
    key: The value to be searched

    n = length(data)
    
    Step 1: Create a list of all possible indices
    indices = [0, 1, 2, ..., n-1]

    Step 2: Shuffle the indices randomly (Fisher-Yates Shuffle)
    FOR i FROM n-1 DOWN TO 1:
        j = random_integer(0, i)
        SWAP(indices[i], indices[j])

    Step 3: Iterate through the shuffled indices
    steps = 0
    FOR each index IN indices:
        steps = steps + 1
        IF data[index] == target:
            RETURN (index, steps) // Found
    
    RETURN (-1, steps) // Not found
END ALGORITHM

Since this program essentially uses linear search, it's time complexities equal that of linear search with worst-case being O(n) and best case being O(1).
## Then, implement the algorithm in C++, using only the following standard headers: <vector> for data storage, <random> for random index generation, and <iostream> for input and output. The implementation should track and report the number of comparisons performed during the search.

```C++

#include <iostream>
#include <vector>
#include <random>

using namespace std;

// Structure to return both the found index and the step count
struct SearchResult {
    int index;
    int steps;
};

SearchResult randomizedSearch(const vector<int>& data, int target) {
    int n = data.size();
    
    //Create a vector of indices [0, 1, 2, ..., n-1]
    vector<int> indices(n);
    for (int i = 0; i < n; ++i) {
        indices[i] = i;
    }

    // Setup the random number generator
    random_device rd;
    mt19937 g(rd());

    //Perform Fisher-Yates shuffle on the indices vector
    for (int i = n - 1; i > 0; --i) {
        // Generate a random index j such that 0 <= j <= i
        uniform_int_distribution<int> dist(0, i);
        int j = dist(g);
        
        // Swap elements at i and j
        int temp = indices[i];
        indices[i] = indices[j];
        indices[j] = temp;
    }

    // Search the data using the randomized index order
    int comparisons = 0;
    for (int i = 0; i < n; ++i) {
        comparisons++;
        int currentIndex = indices[i];
        
        if (data[currentIndex] == target) {
            return {currentIndex, comparisons};
        }
    }

    return {-1, comparisons};
}

int main() {
    const int SIZE = 100000;
    vector<int> data(SIZE);

    // Populate the dataset with distinct elements (0 to 99,999)
    for (int i = 0; i < SIZE; ++i) {
        data[i] = i;
    }

    int target;
    cout << "Enter a target value to search for (0 - 99,999): ";
    cin >> target;

    SearchResult result = randomizedSearch(data, target);

    cout << "\n--- Randomized Search Results ---" << endl;
    if (result.index != -1) {
        cout << "Target found at index: " << result.index << endl;
        cout << "Total comparisons made: " << result.steps << endl;
    } else {
        cout << "Target not found." << endl;
        cout << "Total comparisons made: " << result.steps << endl;
    }

    return 0;
}

```

## Finally, compare and contrast the randomized search algorithm with linear search and binary search in terms of time complexity, data requirements (such as ordering), and practical efficiency. Discuss scenarios in which each approach may be preferred, highlighting the advantages and limitations of randomized search relative to linear and binary search.

Since binary search requires the data to be sorted, it is most practical for large sets of data since the process of sorting the data in and of itself requires memory usage. Randomized search serves basically the same purpose as linear search, and for smaller sets of unsorted data these types of searches will prove most effective.


