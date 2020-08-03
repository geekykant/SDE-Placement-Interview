1. Find the duplicate in an array of N+1 integers. 

```
Input: [1,3,4,2,2]
Output: 2
```

**C++**
```cpp
int findDuplicate(vector<int>& nums) {
	for (int i = 0; i < nums.size(); i++)
		if (nums[abs(nums[i])] > 0)
			nums[abs(nums[i])] = -nums[abs(nums[i])];
		else
			return abs(nums[i]);
	return -1;
}
```

**Python**
```python
def findDuplicate(nums):
    for i in range(len(nums)):
        if nums[abs(nums[i])] > 0:
            nums[abs(nums[i])] = -nums[abs(nums[i])];
        else:
            return abs(nums[i]);
    return None
```
