Sorts
=====

## Selection Sort
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
*Worst Case: O(n<sup>2</sup>)

*Best Case: O(n<sup>2</sup>)

*Average Case: O(n<sup>2</sup>)

*Worst Case Space: O(n)


## Insertion Sort
* On every iteration, one element is selected and placed where it should be in the sorted sublist at the left of the list
* Insertion Sort is stable

> 12    11    13     5     6

> 11    12    13     5     6

> 11    12    13     5     6

>  5    11    12    13     6

>  5     6    11    12    13

##### Implementation
```C++
int i; key; j;
int n = arr.size();

for (i = 1; i < n; i++)  {
	key = arr[i];
	j = i - 1;

	while (j >= 0 && arr[j] > key) {
		arr[j+1] = arr[j];
		j -= 1;
	}

	arr[j+1] = key;
}
```

##### Complexity
*Worst Case:
  * O(n<sup>2</sup>) comparisons
  * O(n<sup>2</sup>) swaps

*Best Case:
  * O(n) comparisons
  * O(1) swaps

*Average Case:
  * O(n<sup>2</sup>) comparisons
  * O(n<sup>2</sup>) swaps
  
*Worst Case Space: O(n)






