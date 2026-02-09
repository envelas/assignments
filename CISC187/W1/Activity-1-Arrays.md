# Tasks
## 1) Explain how to create an array of 100 elements. You can choose any data type of your choice. (requires C++ code)
In C++, you can create an array of 100 elements by declaring the arrays data type (integer, string etc.), naming your array, and then specifying the number of elements in closed brackets. For example, the following code snippet would create an array of 100 integers:
```C++
int numArray[100];
```
## 2) What will be the size of each element of an array. (requires C++ code)
To find the size of each element of an array, you can use the size command and specifiy "element_size." You would then need to pick any array index and it would return the size of that specific element. For example, the following code returns the size of the element at index 0 of the array created above, which also gives us the size of each element in this array.
```C++
size_t element_size = sizeof(numArray[0]);
```
## 3) For an array containing 100 elements, provide the number of steps the following operations would take: (theoretical)
Reading: Reading the array would take 1 step. 
#
Searching for a value not contained within the array: This would take 100 steps. The computer must first sift through every element of the array (in this case 100) before it can conclude that the value is not contained in the array.
#
Insertion at the beginning of the array: This would take 100 steps since insertion at the beginning would push each existing element back 1 index from where it was poreviously.
#
Insertion at the end of the array: This would take 1 step since the new element would simply be appended to the end of the array and none of the previous elements would be affected.
#
Deletion at the beginning of the array: This would take 100 steps since deleting the element at the beginning of the array would cause the index of all the preceding elements to be pushed back 1 index previous from where it was.
# 
Deletion at the end of the array: This would take 1 step since it would not affect any of the other elements in the array.
## 4) Normally the search operation in an array looks for the first instance of a given value. But sometimes we may want to look for every instance of a given value. For example, say we want to count how many times the value “apple” is found inside an array. How many steps would it take to find all the “apples”? Give your answer in terms of N. (theoretical)
Due to the nature of searching for values in an array, this operation would require "N" steps with "N" being the total number of elements in the array. When the program searches for the total number of instances of a specific value in an array such as the string "apples," it needs to sift through every element of that array and compare it to the value you are searching for.
## 5) Research how to find the memory address of an array. You can use any programming language of your choice. (requires code)
In c++, I found 2 ways to find the memory address of an array. One way is by typing in the array's name directly such as in the following code where we once again use the same array created above:
```c++
std::cout << "The array numArray lies at memory address: " << numArray << std::endl;
```
The other method uses the address-of (&) operator on the first element of the array. For example:
```c++
std::cout << "The array numArray lies at memory address: " << &numArray[0] << std::endl;
```
