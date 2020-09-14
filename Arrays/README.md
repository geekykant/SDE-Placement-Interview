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

```
