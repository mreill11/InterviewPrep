Data Structures
===============

## Dynamic Array
* A variable size array that allows elements to be added or removed at random locations
* Allocated at runtime, might need to be expanded however

##### Complexity
* Search: O(n)
* Indexing: O(1)
* Insert: O(1) at end, O(n) otherwise
* Delete: O(1) at end, O(n) otherwise

## Linked List
* Items in a linked list can be easily added or removed, and the size of a linked list does not have to be predefined
![linkedlist](https://upload.wikimedia.org/wikipedia/commons/6/6d/Singly-linked-list.svg)

##### Implementation
```C++
// linked_list_raii.cpp: Singly Linked List (RAII)

#include <cstdlib>
#include <iostream>
#include <stdexcept>

const int NITEMS = 10;

// List declaration ------------------------------------------------------------

template <typename T>
class List {
    protected:
        struct Node {
            T     data;
            Node *next;
        };

        typedef Node * iterator;

        Node  *head;
        size_t length;

    public:
        List() : head(nullptr), length(0) {}
        iterator front() { return head; };

        ~List();                                    // Destructor
        List(const List<T> &other);		    // Copy Constructor
        List<T>& operator=(List<T> other);	    // Assignment Operator
        void swap(List<T> &other);		    // Utility

        size_t size() const { return length; }
        T& at(const size_t i);
        void insert(iterator it, const T &data);
        void push_back(const T &data);
        void erase(iterator it);
};

// List implementation --------------------------------------------------------

// Post-condition: Clears all nodes from list
template <typename T>
List<T>::~List() {
    Node *next = nullptr;

    // Need next otherwise invalid reads (use valgrind)
    for (Node *curr = head; curr != nullptr; curr = next) {
        next = curr->next;
        delete curr;
    }
}

// Post-condition: Copies all nodes from other
template <typename T>
List<T>::List(const List<T> &other)
    : head(nullptr), length(0) {
    for (Node *curr = other.head; curr != nullptr; curr = curr->next) {
        push_back(curr->data);
    }
}

// Post-condition: Clears existing list and copies all nodes from other
template <typename T>
List<T>& List<T>::operator=(List<T> other) {
    swap(other);
    return *this;
}

template <typename T>
void List<T>::swap(List<T> &other) {
    std::swap(head, other.head);
    std::swap(length, other.length);
}

template <typename T>
T& List<T>::at(const size_t i) {
    Node *node = head;
    size_t   n = 0;

    while (n < i && node != nullptr) {
        node = node->next;
        n++;
    }

    if (node) {
        return node->data;
    } else {
        throw std::out_of_range("invalid list index");
    }
}

template <typename T>
void List<T>::insert(iterator it, const T& data) {
    if (head == nullptr && it == nullptr) {
        head = new Node{data, nullptr};
    } else {
    	Node *node = new Node{data, it->next};
    	it->next   = node;
    }
    length++;
}

template <typename T>
void List<T>::push_back(const T& data) {
    if (head == nullptr) {
        head = new Node{data, nullptr};
    } else {
        Node *curr = head;
        Node *tail = head;

        while (curr) {
            tail = curr;
            curr = curr->next;
        }

        tail->next = new Node{data, nullptr};
    }
    length++;
}

template <typename T>
void List<T>::erase(iterator it) {
    if (it == nullptr) {
	throw std::out_of_range("invalid iterator");
    }

    if (head == it) {
	head = head->next;
	delete it;
    } else {
	Node *node = head;

	while (node != nullptr && node->next != it) {
	    node = node->next;
	}

	if (node == nullptr) {
	    throw std::out_of_range("invalid iterator");
	}

	node->next = it->next;
	delete it;
    }

    length--;
}
```

##### Complexity
* Search: O(n)
* Insert:
  * Best Case: O(1)
  * Worst Case: O(n)
* Delete:
  * Best Case: O(1)
  * Worst Case: O(n)

## Stacks
* Stacks are a LIFO abstract data type
* They are usually implemented with a singly linked list, but they can also be implemented with an array
* Stacks have 4 main functions:
  * push() - adds an element to the top
  * pop() - deletes the element at the top
  * top() - returns the top element
  * empty() - returns whether or not the stack is empty
* Stacks do not support access, searching for, or insertion anywhere except the top of the stack
* Size is also limited

##### Implementation
* Linked List implementation: top of the stack is the front of the list
```C++
template <typename T>
class vector_stack {
std::vector<T> data;

public:
	bool empty()   const { return data.empty(); }
	const T& top() const { return data.back(); }
 	void push(const T& value) {
     	data.push_back(value);
 	}
 	void pop() {
     	data.pop_back();
 	} 
};
```

##### Complexity
* push(): O(1)
* pop(): O(1)

## Queues
* Queues are a FIFO abstract data type
* Can be implemented with multiple simple data structures
* Queues have 5 basic functions:
  * push() - add an element to the back of the queue
  * pop() - remove an element from the front of the queue
  * front() - return the item at the front
  * back() - return the item at the back
  * empty() - return whether or not the queue is empty
* Queues only support insertion at the back, and deletion at the front

##### Implementation
* Implementing a Queue with two Stacks
```C++
template <typename T>
class stack_queue {
std::stack<T> in, out;
	void in_to_out() {
     	while (!in.empty()) {
         	out.push(in.top());
         	in.pop();
	 	}
	} 
public:
    bool empty() const { return in.empty() && out.empty(); }
    const T& front() {
        if (out.empty()) in_to_out();
       		return out.top();
     }
    const T& back() const { return in.top(); }
    void push(const T& value) {
        in.push(value);
    }
    void pop() {
      	if (out.empty()) in_to_out();
		out.pop();
	} 
};
```

##### Complexity
* All cases are O(1)

## Priority Queues
* Priority Queues are basically queues that are returned in sorted order
* Each actual value has a priority value associated with it, but these values are often not repeated
* Priority Queues have 4 basic functions:
  * push() - insert value
  * pop() - erase largest value
  * top() - return largest value
  * empty() - return whether or not the priority queue is empty

##### Complexity
* When elements are sorted upon addition:
  * push(): O(n)
  * pop(): O(1)
  * top(): O(1)
* When elements are added to the back:
  * push(): O(1)
  * pop(): O(n)
  * top(): O(n)

## Binary Heaps