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
* Worst Case: O(n<sup>2</sup>)
* Best Case: O(n<sup>2</sup>)
* Average Case: O(n<sup>2</sup>)
* Worst Case Space: O(n)


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
* Worst Case:
  * O(n<sup>2</sup>) comparisons
  * O(n<sup>2</sup>) swaps
* Best Case:
  * O(n) comparisons
  * O(1) swaps
* Average Case:
  * O(n<sup>2</sup>) comparisons
  * O(n<sup>2</sup>) swaps
* Worst Case Space: O(n)


## Merge Sort
* Divide an unsorted list into n sublists, each containing one element
* Repeatedly merge the sublists to create larger sorted sublists

> 14  7  3  12  9  11  6  2

> [14  7  3  12]  [9  11  6  2]

> [14  7] [3  12]  [9  11]  [6  2]

> [14]  [7]  [3]  [12]  [9]  [11]  [6]  [2]

> [7  14]  [3  12]  [9  11]  [2  6]

> [3  7  12  14]  [2  6  9  11]

> [2  3  6  7  9  11  12  14]

##### Implementation
```C++
void merge(int arr[], int l, int m, int r) {
	int i, j, k;
	int n1 = m - l + 1;
	int n2 = r - m;

	int L[n1], R[n2];

	/* Copy data to temp arrays L[] and R[] */
    for (i = 0; i < n1; i++)
        L[i] = arr[l + i];
    for (j = 0; j < n2; j++)
        R[j] = arr[m + 1+ j];

    /* Merge the temp arrays back into arr[l..r]*/
    i = 0; // Initial index of first subarray
    j = 0; // Initial index of second subarray
    k = l; // Initial index of merged subarray
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k] = L[i];
            i++;
        } else {
            arr[k] = R[j];
            j++;
        }

        k++;
    }

	/* Copy the remaining elements of L[], if there are any */
    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }
 
    /* Copy the remaining elements of R[], if there are any */
    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}
 
/* l is for left index and r is right index of the sub-array of arr to be sorted */
void mergeSort(int arr[], int l, int r) {
    if (l < r) {
        // Same as (l+r)/2, but avoids overflow for
        // large l and h
        int m = l+(r-l)/2;
 
        // Sort first and second halves
        mergeSort(arr, l, m);
        mergeSort(arr, m+1, r);
 
        merge(arr, l, m, r);
    }
}
```

##### Complexity
* Worst Case: O(n logn)
* Best Case: O(n logn)
* Average Case: O(n logn)
* Worst Case Space: O(n)



