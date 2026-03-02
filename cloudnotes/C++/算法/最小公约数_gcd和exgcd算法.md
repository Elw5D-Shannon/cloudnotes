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
## exgcd 的推导过程

对于方程：ax+by=gcd⁡(a,b)ax+by=gcd(a,b)

**递归过程**：

1. 当 b=0b=0 时，gcd⁡(a,0)=agcd(a,0)=a，方程变为 ax=aax=a，取 x=1,y=0x=1,y=0
    
2. 当 b≠0b=0 时，先求解：
    
    bx′+(a%b)y′=gcd⁡(b,a%b)bx′+(a%b)y′=gcd(b,a%b)
    
    注意 gcd⁡(a,b)=gcd⁡(b,a%b)gcd(a,b)=gcd(b,a%b)
    
3. 而 a%b=a−⌊a/b⌋×ba%b=a−⌊a/b⌋×b，代入：
    
    bx′+(a−⌊a/b⌋×b)y′=gcd⁡(a,b)bx′+(a−⌊a/b⌋×b)y′=gcd(a,b)ay′+b(x′−⌊a/b⌋×y′)=gcd⁡(a,b)ay′+b(x′−⌊a/b⌋×y′)=gcd(a,b)
4. 与原方程比较：
    
    ax+by=gcd⁡(a,b)ax+by=gcd(a,b)
    
    得到：
    
    x=y′,y=x′−⌊a/b⌋×y′x=y′,y=x′−⌊a/b⌋×y′

这就是为什么代码中先递归调用 `exgcd(b, a % b, y, x)`，然后 `y -= (a / b) * x`。