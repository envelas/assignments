# Stacks and Queues
## Tasks
#### 1. Using Figure 17 as a model, in the book Data Structures in C++, illustrate the result of each operation in the sequence PUSH(S,4), PUSH(S,1), PUSH(S,3), POP(S), PUSH(S,8), and POP(S) on an initially empty stack S stored in array S[1..6]. Code is not required.
First, the PUSH(S,4) operation inserts a 4 into the empty array S:  
[4]  
Second, PUSH(S,1) inserts a 1 to the end of the stack:  
[4,1]  
Then, PUSH(S,3) adds a 3 to the end of the stack:  
[4,1,3]  
POP(S) deletes the last element of the stack:  
[4,1]  
PUSH(S,8) adds an 8 to the end of the stack:  
[4,1,8]  
Finally, POP(S) deletes the element at the end of the stack:  
[4,1]  


#### 2. Using Figure 18 as a model, in the book Data Structures in C++, illustrate the result of each operation in the sequence ENQUEUE(Q,4), ENQUEUE(Q,1), ENQUEUE(Q,3), DEQUEUE(Q), ENQUEUE(Q,8), and DEQUEUE(Q) on an initially empty queue Q stored in array Q[1..6]. Code is not required.

First, ENQUEUE(Q,4) adds a 4 to the empty array Q:  
[4]  
Second, ENQUEUE(Q,1) adds a 1 to the "tail" of the queue:  
[4,1]  
Then, ENQUEUE(Q,3) adds a 3 to the "tail" of the queue:  
[4,1,3]  
DEQUEUE(Q) removes the element at the head of the queue:  
[1,3]  
ENQUEUE(Q,8) adds an 8 to the "tail" of the queue:  
[1,3,8]  
Finally, DEQUEUE(Q) removes the element at the head of the queue:  
[3,8]

#### 3. Rewrite ENQUEUE and DEQUEUE to detect underflow and overflow of a queue. (see Listings 4 & 5 in the book). Code is not required.
For ENQUEUE(Q,x):  
```
if Q.head == Q.tail + 1 or (Q.head == 1 and Q.tail == Q.length)
    error "overflow"
Q[Q.tail] = x
if Q.tail == Q.length
    Q.tail = 1
else Q.tail = Q.tail + 1
```

For DEQUEUE(Q,x):  
```
if Q.head == Q.tail
    error "underflow"
x = Q[Q.head]
if Q.head == Q.length
    Q.head = 1
else Q.head = Q.head + 1
return x
```


#### 4. A stack allows insertion and deletion of elements at only end, and a queue allows insertion at one end and deletion at the other end, a deque (double-ended queue) allows insertion and deletion at both ends. Write four O(1)-time procedures to insert elements into and delete elements from both ends of a deque implemented by an array. Code is not required.
To insert at the head of the queue:  
```
if (Q.head == 1 and Q.tail == Q.length) or (Q.head == Q.tail + 1)
    error "overflow"
if Q.head == 1
    Q.head = Q.length
else Q.head = Q.head - 1
Q[Q.head] = x

```
To insert at the tail of the queue:  
```
if Q.head == Q.tail + 1 or (Q.head == 1 and Q.tail == Q.length)
    error "overflow"
Q[Q.tail] = x
if Q.tail == Q.length
    Q.tail = 1
else Q.tail = Q.tail + 1
```
To delete from the head of the queue:  
```
if Q.head == Q.tail
    error "underflow"
x = Q[Q.head]
if Q.head == Q.length
    Q.head = 1
else Q.head = Q.head + 1
return x
```
To delete from the tail of the queue:  
```
if Q.head == Q.tail
    error "underflow"
if Q.tail == 1
    Q.tail = Q.length
else Q.tail = Q.tail - 1
return Q[Q.tail]
```
