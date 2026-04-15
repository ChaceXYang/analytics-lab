# Python 数据分析完整课程笔记
**FreeCodeCamp — Data Analysis with Python (NumPy, Pandas, Matplotlib, Seaborn)**

> 🎯 讲师：Santiago（remoter.com）
> 📚 内容：数据分析概念 → Jupyter → NumPy → Pandas → 数据清洗 → 数据读取 → Matplotlib → Python 基础回顾

---

## 目录

1. [什么是数据分析](#一什么是数据分析)
2. [工具生态与为什么选 Python](#二工具生态与为什么选-python)
3. [数据分析流程](#三数据分析流程)
4. [实战演示：真实数据集速览](#四实战演示真实数据集速览)
5. [Jupyter Notebook 使用指南](#五jupyter-notebook-使用指南)
6. [NumPy 深入讲解](#六numpy-深入讲解)
7. [Pandas 核心操作](#七pandas-核心操作)
8. [数据清洗（Data Cleaning）](#八数据清洗data-cleaning)
9. [从外部导入数据](#九从外部导入数据)
10. [Matplotlib 可视化](#十matplotlib-可视化)
11. [Python 快速回顾](#十一python-快速回顾)

---

## 一、什么是数据分析

### 1.1 定义（来自 Wikipedia）

> 数据分析是一个**检查、清洗、转换和建模数据**的过程，目标是发现有用信息、形成结论并支持决策制定。

### 1.2 四个核心环节

| 环节 | 说明 | 使用工具 |
|------|------|----------|
| **收集与清洗** | 从各种来源获取数据并整理 | Pandas |
| **建模** | 用统计方法提取规律和模式 | Pandas 统计功能 |
| **发现结论** | 找出有价值的模式或异常值 | Matplotlib / Seaborn |
| **报告与决策支持** | 创建可读报告，供各部门使用 | 可视化 + 导出 |

**核心思想**：把"数据"变成"信息"。
> 例：沃尔玛所有销售记录 → "果味饼干在周二卖得最好" 就是信息。

---

## 二、工具生态与为什么选 Python

### 2.1 两大类工具

| 类型 | 代表工具 | 优势 | 劣势 |
|------|----------|------|------|
| **封闭/托管工具** | Excel、Tableau、Looker | 易学、有官方支持、开箱即用 | 功能边界固定，无法突破 |
| **开放/编程语言** | Python、R、Julia | 极度灵活、通用、可集成任何数据源 | 学习曲线陡峭 |

### 2.2 为什么选 Python？

- **简单直观**：最适合初学者的编程语言之一
- **生态丰富**：数千个库，涵盖密码学、IoT、机器学习等
- **免费开源**：全球智慧贡献，代码质量有保障
- **企业级稳定**：Google、Bank of America 等机构每天依赖 Python
- **社区活跃**：文档详尽，免费教程众多
- **薪资优势**（PayScale 数据）：懂 Python + SQL 的数据分析师收入更高

### 2.3 Python vs R

| | Python | R |
|-|--------|---|
| 易学程度 | ✅ 更容易上手 | 稍难 |
| 通用性 | ✅ 更广泛 | 偏学术/统计 |
| 统计库 | 丰富 | ✅ 极其丰富 |
| 推荐场景 | 通用数据分析、工程化 | 高度统计/学术研究领域 |

---

## 三、数据分析流程

```
① 获取数据
   └── 来源：数据库、CSV/Excel 文件、Web API、爬虫

② 清洗数据
   └── 来源越"野生"（如爬虫），清洗工作越繁重

③ 转换与整形
   └── 合并表格、创建新列、重塑数据结构

④ 分析
   └── 提取规律、捕捉趋势或异常值，统计分析是核心

⑤ 输出与报告
   └── 可视化、报告、支持决策
      └── （数据科学项目：可能还要训练机器学习模型）
```

> 📌 **注意**：现实中这个流程不是线性的，而是一个**循环**，分析师在各步骤之间来回跳跃。

### 数据分析 vs 数据科学

| | 数据分析师 | 数据科学家 |
|-|------------|------------|
| 核心技能 | 强沟通、数据可视化、报告叙事 | 更强的编程和数学能力 |
| 主要工作 | 清洗、分析、可视化、报告 | 机器学习、ETL 流程 |

---

## 四、实战演示：真实数据集速览

### 4.1 分析思维：不要"盯着"数据看

这是从 Excel 思维转向 Python 思维最重要的一步：

- **Excel**：常时间盯着数百万行数据（不可能做到）
- **Python**：你的数据在脑子里，你知道它的形状、统计特征，只需关键时刻查阅

### 4.2 标准分析起手式

```python
import pandas as pd

df = pd.read_csv('data.csv')   # 读取数据

df.shape        # (行数, 列数) — 了解数据规模
df.info()       # 列名、类型、非空值数量
df.describe()   # 数值列的统计摘要（均值、最大、最小、分位数等）
df.head()       # 前5行
df.tail()       # 后5行
```

### 4.3 从统计摘要获取洞见（示例）

```
describe() 输出示例：
- 年龄（age）均值 ≈ 35，中位数接近均值 → 分布较对称
- 存在负利润（profit）→ 可能是数据问题或正常的亏损业务
- 最大年龄 87，最小年龄 17 → 值域合理
```

### 4.4 常用分析操作一览

```python
# 查看某列唯一值分布
df['age_group'].value_counts()

# 快速绘图
df['unit_cost'].plot(kind='box')     # 箱线图
df['unit_cost'].plot(kind='hist')    # 直方图
df['unit_cost'].plot(kind='density') # 核密度图

# 相关性矩阵
df.corr()

# 条件筛选
df[df['state'] == 'Kentucky']

# 按组计算平均值
df.groupby('age_group')['revenue'].mean()

# 创建衍生列
df['revenue_per_age'] = df['revenue'] / df['age']

# 批量修改（例：价格整体上涨3%）
df['price'] = df['price'] * 1.03
```

---

## 五、Jupyter Notebook 使用指南

### 5.1 Jupyter 是什么

- 免费开源的**交互式实时编程环境**
- 主要组件：**Jupyter Notebook**（经典版）和 **JupyterLab**（进化版，有文件树、Git 工具等）
- 可在本地安装，也可用云端服务（Google Colab 等）

### 5.2 为什么用 Jupyter？

- 即时反馈：输入代码立刻看到结果，非常适合数据探索
- 支持混合内容：代码 + 文字说明（Markdown）+ 图表 → 可以生成漂亮的 PDF 报告
- Matplotlib 等图表库可以直接在 Notebook 内渲染

### 5.3 核心概念：单元格（Cell）

Jupyter Notebook 的一切都是**单元格**。每个单元格有两种类型：

| 类型 | 说明 |
|------|------|
| **Code（代码）** | 执行 Python 代码，返回结果 |
| **Markdown** | 格式化文本（标题、粗体、链接、图片等） |

切换类型：
- 按 `M` → 切换为 Markdown
- 按 `Y` → 切换为 Python 代码

### 5.4 两种模式

| 模式 | 识别方式 | 行为 |
|------|----------|------|
| **编辑模式（Edit）** | 单元格内有光标 | 任何字符直接输入到单元格中 |
| **命令模式（Command）** | 单元格内容变灰 | 按键触发各种操作（非输入） |

切换方法：
- 编辑模式 → 命令模式：按 `Esc`
- 命令模式 → 编辑模式：按 `Enter`

### 5.5 常用键盘快捷键（命令模式下）

| 快捷键 | 功能 |
|--------|------|
| `A` | 在当前单元格**上方**插入新单元格 |
| `B` | 在当前单元格**下方**插入新单元格 |
| `DD`（连按两次D）| 删除当前单元格 |
| `Z` | 撤销 |
| `X` | 剪切单元格 |
| `C` | 复制单元格 |
| `V` | 粘贴单元格 |
| `M` | 切换为 Markdown |
| `Y` | 切换为代码 |
| `↑` / `↓` | 在单元格间导航 |

### 5.6 执行单元格

| 快捷键 | 效果 |
|--------|------|
| `Ctrl + Enter` | 执行当前单元格，光标**留在原处** |
| `Shift + Enter` | 执行当前单元格，光标**移到下一个** |

### 5.7 执行编号的意义

每次执行代码，单元格左侧会显示执行编号（如 `[7]`）。无论单元格位置怎样变动，编号永远记录**执行顺序**，方便追踪分析过程。

---

## 六、NumPy 深入讲解

### 6.1 NumPy 是什么

- 全称：Numerical Python
- **多维数组处理库**：支持 1D、2D、3D……任意维度的数组
- 底层基础：Pandas、Matplotlib、SciPy 等几乎所有数据科学库都建立在 NumPy 之上

### 6.2 底层原理：为什么 NumPy 比纯 Python 快？

**原因一：固定数据类型（Fixed Types）**

纯 Python 存储一个整数需要记录 4 项信息（对象值、类型、引用计数、大小），约占 **28 字节**。

NumPy 存储整数只需按指定位数：

| 类型 | 位数 | 字节 |
|------|------|------|
| `int8` | 8 位 | 1 字节 |
| `int16` | 16 位 | 2 字节 |
| `int32`（默认） | 32 位 | 4 字节 |
| `int64` | 64 位 | 8 字节 |

> 💡 同样存一个数字，纯 Python 用 28 字节，NumPy 只用 4 字节，内存利用率相差 7 倍。

**原因二：无需类型检查（No Type Checking）**

- Python List 可以混放整数、字符串、布尔等，遍历时需要逐元素检查类型
- NumPy 数组类型统一，**完全跳过类型检查**，速度更快

**原因三：连续内存（Contiguous Memory）**

- Python List：元素指针散落在内存各处，访问需要"跳跃"
- NumPy Array：所有元素**紧挨在一起**，有两大好处：
  - **SIMD 向量化**：一条 CPU 指令同时处理多个数据
  - **高效缓存命中**：连续内存，CPU 缓存读取效率极高

**性能对比实验（讲师演示）**：
- 对 1000 个数求平方和：Python List 耗时 321 微秒，NumPy 耗时仅为其数十分之一
- 随着数据量增大，Python 进入毫秒级，NumPy 仍停留在微秒级

### 6.3 创建数组

```python
import numpy as np

# 一维数组
a = np.array([1, 2, 3])

# 二维数组（矩阵）
b = np.array([[9.0, 8.0, 7.0],
              [6.0, 5.0, 4.0]])

# 指定数据类型
a = np.array([1, 2, 3], dtype='int16')

# 三维数组：继续嵌套列表即可
```

### 6.4 数组的重要属性

```python
a.ndim      # 维度数量（1D/2D/3D...）
a.shape     # 形状，如 (2, 3) 表示 2行3列
a.dtype     # 数据类型，如 int32、float64
a.itemsize  # 每个元素的字节数
a.size      # 元素总数量
a.nbytes    # 总字节数 = size × itemsize
```

### 6.5 索引与切片

```python
# 一维数组
a = np.array([0, 1, 2, 3])
a[0]          # 第1个元素
a[-1]         # 最后一个元素
a[1:3]        # 切片（不含末端）
a[1:6:2]      # 带步长的切片 [起:止:步]

# 二维数组
matrix = np.array([[1, 2, 3, 4, 5, 6, 7],
                   [8, 9, 10, 11, 12, 13, 14]])

matrix[1, 5]      # 第2行第6列 → 13
matrix[0, :]      # 获取整行
matrix[:, 2]      # 获取整列
matrix[0, 1:6:2]  # 第1行，索引1到5，步长2

# 修改元素
matrix[1, 5] = 20
matrix[:, 2] = [1, 2]   # 修改整列（形状要匹配）
```

**三维数组：由外向内（Work Outside In）**

```python
b = np.array([[[1, 2], [3, 4]],
              [[5, 6], [7, 8]]])

# 想取元素 4：先选外层，再选行，再选列
b[0, 1, 1]  # 输出：4
```

### 6.6 特殊数组初始化

```python
np.zeros((3, 4))          # 全零数组
np.ones((4, 2, 2))        # 全一数组，可指定 dtype
np.full((2, 2), 99)       # 自定义填充值
np.full_like(a, 4)        # 按已有数组形状填充

np.random.rand(4, 2)      # 随机小数 [0,1)，注意：直接传整数不是 tuple！
np.random.randint(0, 7, size=(3, 3))  # 随机整数
np.identity(3)            # 单位矩阵
np.repeat(arr, 3, axis=0) # 重复数组
```

### 6.7 广播（Broadcasting）与向量化操作

```python
a = np.array([1, 2, 3, 4])

# 数组与标量的运算（逐元素）
a + 10    # [11, 12, 13, 14]
a * 2     # [2, 4, 6, 8]
a ** 2    # [1, 4, 9, 16]
a += 100  # 原地修改

# 数组之间的运算（形状必须匹配）
b = np.array([10, 10, 10, 10])
a + b     # [11, 12, 13, 14]
```

> ⚠️ **重要**：NumPy 大多数操作是**不可变的（Immutable）**，会返回新数组而不修改原数组。只有 `+=`、`-=` 等复合赋值才会原地修改。

### 6.8 布尔数组与布尔索引（非常重要！）

```python
a = np.array([0, 1, 2, 3])

# 布尔运算产生布尔数组
a >= 2    # [False, False, True, True]

# 用布尔数组过滤数据
a[a >= 2]              # 输出：[2, 3]
a[a > a.mean()]        # 所有大于均值的元素
~(a >= 2)              # 取反（NOT）

# 多条件组合（用 & 和 |，不能用 and/or！）
a[(a >= 1) & (a <= 3)]  # 大于等于1 且 小于等于3
a[(a == 0) | (a == 3)]  # 等于0 或 等于3
```

**布尔数组的本质**：是向量化布尔运算的结果，可直接用作索引来过滤数据。

### 6.9 常用统计函数

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])

np.sum(arr)          # 所有元素之和
np.sum(arr, axis=0)  # 按列求和（纵向）
np.sum(arr, axis=1)  # 按行求和（横向）
np.min(arr)
np.max(arr, axis=0)
arr.mean()
arr.std()            # 标准差
arr.var()            # 方差
```

### 6.10 线性代数

```python
a = np.ones((2, 3))
b = np.full((3, 2), 2)

np.matmul(a, b)          # 矩阵乘法（不是逐元素！）
np.linalg.det(c)         # 行列式
np.linalg.inv(a)         # 逆矩阵
np.linalg.eig(a)         # 特征值和特征向量
```

---

## 七、Pandas 核心操作

> 📌 Pandas 是数据分析最重要的库，底层依赖 NumPy。

### 7.1 两大核心数据结构

| 结构 | 类比 | 特点 |
|------|------|------|
| **Series** | 带标签的 Python 列表 / 字典 | 一维、有序、有索引、类型统一 |
| **DataFrame** | Excel 表格 | 二维、多列 Series 的组合 |

### 7.2 Series 详解

**创建 Series**

```python
import pandas as pd
import numpy as np

# 基础创建
s = pd.Series([35.467, 63.951, 80.940, 60.665, 127.061, 64.511, 318.523])

# 带名称
s.name = 'G7 Population in Millions'

# 带自定义索引
g7_pop = pd.Series(
    [35.467, 63.951, 80.940, 60.665, 127.061, 64.511, 318.523],
    index=['Canada', 'France', 'Germany', 'Italy', 'Japan', 'UK', 'USA']
)
```

**Series 的特点**：
- 既像列表（有序，支持顺序索引 `iloc`）
- 又像字典（有标签，支持标签索引 `loc`）
- 底层是 NumPy 数组（`.values` 可获取）

**访问元素**

```python
g7_pop['Canada']       # 标签索引
g7_pop[0]              # 顺序索引（不推荐，可能与标签冲突）
g7_pop.iloc[0]         # 安全的顺序索引（推荐）
g7_pop.iloc[-1]        # 最后一个

# 多元素选择
g7_pop[['Canada', 'Japan']]
g7_pop.iloc[[0, 2, -1]]

# 切片（注意：标签切片包含末端！）
g7_pop['Canada':'Italy']   # 包含 Italy ← 与 Python 不同！
g7_pop.iloc[0:3]           # 不包含第3个 ← 与 Python 相同
```

**布尔索引**

```python
g7_pop > 70                      # 布尔 Series
g7_pop[g7_pop > 70]              # 过滤：取出大于70的国家
g7_pop[g7_pop > g7_pop.mean()]   # 大于均值

# 多条件
g7_pop[(g7_pop > 80) & (g7_pop < 200)]
g7_pop[(g7_pop > 80) | (g7_pop < 40)]
```

**修改 Series**

```python
g7_pop['Canada'] = 40.5
g7_pop.iloc[-1] = 500
g7_pop[g7_pop < 70] = 99.9   # 布尔索引修改
```

---

### 7.3 DataFrame 详解

**创建 DataFrame**

```python
df = pd.DataFrame({
    'Population': [35.467, 63.951, 80.940, 60.665, 127.061],
    'GDP': [1785387, 2833687, 3874437, 2167744, 4602367],
    'Surface Area': [9984670, 640679, 357114, 301336, 377930],
    'HDI': [0.913, 0.888, 0.916, 0.873, 0.891],
    'Continent': ['America', 'Europe', 'Europe', 'Europe', 'Asia']
}, index=['Canada', 'France', 'Germany', 'Italy', 'Japan'])
```

**查看数据结构**

```python
df.info()      # 列名、类型、非空值数量
df.shape       # (行数, 列数)
df.describe()  # 数值列的统计摘要
df.dtypes      # 各列数据类型
df.columns     # 列名列表
df.index       # 索引
df.head(3)     # 前3行
df.tail(3)     # 后3行
```

**选取数据——三条核心规则**

| 操作 | 语法 | 说明 |
|------|------|------|
| 按索引选行 | `df.loc['Canada']` | 返回 Series（行转置为列） |
| 按位置选行 | `df.iloc[-1]` | 按顺序，最后一行 |
| 选列 | `df['Population']` | 返回整列 Series |

```python
# 行 + 列同时选
df.loc['France':'Italy', 'Population':'GDP']  # 标签切片（含末端）
df.iloc[1:3, 0:2]                              # 位置切片（不含末端）

# 布尔过滤行
df.loc[df['Population'] > 70]
df.loc[df['Population'] > 70, ['Population', 'GDP']]

# 删除行/列
df.drop('Canada')                          # 删除行
df.drop(['Canada', 'Japan'])               # 删除多行
df.drop(columns=['Population', 'HDI'])     # 删除列
```

> ⚠️ **Pandas 操作基本都是不可变的！** `drop`、`rename` 等操作不修改原 DataFrame，需要重新赋值：
> ```python
> df = df.drop('Canada')
> # 或
> df.drop('Canada', inplace=True)
> ```

**修改 DataFrame**

```python
# 新增列
df['Language'] = ['English', 'French', 'German', 'Italian', 'Japanese']

# 修改现有列
df['Language'] = 'English'   # 所有值改为English

# 计算衍生列（广播操作，极快）
df['GDP_per_capita'] = df['GDP'] / df['Population']

# 重命名
df.rename(columns={'HDI': 'Human Development Index'},
          index={'USA': 'United States'})
```

**读取外部数据**

```python
# 读取 CSV（最常用）
df = pd.read_csv('data.csv')

# 常用参数
pd.read_csv('data.csv',
            header=None,                        # 无表头
            names=['timestamp', 'price'],       # 指定列名
            index_col=0,                        # 第一列作为索引
            parse_dates=['timestamp'],          # 解析日期
            na_values=['?', '!', '-'])          # 指定缺失值标记

# 读取 SQL
import sqlite3
conn = sqlite3.connect('chinook.db')
df = pd.read_sql('SELECT * FROM employees LIMIT 5', conn)

# 读取 HTML（直接解析网页表格！）
tables = pd.read_html('https://en.wikipedia.org/...')
df = tables[0]

# 读取 Excel
df = pd.read_excel('products.xlsx', sheet_name='Products')
```

**快速绘图**

```python
df['price'].plot()                    # 折线图
df['price'].plot(kind='hist')         # 直方图
df['price'].plot(kind='box')          # 箱线图
df.plot(kind='scatter', x='age', y='revenue')  # 散点图
```

---

## 八、数据清洗（Data Cleaning）

### 8.1 数据清洗的四个层次

| 层次 | 问题类型 | 难度 | 示例 |
|------|----------|------|------|
| 1 | **缺失值** | 最简单 | 某行没有价格 |
| 2 | **无效值** | 中等 | 价格列里出现字符串 |
| 3 | **域外值** | 较难 | 年龄列出现 170 |
| 4 | **重复值** | 视情况 | 同一记录出现多次 |

### 8.2 处理缺失值（Missing Values）

**在 Pandas 中**，缺失值用 `NaN`（Not a Number）表示，来自 NumPy。

```python
# 判断是否为缺失值
pd.isna(value)     # 或 pd.isnull(value)，两者完全等价
pd.notna(value)    # 或 pd.notnull(value)

# 应用于整个 Series 或 DataFrame
s.isna()           # 返回布尔 Series
df.isna().sum()    # 每列有多少缺失值
df.notna().sum()   # 每列有多少非空值

# 过滤出非空值
s[s.notna()]
```

**删除缺失值**

```python
# Series
s.dropna()         # 返回新 Series，不修改原 Series！

# DataFrame
df.dropna()                    # 删除任何含空值的行
df.dropna(axis=1)              # 删除任何含空值的列
df.dropna(how='all')           # 只删除全为空的行
df.dropna(thresh=3)            # 保留至少有3个非空值的行
```

**填充缺失值**

```python
s.fillna(0)             # 用0填充
s.fillna(s.mean())      # 用均值填充

# 前向填充（用上一个有效值填）
s.fillna(method='ffill')

# 后向填充（用下一个有效值填）
s.fillna(method='bfill')

# 二维表格的轴向填充
df.fillna(method='ffill', axis=0)   # 纵向（列方向）填充
df.fillna(method='ffill', axis=1)   # 横向（行方向）填充
```

### 8.3 处理无效值

```python
# 查看唯一值
df['sex'].unique()
df['sex'].value_counts()  # 更好，还显示计数

# 替换无效值
df['sex'].replace({'F': 'Female', 'M': 'Male'}, inplace=True)
# 多列替换也适用
```

### 8.4 处理重复值

```python
# 识别重复
s.duplicated()                   # 第一个出现的不标记
s.duplicated(keep='last')        # 最后一个出现的不标记
s.duplicated(keep=False)         # 所有重复都标记

# 删除重复
df.drop_duplicates()
df.drop_duplicates(subset=['name'])          # 按特定列判断重复
df.drop_duplicates(subset=['name', 'pos'])   # 多列组合判断
df.drop_duplicates(keep='last')              # 保留最后出现的
```

### 8.5 字符串处理（`.str` 属性）

字符串列有特殊的 `.str` 属性，类比 Python 原生字符串方法：

```python
df['info'].str.split('_', expand=True)     # 分割为多列
df['info'].str.contains('keyword')         # 是否包含
df['info'].str.strip()                     # 去除空白
df['info'].str.replace('old', 'new')       # 替换
df['info'].str.replace(r'regex', 'new')    # 支持正则表达式

# 其他类型的特殊属性
df['date_col'].dt.year        # 日期型列 → .dt 属性
df['cat_col'].cat.codes       # 分类型列 → .cat 属性
```

---

## 九、从外部导入数据

### 9.1 读取 CSV / 文本文件

```python
# 基础
df = pd.read_csv('data.csv')

# 远程 URL（pandas 自动下载！）
df = pd.read_csv('https://raw.githubusercontent.com/.../data.csv')

# 完整参数示例
df = pd.read_csv(
    'data.csv',
    header=None,
    names=['col1', 'col2'],
    index_col=0,
    parse_dates=[0],
    na_values=['?', '!', 'N/A'],
    dtype={'col1': float, 'col2': str},
    sep=','           # 分隔符（也可用 separator=）
)

# 写入 CSV
df.to_csv('output.csv', index=False, sep=',')
```

**常见参数说明**：

| 参数 | 含义 |
|------|------|
| `header=None` | 第一行不是列名 |
| `names=[...]` | 手动指定列名 |
| `index_col=0` | 第一列作为索引 |
| `parse_dates` | 自动解析日期列 |
| `na_values` | 将这些字符串视为缺失值 |
| `dtype` | 强制指定列类型 |
| `skiprows` | 跳过开头的空行 |

### 9.2 读取 SQL 数据库

```python
import sqlite3
import pandas as pd

# 建立连接
conn = sqlite3.connect('database.db')

# 执行查询
df = pd.read_sql('SELECT * FROM employees LIMIT 5', conn)

# 指定索引列 + 日期解析
df = pd.read_sql('SELECT * FROM orders', conn,
                 index_col='order_id',
                 parse_dates=['order_date'])

# 写入 SQL（默认：表存在时报错）
df.to_sql('new_table', conn, if_exists='replace')  # 替换
df.to_sql('new_table', conn, if_exists='append')   # 追加
```

### 9.3 读取 HTML 表格

```python
# 直接解析网页（pandas 自动下载！）
tables = pd.read_html('https://en.wikipedia.org/wiki/...')
df = tables[0]   # 网页上可能有多个表格，选第一个

# 处理多余的头部行（HTML 表格常见问题）
df = df.drop(df[df['Name'] == 'Name'].index)  # 删除重复出现的表头
```

### 9.4 读取 Excel 文件

```python
# 读取第一个 Sheet
df = pd.read_excel('products.xlsx')

# 读取指定 Sheet
df = pd.read_excel('products.xlsx', sheet_name='Merchants')

# 使用 ExcelFile 类（先检查结构再读取）
xls = pd.ExcelFile('products.xlsx')
print(xls.sheet_names)   # ['Products', 'Descriptions', 'Merchants']
df = xls.parse('Products')

# 写入 Excel
df.to_excel('output.xlsx', sheet_name='Sheet1', index=False)

# 写入多个 Sheet
with pd.ExcelWriter('output.xlsx') as writer:
    df1.to_excel(writer, sheet_name='Products')
    df2.to_excel(writer, sheet_name='Merchants')
```

---

## 十、Matplotlib 可视化

### 10.1 两种 API 风格

**全局 API（Pyplot 风格）** — 常见但不推荐：

```python
import matplotlib.pyplot as plt

plt.figure()
plt.title('My Chart')
plt.plot(x, x**2)
plt.plot(x, -x**2)
plt.show()
```

问题：代码执行顺序影响结果，多图时容易混淆。

**面向对象 API（OOP 风格）** — 推荐：

```python
fig, ax = plt.subplots()          # 一个图
ax.plot(x, y, label='line')
ax.set_title('Title')
ax.set_xlabel('X')
ax.legend()
plt.show()

# 多个子图
fig, axes = plt.subplots(2, 2)    # 2行2列，共4个子图
axes[0, 0].plot(x, y)            # 第1行第1列
axes[0, 1].plot(x, y2)           # 第1行第2列
axes[1, 0].scatter(x, y)         # 第2行第1列
```

> 💡 **为什么推荐 OOP API？**
> 每个 `ax` 都是独立对象，操作时明确指向具体的图，不依赖执行顺序，代码更易读、更易调试。

### 10.2 常用图表类型

```python
# 折线图
ax.plot(x, y, 'g.-', lineStyle='-', marker='.', color='green')

# 散点图
ax.scatter(x, y, s=size, c=color, cmap='viridis')

# 直方图
ax.hist(data, bins=30, alpha=0.5)

# 箱线图
ax.boxplot(data)

# 条形图
ax.bar(categories, values)
ax.bar(categories, values, bottom=prev_values)  # 堆叠条形图

# 核密度估计（KDE）
df['col'].plot(kind='density')
```

### 10.3 Pandas 直接绘图

```python
# 从 DataFrame 直接画图（底层调用 Matplotlib）
df.plot()                          # 折线图
df.plot(kind='hist')               # 直方图
df['col'].plot(kind='box')         # 箱线图
df.plot(kind='scatter', x='a', y='b')  # 散点图
df['col'].value_counts().plot(kind='bar')   # 条形图
df['col'].value_counts().plot(kind='pie')   # 饼图
```

---

## 十一、Python 快速回顾

> 适合有其他语言基础、需要快速上手 Python 的读者

### 11.1 基本语法特点

- **用缩进定义代码块**（不用花括号）
- **不需要声明变量类型**（动态类型但强类型）
- **注释**：用 `#`
- **Python 3 为主流**（Python 2 已于 2020 年废弃）

```python
def my_function(x, y=10):   # def 定义函数，y 有默认值
    if x > 0:
        return x + y
    else:
        return 0
```

### 11.2 数据类型

```python
# 数字
age = 25          # int
price = 3.14      # float

# 字符串
name = 'Python'
multi_line = """这是
多行字符串"""

# 布尔
is_active = True
is_empty = False

# None（相当于 null）
result = None
```

### 11.3 核心数据结构

| 结构 | 特点 | 示例 |
|------|------|------|
| **List** | 有序、可变、可混合类型 | `[1, 'a', True]` |
| **Tuple** | 有序、**不可变** | `(1, 2, 3)` |
| **Dict** | 键值对、无序（Python 3.7+ 有序） | `{'name': 'John', 'age': 25}` |
| **Set** | 无序、**唯一值**、成员检查极快 | `{1, 2, 3}` |

```python
# List 操作
lst = [1, 2, 3]
lst.append(4)
4 in lst          # True

# Dict 操作
user = {'name': 'John', 'age': 25}
user['email']     # KeyError 若不存在
user.get('email', 'default')   # 安全访问

# 遍历 Dict
for key in user:             # 只遍历键
for key, val in user.items(): # 键值同时遍历
```

### 11.4 循环

```python
# for 循环（推荐）
names = ['Alice', 'Bob', 'Charlie']
for name in names:
    print(name)

# 模拟数字循环
for i in range(10):
    print(i)

# while（尽量少用，有死循环风险）
while condition:
    ...
```

### 11.5 函数

```python
def add(x, y=0):         # y 有默认值
    return x + y

# 如果没有 return，函数默认返回 None
```

### 11.6 模块导入

```python
import numpy as np                  # 标准导入
from pandas import DataFrame        # 只导入特定对象
import matplotlib.pyplot as plt     # 别名
```

### 11.7 异常处理

```python
try:
    result = int('not a number')
except ValueError as e:
    print(f'Error: {e}')
```

---

## 课程总结

```
Python 数据分析完整工具链

数据获取 → pd.read_csv / read_sql / read_excel / read_html
         ↓
数据探索 → df.info() / df.describe() / df.head() / df.shape
         ↓
数据清洗 → isna() / dropna() / fillna() / replace() / str.xxx
         ↓
数据转换 → 创建新列 / 广播计算 / 布尔过滤 / groupby
         ↓
统计分析 → mean / std / corr / describe
         ↓
可视化   → df.plot() / matplotlib axes API
         ↓
输出导出 → to_csv() / to_excel() / to_sql()
```

> 🔑 **核心理念**：数据分析师不需要时刻"盯着"数据。掌握数据的形状、类型、统计特征，用代码来问问题，用图表来发现规律。
