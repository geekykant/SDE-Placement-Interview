### Sorting Techniques

#### 1. Bubble Sort - O(N^2)

```cpp
void sortNums(vector<int> &nums) {
	int n = nums.size();

	for (int i = 0; i < n; i++)
		for (int j = 0; j < n - i - 1; j++)
			if (nums[j] > nums[j + 1])
				swap(nums[j], nums[j + 1]);
}
```

#### 2. Quick Sort - O(N^2)

```cpp
int partition(vector<int>& nums, int l, int r) {
    int pivot = nums[r];
    int i = l - 1;

    for (int j = l; j < r; ++j) {
        if (nums[j] <= pivot) {
            i++;
            swap(nums[i], nums[j]);
        }
    }
    swap(nums[i + 1], nums[r]);
    return i + 1;
}

void quickSort(vector<int>& nums, int l, int r) {
    if (l < r) {
        int pi = partition(nums, l, r);
        quickSort(nums, l, pi - 1);
        quickSort(nums, pi + 1, r);
    }
}
```

#### 3. Selection Sort - O(Nlogn)
```cpp
void sortSelection(vector<int>& nums) {
    for (int i = 0; i < nums.size(); i++) {
        int minJ = i;
        for (int j = i; j < n; j++)
            if (nums[j] < nums[minJ])
                minJ = j;
        swap(nums[i], nums[minJ]);
    }
}
```

#### 4. Merge Sort - O(Nlogn)

```cpp
void merge(vector<int>& nums, int l, int m, int r) {
    int n1 = m - l + 1, n2 = r - m;
    vector<int> L(n1), R(n2);

    for (int i = 0; i < n1; i++)
        L[i] = nums[i + l];
    for (int j = 0; j < n2; j++)
        R[j] = nums[m + j + 1];

    int i = 0, j = 0, k = l;
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            nums[k] = L[i++];
        } else {
            nums[k] = R[j++];
        }
        k++;
    }

    while (i < n1) {
        nums[k++] = L[i++];
    }
    while (j < n2) {
        nums[k++] = R[j++];
    }
}

void mergeSort(vector<int>& nums, int l, int r) {
    if (l < r) {
        int m = l + (r - l) / 2;

        mergeSort(nums, l, m);
        mergeSort(nums, m + 1, r);
        merge(nums, l, m, r);
    }
}
```
