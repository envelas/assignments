## Implementing a Stack Using a Linked List in C++ (Code)

```C++
#include <iostream>

using namespace std;

struct Node {
    int data;
    Node* next;
};

class Stack {
private:
    Node* top;

public:
    Stack();

    void push(int value);
    void pop();
    int peek();
    bool isEmpty();
    void display();
};

Stack::Stack() {
    top = nullptr;
}

void Stack::push(int value) {
    Node* newNode = new Node();
    newNode->data = value;
    newNode->next = top;
    top = newNode;
}

void Stack::pop() {
    if (isEmpty()) {
        cout << "Stack Underflow" << endl;
        return;
    }
    Node* temp = top;
    top = top->next;
    delete temp;
}

int Stack::peek() {
    if (isEmpty()) {
        cout << "Stack is empty" << endl;
        return -1; 
    }
    return top->data;
}

bool Stack::isEmpty() {
    return top == nullptr;
}

void Stack::display() {
    if (isEmpty()) {
        cout << "Stack is empty" << endl;
        return;
    }
    Node* temp = top;
    cout << "Stack elements:" << endl;
    while (temp != nullptr) {
        cout << temp->data << endl;
        temp = temp->next;
    }
}

int main() {
    Stack s;

    s.push(10);
    s.push(20);
    s.push(30);
    s.push(40);

    s.display();
    cout << endl;

    s.pop();

    cout << "Top element: " << s.peek() << endl << endl;

    s.display();

    return 0;
}
```
## Reflection Questions
#### Why is a linked list efficient for stack implementation?
In a stack where a user seeks the "Last-in, First Out" model, linked lists work perfectly sice they allow quick insertion and deletion at the head. Linked-Lists also allow for easy expansion of the stack since each node has its own memory address allowing for a dynamic size.  
#### What is the time complexity of push and pop operations?
The push operation has a time complexity of O(1). A new node is added to the head of the stack and the pointer is updated to point to the new head, allowing addition of this element without iterating through the entire stack.  
The pop operation has a time complexity of O(1). The pointer is removed from the current top and instead points now to the new head, seamlessly "deleting" the old head without stack iteration. 
#### What happens if memory is not deallocated after pop?
Not deallocating this memory can lead to a memory leak. To the operating system, that memory address is still in use even though the pointer has been removed, leading to possible crashes. 
#### Compare a stack implemented with an array versus a linked list.
In arrays, the size is fixed while in a linked list, the size is dynamic, it can continue to grow as needed. Memory wise, arrays contain only the data while linked lists contain both the data and the pointers per node. Arrays are faster for reading and for inserting / deleting at the end. Linked lists are faster for insertion / deletion at the beginning. They both share similar search times and similar times for insertion or deletion in the middle. Linked lists prove more efficient for certain scenarios such as removing invalidly formatted emails from large lists. In an array, you have to iterate through the entire list for every email deleted, while a linked-list would only have to iterate through the list once, deleting each element as it goes.
