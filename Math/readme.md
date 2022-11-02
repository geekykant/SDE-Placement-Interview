## Math

1. Permuation
```cpp
int factorial(int n) {
    if (n == 1) return 1;
    return n * factorial(n - 1);
}

int permutation(int n, int r) {
    return factorial(n) / factorial(n - r);
}
```

2. Combination

> Method 1 - using factorial
```cpp
int factorial(int n) {
    if (n == 1) return 1;
    return n * factorial(n - 1);
}

int combination(int n, int r) {
    return factorial(n) / factorial(n - r) * factorial(r);
}
```

> Method 2 - comb(n, k) = comb(n-1, k) + comb(n-1, k-1);
```cpp
int comb(int n, int k) {
    if (k == 0) return 1;
    if (n == k) return 1;  // or if (n == 0) return 0;
    return comb(n - 1, k) + comb(n - 1, k - 1);
}
```

3. GCD
```cpp
int gcd(int a, int b) {
    if (b == 0) return a;
    return gcd(b, a % b);
}
```

4. LCM
```cpp
long long lcm(int a, int b) {
    return (a / (gcd(a, b))) * b;
}
```
