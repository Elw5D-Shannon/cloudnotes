# 基本 gcd

```cpp
// 计算最大公约数
long long gcd(long long a, long long b) {
    while (b) {
        long long temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}
// 或递归写法
long long gcd(long long a, long long b) {
    return b == 0 ? a : gcd(b, a % b);
}
```

