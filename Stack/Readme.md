## Stack

Stack is a data structure that follows **FIFO - First In First Out**. - BigO(1)
- **Mostly implemented using deque**
- Also called container adapter

### Applications
- Function call Stack
- Checking for balanced paranthesis
- Reversing items
- Infix to Prefix/Postfix conversion or Evaluation
- **Stack span problem**
- Undo/Redo operation OR Forward/Backward

**Basic Code - CPP**
```cpp
stack<int> s;
s.push(10);
s.push(30);
s.push(40);

cout<<s.size()<<endl;
cout<<s.top()<<endl; //top item
s.pop(); //removes item

cout<<s.top()<<endl;

while(!s.empty()){
  cout<<s.top()<<" ";
  s.pop();
}

```
Implementation
- Stack can be implemented using either **Array or Linked List**

**Monotoically Increasing**

Method 1:
```cpp
stack<int> st;
unordered_map<int, int> nextGreater;
for(int i=nums2.size()-1; i >= 0; i--){
    while(!st.empty() && nums2[i] >= nums2[st.top()]) st.pop();
    if(st.empty())
        nextGreater[nums2[i]] = -1;
    else
        nextGreater[nums2[i]] = nums2[st.top()];

    st.push(i);
}
```

Method 2:
```cpp
unordered_map<int, int> nextGreater;
stack<int> st;
for(int num: nums2){
    while(!st.empty() && num > st.top()){
        nextGreater[st.top()] = num;
        st.pop();
    }
    st.push(num);
}
```

