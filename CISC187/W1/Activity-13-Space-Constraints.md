# Space Constraints
## Objective
How to write a space-efficient code
## Tasks
### 1. Following is the 'Word Builder' algorithm. Describe its space complexity in terms of Big O.
```
function wordBuilder(array) { 
		let collection = [];
		for(let i = 0; i < array.length; i++) { 
				for(let j = 0; j < array.length; j++) {
						if (i !== j) {
								collection.push(array[i] + array[j]);
						}
				}
		}
		return collection; 
}
```
The algorithm's space complexity is O(N^2). It takes pairs of strings from the input array and creates the "collection" array to store these pairs. Mathematically, the total number of pairs or elements that are created is N(N-1) which in big-o notation reduces to O(N^2).
### 2. Following is a function that reverses an array. Describe its space complexity in terms of Big O:
```
function reverse(array) { 
		let newArray = [];
		for (let i = array.length - 1; i >= 0; i--) { 
				newArray.push(array[i]);
		}
		return newArray;
}
```
This function's space complexity is O(N). This is due to the fact that in order to reverse the input array, it creates a new array that takes the input array's elements in reverse order, for a total number of elements of N.
### 3. Create a new function to reverse an array that takes up just O(1)extra space.
```
function reverse(array) {
    for (let i = 0; i < Math.floor(array.length / 2); i++) {
        let temp = array[i];
        array[i] = array[array.length - 1 - i];
        array[array.length - 1 - i] = temp;
    }
    return array;
}
```
Since this function does not create a new array, rather it uses the temporary variable "temp" to store temporary values, it has a space complexity of O(N).
### 4. Following are three different implementations of a function that accepts an array of numbers and returns an array containing those numbers multiplied by 2. For example, if the input is [5, 4, 3, 2, 1], the output will be [10, 8, 6, 4, 2].
```
function doubleArray1(array) { 
	let newArray = [];

	for(let i = 0; i < array.length; i++) { 
		newArray.push(array[i] * 2);
	}
	return newArray; 
}


function doubleArray2(array) {
	for(let i = 0; i < array.length; i++) {
  	array[i] *= 2;
  }
	return array; 
}


function doubleArray3(array, index=0) { 
	if (index >= array.length) { return; }
  array[index] *= 2;
  doubleArray3(array, index + 1);
	return array; 
}
```
### Fill in the table that follows to describe the efficiency of these three versions in terms of both time and space: 
Version #1	- Time complexity: O(N) Space complexity: O(N)  
Version #2 -  Time complexity: O(N) Space complexity: O(1)  
Version #3	- Time complexity: O(N) Space complexity: O(N)  
Since version 3 is a recursive function, it takes up a unit of memory for each recursive call it makes (the call stack). 
