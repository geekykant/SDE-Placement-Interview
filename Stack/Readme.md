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
