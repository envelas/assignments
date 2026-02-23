# Sorting Algorithms

## Tasks

### 1. Use Big O Notation to describe the time complexity of an algorithm that takes 4N + 16 steps.
Since Big O Notation ignores constants and constant multiples or coefficients, the time complexity of this algorithm is simply O(N) which is a linear time complexity. As N gets increasingly larger, the constant 16 becomes irrelevant. If the effect of the multiplier of 4 is observed on a graph as compared to just N, both growths are linear and once again with a large N the multiplier becomes irrelevant as the time complexity can still be described simply as the linear growth O(N).

### 2. Use Big O Notation to describe the time complexity of an algorithm that takes 2N^2. 
As stated in the previous question, the effect of the constant multiplier or coefficient is irrelevant for large values of N. Big O notation cares only about the higher order nature of the algorithm, or the highest power exponent, which in this case is 2. The notation would be written as O(N^2) which describes quadratic growth.

### 3. Use Big O Notation to describe the time complexity of the following function, which returns the sum of all numbers of an array after the numbers have been doubled:

```
def double_then_sum(array) 
	doubled_array = []

	array.each do |number| 
		doubled_array << number *= 2
	end

	sum = 0

	doubled_array.each do |number| 
		sum += number
	end
	return sum 
end
```
This function would first iterate through the entire array doubling each value, a process taking N steps with N being the total size of the array. Summing each value would require iterating through the entire array again for an additional N number of steps for a grand total of N + N or 2N steps. In Big O notation this would simply be the linear time complexity O(N).

### 4. Use Big O Notation to describe the time complexity of the following function, which accepts an array of strings and prints each string in multiple cases:

```
def multiple_cases(array) 
	array.each do |string|
		puts string.upcase 
		puts string.downcase 
		puts string.capitalize
	end 
end
```
This function is performing 3 actions on each index of an array, for a total of 3N steps. In Big O notation this would be the linear time complexity O(N) as the multiplier 3 becomes irrelevant for larger values of N.

### 5. The next function iterates over an array of numbers, and for each number whose index is even, it prints the sum of that number plus every number in the array. What is this function’s efficiency in terms of Big O Notation?

```
def every_other(array) 
	array.each_with_index do |number, index|
		if index.even?
			array.each do |other_number|
            	puts number + other_number
			end 
		end
	end 
end
```
On average, the number of even indexes in an array are approximately N/2. Every time an even index is found, the whole array gets iterated through once again. The total amount of steps this would take is N * N/2 or (N^2)/2 steps. In Big O notation, this would be the quadratic time complexity O(N^2) since the divisor 2 becomes irrelevant for larger values of 2.

https://sdccd.us-west-2.instructuremedia.com/embed/0651f7e4-4939-4791-b8ac-70ee86fedc43
