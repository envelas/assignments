# Recursions
## Objective
Implement recursions in C++
### Tasks
#### 1. The following function prints every other number from a low number to a high number. For example, if low is 0 and high is 10, it would print:  
```  
0  
2  
4  
6  
8  
10  
```
#### Identify the base case in the function:
```
  def print_every_other(low, high)   
    return if low > high  
    puts low  
    print_every_other(low + 2, high)  
end  
```

The base case for this function would be 10, or in other words, the "high" number. Specifically, when the "low" variable, which is the variable that is storing the new values as the recursion occurs, stores a value that is greater than the value stored in "high," the function ends.
#### 2. My kid was playing with my computer and changed my factorial function so that it computes factorial based on (n - 2) instead of (n - 1). Predict what will happen when we run factorial(10) using this function:  
```
def factorial(n)  
    return 1 if n == 1  
    return n * factorial(n - 2)  
end  
```
The function will perform an infinite recursion as it will skip right past the integer "1" and proceed indefinitely for all negative integers. Although taking the factorial of a negative integer is undefined mathematically, since this function provides its own definition for a factorial, the process will indeed continue for all negative integers and will alternate between returning a positive and negative number.
#### 3. Following is a function in which we pass in two numbers called low and high. The function returns the sum of all the numbers from low to high. For example, if low is 1, and high is 10, the function will return the sum of all numbers from 1 to 10, which is 55. However, our code is missing the base case, and will run indefinitely! Fix the code by adding the correct base case:  
```
  def sum(low, high)  
    return high + sum(low, high - 1)  
end  
```

A correct base case for the function could be:
```
return if high < low
```
Using this base case, when the value stored in "high" is less than the "low" value, the process will end. For example, If low is 1 and high is 10, the recursion would continue until high - 1 = 0. At this point, high is less than low, and the function will end.
#### 4. Here is an array containing both numbers as well as other arrays, which in turn contain numbers and arrays:  
```
  array=[ 1,   
        2,   
        3,  
        [4, 5, 6],  
        7,  
        [8,  
          [9, 10, 11,  
            [12, 13, 14]  
          ]   
        ],  
        [15, 16, 17, 18, 19,  
          [20, 21, 22,  
            [23, 24, 25,  
              [26, 27, 29]  
            ], 30, 31   
          ], 32  
        ], 33   
      ]  
```
#### Write a recursive function that prints all the numbers (and just numbers).
