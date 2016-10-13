Complexity
==========

## Time Complexity
* Linear, directly proportional to n:
```C
for ( i = 0; i < N; i++ )
     statement;
```
* Quadratic, proportional to the square of n because of nested loops:
```C
for ( i = 0; i < N; i++ ) {
  for ( j = 0; j < N; j++ )
    statement;
}
```
* Logarithmic, the algorithm divides the input in half:
```C
while ( low <= high ) {
  mid = ( low + high ) / 2;
  if ( target < list[mid] )
    high = mid - 1;
  else if ( target > list[mid] )
    low = mid + 1;
  else break;
}
```
* N * logn, the program consists of n loops of a logarithmic function:
```C
void quicksort ( int list[], int left, int right )
{
  int pivot = partition ( list, left, right );
  quicksort ( list, left, pivot - 1 );
  quicksort ( list, pivot + 1, right );
}
```

## Space Complexity
* Space complexity accounts for the input size as well as auxilary spaced used