# Adaptive Sorting Strategy

## Part A: Adaptive Sorting Selection

1. Create an array of 50 integers.

2. Implement both sorting algorithms:
    -Selection Sort
    -Insertion Sort

3. Your program must analyze the initial ordering of the array and determine which scenario it represents (best, average, or worst) based on a clearly defined threshold that you assume.

4. Based on your analysis, your program should automatically choose the more appropriate sorting algorithm.

```C++
#include <iostream>
#include <algorithm>
#include <ctime>     
#include <cstdlib>   

using namespace std;

const int SIZE = 50;
const int ORDERING_THRESHOLD = 122; // Threshold for "nearly sorted" (approx 10% of total possible diversions)

// Function to implement Insertion Sort
void insertionSort(int arr[], int n) {
    for (int i = 1; i < n; ++i) {
        int key = arr[i];
        int j = i - 1;
        
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
}

// Function to implement Selection Sort
void selectionSort(int arr[], int n) {
    for (int i = 0; i < n - 1; ++i) {
        int min_idx = i;
        for (int j = i + 1; j < n; ++j) {
            if (arr[j] < arr[min_idx]) {
                min_idx = j;
            }
        }
        swap(arr[min_idx], arr[i]);
    }
}

// Function to analyze the array ordering and determine the scenario
int arrayOrdering(int arr[], int n) {
    int diversions = 0;
    for (int i = 0; i < n - 1; ++i) {
        for (int j = i + 1; j < n; ++j) {
            if (arr[i] > arr[j]) {
                diversions++;
            }
        }
    }
    return diversions;
}

int main() {
    // Create an array of 50 integers
    int data[SIZE];

    // Seed the random number generator
    srand(time(0));

    // Fill the array with random numbers (0-99)
    for (int i = 0; i < SIZE; ++i) {
        data[i] = rand() % 100;
    }

    int diversions = arrayOrdering(data, SIZE);

    // Choose the sorting algorithm based on the threshold
    if (diversions <= ORDERING_THRESHOLD) {
        insertionSort(data, SIZE);
    } else {
        selectionSort(data, SIZE);
    }

    return 0;
}
```
## Part B: Case Classification Without Sorting
## Part C: Documentation
Provide a written explanation that includes:

-The threshold definition you used to differentiate between best, average, and worst cases.
-The reasoning behind your assumption.
-Why your program selects one sorting algorithm over the other in specific scenarios.
-A brief discussion of how input order affects the time complexity of Selection Sort and Insertion Sort.

Your explanation should demonstrate a clear understanding of algorithmic behavior and time complexity analysis.


