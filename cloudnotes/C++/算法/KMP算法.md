#未掌握 

**KMP算法**（Knuth-Morris-Pratt算法）是一种**高效的字符串匹配算法**，由三位计算机科学家（Knuth、Morris、Pratt）共同提出。

### 1. 算法要解决的问题

在一个**主串**中查找一个**模式串**出现的位置。

- 主串：`"BBC ABCDAB ABCDABCDABDE"`
    
- 模式串：`"ABCDABD"`
    
- 目标：找出模式串在主串中的位置
    

### 2. 核心思想

KMP的核心思想是：**利用匹配失败后的信息，尽量减少模式串与主串的匹配次数**。

#### 对比传统暴力匹配

- **暴力匹配**：匹配失败后，主串指针回退到下一个字符，模式串指针回退到开头，重新匹配
    
- **KMP算法**：匹配失败后，主串指针**不回退**，只移动模式串到合适的位置继续匹配
    

### 3. 工作原理示意图

假设我们在位置 i 匹配失败：

text

主串:    ... A B C D A B [X] ...
                        ↑
模式串:        A B C D A B [Y]
                        ↑
失败位置:               i

- **暴力法**：主串指针回退到 i-5+1，模式串回退到开头
    
- **KMP**：主串指针**不动**，模式串直接移动到合适位置：
    

text

主串:    ... A B C D A B [X] ...
                        ↑
模式串:                A B C D A B Y
                        ↑
新对齐位置

## next数组

**next数组**是KMP算法的核心，它**预先计算**模式串中每个位置的最长相同前后缀长度。

### 1. 什么是next数组？

next数组是一个预处理数组，`next[j]` 表示：**当模式串第 j 个字符匹配失败时，模式串应该跳转到哪个位置继续匹配**。

更准确地说：`next[j]` = 模式串的前 j 个字符组成的子串中，**最长相等前后缀的长度**。

### 2. 前缀和后缀的概念

以字符串 `"ABCAB"` 为例：

- **前缀**：A、AB、ABC、ABCA（不包含最后一个字符）
    
- **后缀**：B、AB、CAB、BCAB（不包含第一个字符）
    
- **最长相等前后缀**：`"AB"`（长度=2）
    

### 3. 计算next数组示例

模式串：`"ABABC"`

|位置 j|子串|最长相等前后缀|next[j]|
|---|---|---|---|
|0|"A"|无|-1|
|1|"AB"|无|0|
|2|"ABA"|"A"（长度1）|1|
|3|"ABAB"|"AB"（长度2）|2|
|4|"ABABC"|无|0|

### 4. next数组的作用图解

模式串 `"ABABC"`，主串 `"ABABABC"`：

text

步骤1：匹配到位置4失败
主串: A B A B A B C
模式串: A B A B C
            ↑ 这里不匹配（A vs C）
步骤2：查next[4]=2，模式串跳转到位置2
主串: A B A B A B C
模式串:     A B A B C
            ↑ 从位置2继续匹配

### 5. 代码实现
```cpp

// 获取next数组
void getNext(const string& pattern, int next[]) {
    int j = 0, k = -1;
    next[0] = -1;
    int len = pattern.length();
    
    while (j < len - 1) {
        if (k == -1 || pattern[j] == pattern[k]) {
            j++;
            k++;
            next[j] = k;
        } else {
            k = next[k];  // 回溯
        }
    }
}
// KMP搜索算法
int KMP(const string& text, const string& pattern) {
    int next[pattern.length()];
    getNext(pattern, next);
    
    int i = 0, j = 0;
    int tLen = text.length();
    int pLen = pattern.length();
    
    while (i < tLen && j < pLen) {
        if (j == -1 || text[i] == pattern[j]) {
            i++;
            j++;
        } else {
            j = next[j];  // 模式串向右移动
        }
    }
    
    if (j == pLen)
        return i - j;  // 匹配成功，返回起始位置
    else
        return -1;     // 匹配失败
}

```

### 6. next数组的优化（nextval）

有时next数组还可以进一步优化，得到**nextval数组**，避免不必要的比较：
```cpp

// 优化的next数组（nextval）
void getNextval(const string& pattern, int nextval[]) {
    int j = 0, k = -1;
    nextval[0] = -1;
    int len = pattern.length();
    
    while (j < len - 1) {
        if (k == -1 || pattern[j] == pattern[k]) {
            j++;
            k++;
            if (pattern[j] != pattern[k])
                nextval[j] = k;
            else
                nextval[j] = nextval[k];  // 如果相同，继续递归
        } else {
            k = nextval[k];
        }
    }
}

```

### 7. 复杂度分析

|指标|暴力匹配|KMP算法|
|---|---|---|
|最坏时间复杂度|O(m×n)|**O(m+n)**|
|空间复杂度|O(1)|O(n)|
|主串指针|会回溯|**永不回溯**|

其中：

- m = 主串长度
    
- n = 模式串长度
    

### 8. 理解要点

1. **next数组的本质**：一个"失配时的跳转表"
    
2. **核心优势**：主串指针永不回溯，适合处理大文件流式输入
    
3. **适用场景**：
    
    - 主串很大，不能回溯
        
    - 模式串有重复结构（前后缀）
        
    - 需要快速多次匹配
        

### 9. 形象比喻

想象你在查字典找单词：

- **暴力匹配**：每次查错一个字母，就从头开始查
    
- **KMP算法**：你知道"pre"后面可能是"fix"、"sent"等，如果查"prefix"时"x"不对，你知道可以直接跳到"s"开始查"present"，不用回到"p"重新开始
    

这就是KMP的智慧：**利用已知信息，避免重复劳动**。