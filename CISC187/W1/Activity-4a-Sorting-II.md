
# Sorting Algorithms

## Tasks

### 1. Proof that, under the average-case scenario, the insertion sort has a time complexity of O(N^2). Draw a clear figure and show all the operations clearly.

### 2. Insertion sort normally begins with i = 1 (0-based indexing). Let N = 5 and assume the array is in descending order (worst case).

### Count operations where:

### a comparison is A[j] > key

### a shift is A[j+1] = A[j]

### a) Start the algorithm at i = 1. Verify the total operations = 20.
### b) Start the algorithm at i = 2, then i = 3. Count operations again.
### c) For (b), does the algorithm still sort the entire array? Explain.

### 3. The following function returns whether or not a capital “X” is present within a string. 4 pt
```
function containsX(string) {
	foundX = false;
	for(let i = 0; i < string.length; i++) { 
		if (string[i] === "X") {
			foundX = true; 
		}
	}
	return foundX; 
}
```
### (a) What is this function’s time complexity regarding Big O Notation?

### b) Then, modify the code to improve the algorithm’s efficiency for best- and average-case scenarios.
