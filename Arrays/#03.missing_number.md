3. **Repeat and Missing Number**

Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the one that is missing from the array.

```
Input: [0,1,2,3,4,6,7,8]
Output: 5
```

**CPP (Best)**
```cpp
int findMissing(vector<int>& nums) {
	int size = nums.size();
	int alg_sum = size * (size + 1) / 2;
	int sum = 0;
	
	for (auto num : nums)
		sum += num;

	return alg_sum - sum;
}
```

**CPP**
```cpp
int findMissing(vector<int>& nums) {
	int xor_result = 0, i = 0;

	for (i = 0; i < nums.size(); i++)
		xor_result = i ^ nums[i] ^ xor_result;

	return i ^ xor_result;
}
```
