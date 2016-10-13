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


## Queues


## Priority Queues


## Binary Heaps