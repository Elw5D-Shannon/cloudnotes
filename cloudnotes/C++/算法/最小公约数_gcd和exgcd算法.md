# 基本 gcd

欧几里得算法

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

## exgcd

拓展欧几里得算法，
可以求解方程 $ax+by=gcd(a,b)$ 的一组整数解 $(x,y)$。

```cpp

// 返回 gcd(a,b)，并求出 x,y 满足 ax + by = gcd(a,b)
long long exgcd(long long a, long long b, long long &x, long long &y) {
    if (b == 0) {
        x = 1;
        y = 0;
        return a;
    }
    long long g = exgcd(b, a % b, y, x);
    y -= (a / b) * x;
    return g;
}
```