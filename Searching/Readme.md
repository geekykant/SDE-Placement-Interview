## Searching

### Binary Search (Sorted) - O(log2n)

```
arr[] = {10, 20, 30, 40, 50}
x = 20
```

```cpp
int binarySeach(int arr[], int n, int x) {
	int low = 0, high = n - 1;
	int mid;

	while (low <= high) {
		mid = (low + high) / 2;

		if (arr[mid] == x)
			return mid;
		else if (arr[mid] > x)
			high = mid - 1;
		else
			low = mid + 1;
	}

	return -1;
}
```

### Recursive Binary Search (Sorted) - O(log2n)

```cpp
int bSeach(int arr[], int low, int high, int x) {
	int mid = (low + high) / 2;
	if (arr[mid] == x)
		return mid;

	if (arr[mid] > x)
		return bSeach(arr, low, mid - 1, x);
	else
		return bSeach(arr, mid + 1, high, x);
}
```

**Extension problem** - Count Ones

```cpp
int countOnes(int arr[], int low, int high) {
	int mid = (low + high) / 2;
  if ((mid == high || arr[mid + 1] == 0) && arr[mid] == 1)
		return mid + 1;

	if (arr[mid] == 0)
		return countOnes(arr, low, mid - 1);
	else
		return countOnes(arr, mid + 1, high);
}
```
