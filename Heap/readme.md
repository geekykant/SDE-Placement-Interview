### Heap

### Custom Heap Implementation

**Step 1: Build Heap**
```cpp
/**
 * Essentially we only need to heapify internal nodes which is from [0 to n/2-1]. 
 * This function sets maxHeap to the root node and below subtree roots.
 */
void heapify(vector<int>& nums, int curIdx, int size) {
    int largestIdx = curIdx;
    int l = 2 * curIdx + 1;
    int r = 2 * curIdx + 2;

    if (l < size && nums[l] > nums[largestIdx])
        largestIdx = l;
    if (r < size && nums[r] > nums[largestIdx])
        largestIdx = r;

    if (largestIdx != curIdx) {
        swap(nums[largestIdx], nums[curIdx]);

        // After heapify, it moves to the largest sub-node
        // and again heapifies it
        heapify(nums, largestIdx, size);
    }
}

int main() {
    vector<int> nums = {3, 2, 5, 7, 1, 6, 4};
    
    // Build Heap - Heapify only the internal nodes [0 to n/2-1]
    for (int i = nums.size() / 2 - 1; i >= 0; i--)
        heapify(nums, i, nums.size());

    //Now heap has - 7 3 6 2 1 5 4 - (Only useful to get max/min from heap)
    printVectors(nums); 
    return 0;
}
```

**Step 2: Heap Sort**
```cpp
/**
 * Essentially we only need to heapify internal nodes which is from [0 to n/2-1]. 
 * This function sets maxHeap to the root node and below subtree roots.
 */
void heapify(vector<int>& nums, int curIdx, int size) {
    int largestIdx = curIdx;
    int l = 2 * curIdx + 1;
    int r = 2 * curIdx + 2;

    if (l < size && nums[l] > nums[largestIdx])
        largestIdx = l;
    if (r < size && nums[r] > nums[largestIdx])
        largestIdx = r;

    if (largestIdx != curIdx) {
        swap(nums[largestIdx], nums[curIdx]);

        // After heapify, it moves to the largest sub-node
        // and again heapifies it
        heapify(nums, largestIdx, size);
    }
}

void heapSort(vector<int>& nums) {
    // Heapify only the internal nodes [n/2-1 to 0]
    for (int i = nums.size() / 2 - 1; i >= 0; i--)
        heapify(nums, i, nums.size());

    // The first - 0 element will automatically get sorted.
    // We sort only (n-1) elements and keep removing nodes by one.
    for (int i = nums.size() - 1; i > 0; i--) {
        //swap heap root at 0 with last element
        swap(nums[0], nums[i]);
        heapify(nums, 0, i); //nums.size() reduced to i
    }
}

int main() {
    vector<int> nums = {3, 2, 5, 7, 1, 6, 4};
    heapSort(nums); //ascending order

    printVectors(nums); //Ouput: 1 2 3 4 5 6 7
    return 0;
}
```
