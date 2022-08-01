### Segment Trees

- A Segment Tree is a data structure that stores information about array intervals as a tree.
- This allows answering range queries over an array efficiently, while still being flexible enough to allow quick modification of the array. 

> Segment Tree is useful when the array has many "update" operations in intervals. [Read more](https://cp-algorithms.com/data_structures/segment_tree.html)

Video Tutorial - https://www.youtube.com/watch?v=2bSS8rtFym4&ab_channel=TECHDOSE

#### C++ Code
<img width="820" src="https://user-images.githubusercontent.com/27401142/182177229-6db97527-7130-403a-ae90-0032b5e4f39c.png">

```cpp
void updateValue(vector<int>& st, int start, int end, int updatingIdx, int diff, int idx) {
    // To be updated idx is outside range
    if (updatingIdx < start || updatingIdx > end)
        return;

    //Idx is in the range of this node, update the value
    // of this node and its children
    st[idx] += diff;
    if (start != end) {
        int mid = start + (end - start) / 2;
        updateValue(st, start, mid, updatingIdx, diff, 2 * idx + 1);
        updateValue(st, mid + 1, end, updatingIdx, diff, 2 * idx + 2);
    }
}

int getSum(vector<int>& st, int start, int end, int searchStartIdx, int searchEndIdx, int idx) {
    // Case 1: Full overlaping condition
    // Segment of the node is part of the range
    // --searchStartIdx-- start ---- end ---searchEndIdx---
    if (searchStartIdx <= start && searchEndIdx >= end)
        return st[idx];

    // Case 2: NO-overlap condition
    // ---end -- searchStartIdx--
    // ---searchEndIdx -- start--
    if (end < searchStartIdx || start > searchEndIdx)
        return 0;

    // Case 3: Partial Overlap
    int mid = start + (end - start) / 2;
    return getSum(st, start, mid, searchStartIdx, searchEndIdx, 2 * idx + 1) +
           getSum(st, mid + 1, end, searchStartIdx, searchEndIdx, 2 * idx + 2);
}

int fillSTValues(vector<int>& nums, vector<int>& st, int start, int end, int idx) {
    // If there is only single element in array, store in st
    // and return it
    if (start == end) {
        st[idx] = nums[start];
        return nums[start];
    }

    // Split at any pivot into left and right subtrees
    // and store their sum into current node
    int mid = start + (end - start) / 2;
    st[idx] = fillSTValues(nums, st, start, mid, 2 * idx + 1) +
              fillSTValues(nums, st, mid + 1, end, 2 * idx + 2);

    return st[idx];
}

void buildST(vector<int>& nums, vector<int>& st) {
    //allocate memory for segement tree
    int n = nums.size();
    int x = (int)(ceil(log2(n)));

    //Maximum size of segment tree
    int max_size = 2 * (int)pow(2, x) - 1;

    st.resize(max_size);
    fillSTValues(nums, st, 0, n - 1, 0);
}

int main() {
    vector<int> nums = {1, 3, 5, 7, 9, 11};
    int n = nums.size();

    //build segment tree
    vector<int> st;
    buildST(nums, st);

    //Find sum in range - output = 32
    int searchStartIdx = 2, searchEndIdx = 5;
    cout << getSum(st, 0, n - 1, searchStartIdx, searchEndIdx, 0) << endl;

    //Update value
    int newValue = 7, updatingIdx = 2;
    int diff = newValue - nums[updatingIdx];
    updateValue(st, 0, n - 1, diff, updatingIdx, 0);

    //Find sum range again - output = 34
    cout << getSum(st, 0, n - 1, searchStartIdx, searchEndIdx, 0) << endl;

    return 0;
}
```
