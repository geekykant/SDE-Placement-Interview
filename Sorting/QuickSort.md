## Quick Sort (No duplicate mid element)

**Python**
```python
def mergeSort(nums):
    if len(nums) == 0 or len(nums) == 1:
        return nums
        
    mid = nums[-1] 
    low = [num for num in nums if num < mid]
    high = [num for num in nums if num > mid]
    
    return mergeSort(low) + [mid] + mergeSort(high)
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

**Working**
<br><br>
Gfg Link - <a href="https://www.geeksforgeeks.org/quick-sort/">https://www.geeksforgeeks.org/quick-sort/</a>
<img src="https://www.geeksforgeeks.org/wp-content/uploads/gq/2014/01/QuickSort2.png">
