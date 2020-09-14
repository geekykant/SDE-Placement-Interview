# Arrays

Array is a collection of similar datatype values. There are both static and dynamic arrays.

*For CPP*,
static -> int arr[10];<br>
dynamic -> vector<int> arr;


#1. Finding second largest element in array

```cpp
int secondLargest(int arr[], int n) {
	int largest = arr[0], secondLargest = -1;

	for (int i = 0; i < n; i++)
		if (arr[i] > largest) {
			secondLargest = largest;
			largest = arr[i];
		}

	return secondLargest;
}
```

#2. Shifting zeros element to last

```cpp
void lastZeros(int& arr[], int n) {
	int count = 0;

  for (int i = 0; i < n; i++)
		if (arr[i] != 0) {
			swap(arr[i], arr[count]);
			count++;
		}
}
```

#3. Reverse an array

```cpp
void reverseArray(int arr[], int n) {
	int low = 0, high = n - 1;

	while (low < high) {
		swap(arr[low], arr[high]);
		low++, high--;
	}
}
```

#4. Left rotate an array by a number (m)

```cpp
void leftRotate(int arr[], int n, int m) {
	int new_arr[n];

	for (int i = 0; i < n; i++) {
		int pos = (i - m) % 4;
		if (pos < 0)
			pos += n;
		
		new_arr[pos] = arr[i];
	}

	printSolution(new_arr, n);
}
```

#5. Equilibrium index of an array

Equilibrium index of an array is an index such that the sum of elements at lower indexes is equal to the sum of elements at higher indexes.

```
Input: [-7, 1, 5, 2, -4, 3, 0]
Output: 3
A[0] + A[1] + A[2] = A[4] + A[5] + A[6]
```

```cpp
int eqindex(int arr[], int n) {
	int sum = 0, leftsum = 0;

	for (int i = 0; i < n ; i++)
		sum += arr[i];

	for (int i = 0; i < n; i++) {
		sum -= arr[i];
		if (sum == leftsum)
			return i;

		leftsum += arr[i];
	}

	return -1;
}
```
