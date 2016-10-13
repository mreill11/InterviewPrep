Sorts
=====

### Selection Sort
* The list is divided into two parts: a sorted sublist and the remaining unsorted list
* The algorithm finds the smallest element and swaps it with the leftmost element in the unsorted list
* This grows the sorted sublist by one element
* Selection Sort is not stable

> 64    25    12    22    11

> 11    25    12    22    64

> 11    12    25    22    64

> 11    12    22    25    64

> 11    12    22    25    64

##### Implementation
```C++
int i, j;

for (j = 0; j < n - 1; j++) {
	int iMin = j;

	for (i = j + 1; i < n; i++) {
		if (a[i] < a[iMin])
			iMin = i;
	}
	if (iMin != j)
		swap(a[j], a[iMin]);
}
```

##### Complexity
* Worst Case: O(n^2)
* Best Case: O(n^2)
* Average Case: O(n^2)
* Worst Case Space: O(n^2)