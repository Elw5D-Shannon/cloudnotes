
## 一、**基础统计函数**

### 1. **中心趋势度量**
```python
import numpy as np
arr = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9])
# 平均值
mean_val = np.mean(arr)  # 5.0
# 中位数
median_val = np.median(arr)  # 5.0
# 加权平均值
weights = np.array([1, 1, 1, 2, 2, 2, 3, 3, 3])  # 权重
weighted_mean = np.average(arr, weights=weights)  # 约5.333
# 众数（需要SciPy）
from scipy import stats
mode_val = stats.mode(arr)  # 众数和出现次数
```

### 2. **离散程度度量**
```python
# 标准差（与np.std()相同）
std_val = np.std(arr)  # 总体标准差
std_sample = np.std(arr, ddof=1)  # 样本标准差（无偏估计）
# 方差
var_val = np.var(arr)  # 总体方差
var_sample = np.var(arr, ddof=1)  # 样本方差
# 极差（最大值-最小值）
range_val = np.ptp(arr)  # 8
# 分位数
q25 = np.percentile(arr, 25)  # 25%分位数，2.5
q50 = np.percentile(arr, 50)  # 中位数，5.0
q75 = np.percentile(arr, 75)  # 75%分位数，7.5
# 四分位距（IQR）
q75_val = np.percentile(arr, 75)
q25_val = np.percentile(arr, 25)
iqr_val = q75_val - q25_val  # 5.0
```

### 3. **高阶统计量**
```python
# 偏度（衡量分布不对称性）
from scipy.stats import skew
skewness = skew(arr)  # 对称数据接近0
# 峰度（衡量分布尖锐程度）
from scipy.stats import kurtosis
kurt = kurtosis(arr)  # 正态分布为0
# 协方差矩阵
arr1 = np.array([1, 2, 3, 4, 5])
arr2 = np.array([5, 4, 3, 2, 1])
cov_matrix = np.cov(arr1, arr2)  # 2x2协方差矩阵
# 相关系数
corr_coef = np.corrcoef(arr1, arr2)  # -1.0（完全负相关）
```

## 二、**数学运算函数**

### 1. **基本数学运算**
```python
arr = np.array([1, 4, 9, 16, 25])
# 平方根
sqrt_arr = np.sqrt(arr)  # [1., 2., 3., 4., 5.]
# 指数
exp_arr = np.exp(arr)  # e的arr次方
# 对数
log_arr = np.log(arr)  # 自然对数
log10_arr = np.log10(arr)  # 以10为底
log2_arr = np.log2(arr)  # 以2为底
# 绝对值
abs_arr = np.abs(np.array([-1, -2, 3, -4]))  # [1, 2, 3, 4]
# 符号函数
sign_arr = np.sign(np.array([-5, 0, 5]))  # [-1, 0, 1]
```

### 2. **三角函数**
```python
angles = np.array([0, np.pi/6, np.pi/4, np.pi/3, np.pi/2])
# 正弦、余弦、正切
sin_val = np.sin(angles)
cos_val = np.cos(angles)
tan_val = np.tan(angles)
# 反三角函数
arcsin_val = np.arcsin([0, 0.5, 1])  # 反正弦
arccos_val = np.arccos([0, 0.5, 1])  # 反余弦
arctan_val = np.arctan([0, 1, np.inf])  # 反正切
# 角度弧度转换
degrees = np.degrees(np.pi)  # 180.0
radians = np.radians(180)  # π
```

### 3. **舍入函数**
```python
arr = np.array([1.234, 2.567, 3.891])
# 四舍五入
rounded = np.round(arr, 2)  # [1.23, 2.57, 3.89]
# 向下取整
floor_arr = np.floor(arr)  # [1., 2., 3.]
# 向上取整
ceil_arr = np.ceil(arr)  # [2., 3., 4.]
# 截断取整
trunc_arr = np.trunc(arr)  # [1., 2., 3.]
# 最近整数
rint_arr = np.rint(arr)  # [1., 3., 4.]
```

## 三、**线性代数函数**

### 1. **矩阵运算**
```python
# 创建矩阵
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])
# 矩阵乘法
matmul = np.matmul(A, B)  # 或 A @ B
# [[19, 22],
#  [43, 50]]
# 点积
dot_product = np.dot(A, B)  # 对于矩阵就是矩阵乘法
# 内积
inner_product = np.inner(A, B)  # 另一种点积形式
# 外积
outer_product = np.outer([1, 2, 3], [4, 5, 6])
# [[ 4,  5,  6],
#  [ 8, 10, 12],
#  [12, 15, 18]]
```

### 2. **矩阵分解与特征值**
```python
# 行列式
det_A = np.linalg.det(A)  # -2.0
# 逆矩阵
inv_A = np.linalg.inv(A)  # 如果矩阵可逆
# 伪逆（广义逆）
pinv_A = np.linalg.pinv(A)  # 即使不可逆也可计算
# 特征值和特征向量
eigenvalues, eigenvectors = np.linalg.eig(A)
# 奇异值分解（SVD）
U, S, Vh = np.linalg.svd(A)
# QR分解
Q, R = np.linalg.qr(A)
# Cholesky分解（正定矩阵）
C = np.array([[4, 2], [2, 3]])  # 正定矩阵
L = np.linalg.cholesky(C)  # 下三角矩阵
```

