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

