#2. **Sort an array of 0’s 1’s 2’s without using extra space or sorting algo**

Given an array with n objects colored red, white or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

Note: You are not suppose to use the library's sort function for this problem.

```
Input: [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]
```

**Python (Best)**
```python
def sortColors(nums):
    low = mid = 0
    high = len(nums)-1

    while(mid<=high):
        if nums[mid] == 0:
            nums[mid], nums[low] = nums[low],nums[mid]
            mid+=1
            low+=1
        elif nums[mid] == 2:
            nums[mid], nums[high] = nums[high],nums[mid]
            high-=1
        else:
            mid+=1

    return nums
```

**C++ (Best)**
```cpp
vector<int> sortColors(vector<int>& nums) {
	int low, mid, high;
	low = mid = 0;
	high = nums.size() - 1;

	while (mid <= high)
		switch (nums[mid]) {
		case 0:
			swap(nums[mid], nums[low]);
			mid++;
			low++;
			break;
		case 2:
			swap(nums[mid], nums[high]);
			high--;
			break;
		case 1:
			mid++;
			break;
		}
	return nums;
}
```
