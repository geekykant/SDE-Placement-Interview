### Bit Manipulation

**Swap Two Nos**
```cpp
pair<int, int> swap(int a, int b) {
    a = a ^ b;
    b ^= a;
    a ^= b;
    return {a, b};
}
```

**Set the ith bit**
> num |= (1 << i);

**Check if the ith bit is set**
> num & (1 << i)
