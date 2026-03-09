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
辗转相除法求最小公约数。
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



当 $b = 0$ 时：
- $gcd(a, 0) = a$
- 方程变为：$a \cdot x + 0 \cdot y = a$
- 显然有一组解：$x = 1, y = 0$
当 $b 不为零0$ 时：
假设我们知道了下一层的解 $(x', y')$ 满足：
$b \cdot x' + (a \bmod b) \cdot y' = gcd(b, a \bmod b)$

根据欧几里得算法：
$gcd(a, b) = gcd(b, a \bmod b)$
所以：
$b \cdot x' + (a \bmod b) \cdot y' = gcd(a, b) \tag{1}$

由
$a \bmod b = a - \lfloor \frac{a}{b} \rfloor \cdot b$
可知
$b \cdot x' + (a - \lfloor \frac{a}{b} \rfloor \cdot b) \cdot y' = gcd(a, b)$

整理得：

$a \cdot y' + b \cdot (x' - \lfloor \frac{a}{b} \rfloor \cdot y') = gcd(a, b) \tag{2}$



比较 $ax + by = gcd(a, b)$ 和 (2) 式：

$$\begin{cases}

x = y' \\

y = x' - \lfloor \frac{a}{b} \rfloor \cdot y'

\end{cases}$$

EXGCD 的时间复杂度与 GCD 相同，为 O(log min(a, b))