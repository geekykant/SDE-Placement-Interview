4. Given an unsorted array of size n. Array elements are in the range from 1 to n. One number from set {1, 2, …n} is missing and one number occurs twice in the array. 
Find these two numbers.

```
Input: arr[] = {3, 1, 3}
Output: Missing = 2, Repeating = 3
```

**CPP (Best)**
```cpp
void findMissingDuplicate(vector<int>& nums) {
	for (int i = 0; i < nums.size(); i++)
		if (nums[abs(nums[i]) - 1 ] > 0)
			nums[abs(nums[i]) - 1] = -nums[abs(nums[i]) - 1];
		else
			cout << "Duplicate No:" << abs(nums[i]) << " ";

	for (int i = 0; i < nums.size(); i++)
		if (nums[i] > 0)
			cout << "Missing No:" << (i + 1);

}
```
