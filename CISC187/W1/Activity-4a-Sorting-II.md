
# Sorting Algorithms

## Tasks

### 1. Proof that, under the average-case scenario, the insertion sort has a time complexity of O(N^2). Draw a clear figure and show all the operations clearly.
Pseudocode of Insertion sort taken out of the reading:

```
i ← 1
while i < length(A) // where A is the array
    j ← i
    while j > 0 and A[j-1] > A[j]
        swap A[j] and A[j-1]
        j ← j - 1
    end while
    i ← i + 1
end while
```
To symbolize the average case, you can assume that inserting a new, sorted jth element requires moving past roughly j/2 elements. Generalize this to the Nth insertion, you get N/2 runs for the Nth insertion. By summing all the operations and replacing j with N i.e 1/2 + 2/2 + 3/2 +... N/2 you can reduce the expression to (N^2)/4 which in Big O notation is reduced to the quadratic time complexity O(N^2).

### 2. Insertion sort normally begins with i = 1 (0-based indexing). Let N = 5 and assume the array is in descending order (worst case).

### Count operations where:

### a comparison is A[j] > key

10 total comparisons

### a shift is A[j+1] = A[j]

10 total shifts

### a) Start the algorithm at i = 1. Verify the total operations = 20.
### b) Start the algorithm at i = 2, then i = 3. Count operations again.
For i = 2, 2 comparisons and 2 shifts occur since A[1] and A[0] are never compared and assumed to be sorted. For i = 3, 3 comparisons and 3 shifts occur. 
### c) For (b), does the algorithm still sort the entire array? Explain.
The algorithm fails to sort the entire array in this scenario since the first two elements are never checked and are assumed to already be sorted. 
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
If you analyze all the possible scenarios: the string contains X in the very beginning, the string contains X somewhere in the middle, the string contains X somewhere in the end, or the string does not contain X, and then take the total steps for each scenario and average them (1 + N/2 + N + N)/4 you end up with a time complexity of O(N) since all constants and multipliers/ divisors are ignored.

### b) Then, modify the code to improve the algorithm’s efficiency for best- and average-case scenarios.
For the both the best-case and worst-case scenario, the code can be improved by simply returning "true" the instant the "X" is found rather than having a preset variable foundX initialized to false and then updated to true after iterating through the entire string.
```
function containsX(string) {
    for (let i = 0; i < string.length; i++) {
        if (string[i] === "X") {
            return true;
        }
    }
    return false;
}
```
