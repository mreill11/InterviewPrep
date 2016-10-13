Trees
=====

## Binary Trees
* Binary search trees consist of linked nodes. These nodes have exactly one parent, they link up to two children, and never have more than one sibling.
* The topmost node is referred to as the root node, and the bottom most nodes are called leaves
* The depth of a tree is the number of steps away leaves are from the root
* A full tree is when every leaf has the same depth and every non leaf has two children
* A complete tree is a full tree with the added parameter that every level except the deepest has the maximum number of nodes

## Tree Traversal (Depth First)
![binarytree](http://www.geeksforgeeks.org/wp-content/uploads/2009/06/tree12.gif)
### In-Order
1. Traverse the left most subtree
2. Visit the root
3. Traverse the right subtree

Result: 4-2-5-1-3

##### Implementation
```C++
void printInorder(struct node* node) {
	if (node == NULL)
		return;

	/* first recur on left child */
	printInorder(node->left);

	/* then print the data of node */
	printf("%d ", node->data);

	/* now recur on right child */
	printInorder(node->right);
}
```

![binarytree](http://www.geeksforgeeks.org/wp-content/uploads/2009/06/tree12.gif)
### Pre-Order
1. Visit the root
2. Traverse the left subtree
3. Traverse the right subtree

Result: 1-2-4-5-3

##### Implementation
```C++
void printPreorder(struct node* node) {
	if (node == NULL)
	   return;

	/* first print data of node */
	printf("%d ", node->data);

	/* then recur on left sutree */
	printPreorder(node->left);

	/* now recur on right subtree */
	printPreorder(node->right);

}
```

![binarytree](http://www.geeksforgeeks.org/wp-content/uploads/2009/06/tree12.gif)
### Post-Order
1. Traverse the left subtree
2. Traverse the right subtree
3. Visit the root

Result: 4-5-2-3-1

##### Implementation
```C++
void printPostorder(struct node* node) {
	if (node == NULL)
	 	return;

	// first recur on left subtree
	printPostorder(node->left);

	// then recur on right subtree
	printPostorder(node->right);

	// now deal with the node
	printf("%d ", node->data);
}
```


## Binary Search Tree
![binarysearchtree](http://proprogramming.org/wp-content/uploads/2015/07/binary-search-tree-c-.png)
* A Binary Search Tree is a binary tree that satisfies the following condition:
  * A parent node is greater than all values in it's left subtree, but less than all values in it's right subtree

##### Implementation
* Array Implementation:
  * Breadth First Order (root, children, grandchildren)
  * Traversal References:
    * Parent(i) = floor((i - 1) / 2)
    * LeftChild(i) = (2 * i) + 1
    * RightChild(i) = (2 * i) + 2
* Node Implementation:
```C++
struct Node {
	T data;
	Node *left;
	Node *right;
}
```

##### Complexity
* O(logn) on average for search, insert, and remove
* O(n) worst case

##### Traversals
1. Breadth-First
  * Travels through tree left to right horizontally
  * Implementation using a queue:
```C++
template <typename T>
void bfs(Node<T> *root) {
	queue<Node<T>*> q;
	q.push(root);
	while (!q.empty()) {
		auto n = q.front();
		q.pop();
		cout << n->data << " ";
		if (n->left)
			q.push(n->left);
		if (n->right)
			q.push(n->right);
	}
	cout << endl;
}
```
2. Depth-First
  * Starts at the root and travels as far downward as possible before backtracking
  * Implementation using a stack:
```C++
template <typename T>
void dsf(Node<T> *root) {
	stack<Node<T>*> s;
	s.push(root);
	while (!s.empty()) {
		auto n = s.top(); s.pop();
        cout << n->data << " ";
        if (n->right)
        	s.push(n->right);
        if (n->left)
        	s.push(n->left);
	}
	cout << endl;
}
```
3. Depth-First (recursive)
  * Implementation:
```C++
template <typename T>
void dfs_recursive(Node<T> *root) {
	if (root == nullptr) {
	 	return;
	}

	cout << root->data << " ";

	if (root->left)  dfs_recursive(root->left);
	if (root->right) dfs_recursive(root->right);
}
```

## B-Tree
![btree](http://flylib.com/books/2/300/1/html/2/images/17fig34.jpg)
* A B-Tree is a more generalized BST
* Nodes of a B-Tree can have more than two children, and can contain more than a single entry
* A B-Tree is often found in file systems and databases
* Every node is a sorted array, and a B-Tree is self balancing
  * Every node has at least MIN entries and MIN+1 children (except root)
  * Every node has at most 2 * MIN entries and 2 * MIN + 1 children

##### Complexity
* O(logn) for search, insert, and remove average case
* O(logn) worst case for the above operations


## Red-Black Tree
![redblacktree](http://d1gjlxt8vb0knt.cloudfront.net//wp-content/uploads/RedBlackTree.png)
* Red-Black Trees are essentially B-Tree's that fit into BSTs
* A black node signifies a B-Node
  * Red nodes are children of B-Nodes
* The root must be black, and no path has two red nodes in a row
* Every path has the same number of black nodes, every path has the same number of B-Nodes
* Rules of Insertion:
  * If the tree is empty, the new node is black. Otherwise, it is red
  * Unbalanced 4 node:
    * Rotate left to make a new local root with the old root as the left child and the right child still the right child
    * Switch colors of the new local root and the new left child. If the new root had children before it was rotated, make them child of the right child
  * Overfull 5 node:
    * Flip colors of all local black nodes and their children



