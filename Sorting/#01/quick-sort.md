###  #01. Quick Sort

**CPP**
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

vector<int> sortArray(vector<int>& nums) {
    quickSort(nums, 0, nums.size() - 1);
    return nums;
}
```

## 3-Way Quick Sort

```python
def mergeSort(nums):
    if len(nums) == 0 or len(nums) == 1:
        return nums

    mid = nums[-1]
    
    mids = [num for num in nums if num == mid]
    low = [num for num in nums if num < mid]
    high = [num for num in nums if num > mid]
    
    return mergeSort(low) + mids + mergeSort(high)
```


**Python** (No duplicate elements)
```python
def mergeSort(nums):
    if len(nums) == 0 or len(nums) == 1:
        return nums
        
    mid = nums[-1] 
    low = [num for num in nums if num < mid]
    high = [num for num in nums if num > mid]
    
    return mergeSort(low) + [mid] + mergeSort(high)
```

**Working**
<br><br>
Gfg Link - <a href="https://www.geeksforgeeks.org/quick-sort/">https://www.geeksforgeeks.org/quick-sort/</a>
<img src="https://www.geeksforgeeks.org/wp-content/uploads/gq/2014/01/QuickSort2.png">