### 3. **矩阵范数与秩**
```python
# 矩阵范数
norm_fro = np.linalg.norm(A, 'fro')  # Frobenius范数
norm_1 = np.linalg.norm(A, 1)  # 1-范数
norm_2 = np.linalg.norm(A, 2)  # 2-范数（最大奇异值）
norm_inf = np.linalg.norm(A, np.inf)  # 无穷范数
# 矩阵的秩
rank_A = np.linalg.matrix_rank(A)  # 2
# 矩阵的迹（对角线元素和）
trace_A = np.trace(A)  # 5
# 矩阵的条件数
cond_A = np.linalg.cond(A)  # 条件数（衡量矩阵病态程度）
```

## 四、**随机数生成与统计**

### 1. **随机数生成**
```python
# 设置随机种子（可重复性）
np.random.seed(42)
# 均匀分布
uniform_arr = np.random.uniform(0, 1, 10)  # [0,1)均匀分布
# 正态分布
normal_arr = np.random.normal(0, 1, 10)  # 均值0，标准差1
# 其他常见分布
binomial_arr = np.random.binomial(10, 0.5, 10)  # 二项分布
poisson_arr = np.random.poisson(5, 10)  # 泊松分布
exponential_arr = np.random.exponential(1, 10)  # 指数分布
```

### 2. **统计检验相关**
```python
# 直方图统计
data = np.random.normal(0, 1, 1000)
hist, bin_edges = np.histogram(data, bins=10)
# 累积分布
cumulative_sum = np.cumsum(data)
# 移动平均
window_size = 5
moving_avg = np.convolve(data, np.ones(window_size)/window_size, mode='valid')
# 百分位数计算
percentiles = np.percentile(data, [25, 50, 75, 90, 95, 99])
```

## 五、**数组操作与聚合**

### 1. **聚合操作**
```python
arr_2d = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
# 求和
total_sum = np.sum(arr_2d)  # 45
sum_rows = np.sum(arr_2d, axis=0)  # 按列求和 [12, 15, 18]
sum_cols = np.sum(arr_2d, axis=1)  # 按行求和 [6, 15, 24]
# 累积和
cumulative = np.cumsum(arr_2d)  # 展平后的累积和
# 乘积
total_prod = np.prod(arr_2d)  # 362880
prod_rows = np.prod(arr_2d, axis=0)  # 按列求积
# 最小/最大值
min_val = np.min(arr_2d)  # 1
max_val = np.max(arr_2d)  # 9
min_idx = np.argmin(arr_2d)  # 最小值的索引（展平后）
# 沿轴聚合
min_per_col = np.amin(arr_2d, axis=0)  # 每列最小值 [1, 2, 3]
max_per_row = np.amax(arr_2d, axis=1)  # 每行最大值 [3, 6, 9]
```

### 示例：**线性回归**
```python
def linear_regression(X, y):
    """最小二乘法线性回归"""
    # 添加截距项
    X_with_intercept = np.column_stack([np.ones(len(X)), X])
    
    # 计算参数：β = (X^T X)^{-1} X^T y
    XTX_inv = np.linalg.inv(X_with_intercept.T @ X_with_intercept)
    beta = XTX_inv @ X_with_intercept.T @ y
    
    # 预测
    y_pred = X_with_intercept @ beta
    
    # R^2分数
    ss_res = np.sum((y - y_pred) ** 2)
    ss_tot = np.sum((y - np.mean(y)) ** 2)
    r_squared = 1 - (ss_res / ss_tot)
    
    return beta, y_pred, r_squared
```

## 八、**常用函数速查表**

| 类别 | 函数 | 功能描述 |
|------|------|----------|
| **统计** | `np.mean()`, `np.median()` | 均值、中位数 |
| | `np.std()`, `np.var()` | 标准差、方差 |
| | `np.percentile()`, `np.quantile()` | 分位数 |
| | `np.corrcoef()`, `np.cov()` | 相关系数、协方差 |
| **数学** | `np.sqrt()`, `np.exp()`, `np.log()` | 平方根、指数、对数 |
| | `np.sin()`, `np.cos()`, `np.tan()` | 三角函数 |
| | `np.round()`, `np.floor()`, `np.ceil()` | 舍入函数 |
| **线性代数** | `np.linalg.inv()`, `np.linalg.det()` | 逆矩阵、行列式 |
| | `np.linalg.eig()`, `np.linalg.svd()` | 特征值、奇异值分解 |
| | `np.linalg.norm()`, `np.linalg.cond()` | 范数、条件数 |
| **随机** | `np.random.rand()`, `np.random.randn()` | 均匀、正态分布 |
| | `np.random.randint()`, `np.random.choice()` | 整数、随机选择 |
| **聚合** | `np.sum()`, `np.prod()`, `np.cumsum()` | 求和、乘积、累积和 |
| | `np.min()`, `np.max()`, `np.argmin()` | 最小、最大值及索引 |

