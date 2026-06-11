# Python 零基础完全教程 —— 物理系学生的编程第一课

> **我是你的 Python 老师。** 本教程假设你之前**完全没有编程经验**，从安装软件开始，一步一步带你掌握 Python，直到能独立写出物理仿真程序。
>
> **教学理念**：不讲计算机科学的历史，不讲底层原理，只讲你在物理计算中**真正会用到的内容**。每一个概念都配有物理例子，每一段代码都解释清楚「为什么这么写」以及「如果不这么写会怎样」。
>
> **学完本教程后，你将能够**：
> - 用 Python 做数值计算、数据处理和科学绘图
> - 阅读和理解他人的仿真代码
> - 将物理公式转化为可运行的程序
> - 为后续学习 NumPy/SciPy/物理仿真打下坚实基础

---

## 目录

- [第 0 课：在开始之前——安装与环境](#第-0-课在开始之前安装与环境)
- [第 1 课：你的第一个 Python 程序](#第-1-课你的第一个-python-程序)
- [第 2 课：数字与计算——用 Python 当计算器](#第-2-课数字与计算用-python-当计算器)
- [第 3 课：变量——给数据取个名字](#第-3-课变量给数据取个名字)
- [第 4 课：字符串——处理文字信息](#第-4-课字符串处理文字信息)
- [第 5 课：列表——存放一组数据](#第-5-课列表存放一组数据)
- [第 6 课：判断——让程序做决策](#第-6-课判断让程序做决策)
- [第 7 课：循环——重复执行的力量](#第-7-课循环重复执行的力量)
- [第 8 课：函数——把代码打包成积木](#第-8-课函数把代码打包成积木)
- [第 9 课：元组与字典——更多组织数据的方式](#第-9-课元组与字典更多组织数据的方式)
- [第 10 课：文件读写——保存和加载数据](#第-10-课文件读写保存和加载数据)
- [第 11 课：引入外部工具——模块与库](#第-11-课引入外部工具模块与库)
- [第 12 课：NumPy 入门——数值计算的瑞士军刀](#第-12-课numpy-入门数值计算的瑞士军刀)
- [第 13 课：Matplotlib 入门——把你的数据画出来](#第-13-课matplotlib-入门把你的数据画出来)
- [第 14 课：面向对象编程——组织大型程序的方式](#第-14-课面向对象编程组织大型程序的方式)
- [第 15 课：错误处理——写出健壮的代码](#第-15-课错误处理写出健壮的代码)
- [第 16 课：综合实战——谐振子仿真](#第-16-课综合实战谐振子仿真)
- [附录：常见问题与排错指南](#附录常见问题与排错指南)

---

## 第 0 课：在开始之前——安装与环境

### 0.1 我们需要什么

写 Python 程序只需要两样东西：

1. **Python 解释器**：负责运行你写的代码。就像物理实验需要测量仪器，Python 解释器就是你运行代码的"仪器"。
2. **一个写代码的地方**：推荐 **VS Code**（Visual Studio Code），它是目前最流行的代码编辑器，免费且强大。

### 0.2 安装步骤

#### 第一步：安装 Python 解释器

1. 打开浏览器，访问 https://www.python.org/downloads/
2. 点击黄色的「Download Python」按钮（下载最新版本即可，比如 Python 3.12）
3. 运行下载的安装程序
4. ⚠️ **重要**：安装界面底部有一个复选框「Add Python to PATH」，**一定要勾选**！这让你能在任何位置运行 Python
5. 点击「Install Now」，等待安装完成

#### 第二步：验证安装

安装完成后，我们来确认 Python 已经正确安装。

打开**命令提示符**（按键盘上的 `Win + R`，输入 `cmd`，回车），在黑色窗口中输入：

```bash
python --version
```

如果看到类似 `Python 3.12.0` 的输出，说明安装成功！

再输入：

```bash
python
```

你会看到 `>>>` 符号——这就是 Python 的**交互模式**，你可以在这里直接输入 Python 代码并立即看到结果。试试输入：

```python
>>> 1 + 1
2
>>> print("Hello, 物理世界!")
Hello, 物理世界!
```

输入 `exit()` 或按 `Ctrl + Z` 然后回车可以退出交互模式。

#### 第三步：安装 VS Code

1. 访问 https://code.visualstudio.com/
2. 下载并安装 VS Code
3. 打开 VS Code
4. 点击左侧的「扩展」图标（四个方块），搜索「Python」
5. 安装微软官方出品的「Python」扩展

#### 第四步：创建你的第一个项目文件夹

1. 在桌面或你喜欢的任何位置，新建一个文件夹，命名为 `python_learning`
2. 打开 VS Code，点击「File → Open Folder」，选择 `python_learning` 文件夹
3. 在左侧文件列表中，右键 →「New File」，命名为 `lesson1.py`
4. 在文件中输入：

```python
print("我是物理系学生，我开始学 Python 了！")
```

5. 点击右上角的三角形「▶」按钮运行，或按 `Ctrl + F5`
6. 如果下方终端输出了这句话，恭喜你，环境配置完成！

> 💡 **实用技巧**：VS Code 中按 `Ctrl + S` 保存文件，按 `Ctrl + `` 打开/关闭终端，按 `Ctrl + /` 注释/取消注释当前行。

---

## 第 1 课：你的第一个 Python 程序

### 1.1 `print()` —— 让计算机说话

`print()` 是 Python 中最常用的函数。它的作用是把括号里的内容显示在屏幕上。

```python
print("你好，世界！")
print(42)
print(3.14159)
```

**运行结果：**
```
你好，世界！
42
3.14159
```

> 📘 **重要概念——函数**：`print` 是一个函数。函数就像一个机器：你从一端放入原料（括号里的内容），它执行某种操作（显示到屏幕），可能产出结果。Python 有大量内置函数，你以后还会自己定义函数。

### 1.2 什么是「语句」

Python 程序中，一行代码就是一个**语句**。计算机从上到下、一行一行地执行语句：

```python
print("第一行")
print("第二行")
print("第三行")
```

输出就是：

```
第一行
第二行
第三行
```

### 1.3 注释——给人类看的说明

在 Python 中，`#` 后面的内容会被**忽略**，不会执行。这叫**注释**。

```python
# 这是一条注释，Python 完全不理它
print("这行会被执行")  # 行尾也可以写注释
# print("这行不会被执行，因为它前面有 #")
```

注释的用途：
- 解释复杂的代码逻辑
- 标记待办事项
- 暂时禁用某行代码（调试时常用）

> 💡 **好习惯**：写代码时，多写注释。一周后你回来看自己的代码，会感谢当时的自己。

### 1.4 常见的「第一个错误」

初学者最常见的错误是**语法错误（SyntaxError）**——打字打错了。Python 会很友好地告诉你错在哪一行：

```python
print("Hello"    # 忘记写右括号
```

Python 会报错：

```
SyntaxError: '(' was never closed
```

**不要害怕错误！** 错误信息是 Python 在帮助你。仔细读错误信息，找到出错的行号，检查附近有没有拼写错误、少括号、少引号。

---

## 第 2 课：数字与计算——用 Python 当计算器

### 2.1 基本运算

Python 是一个超级强大的计算器。看看这些运算：

```python
print(3 + 5)      # 加法 → 8
print(10 - 3)     # 减法 → 7
print(4 * 6)      # 乘法 → 24
print(15 / 4)     # 除法 → 3.75（注意：结果是浮点数）
print(15 // 4)    # 整数除法（取商） → 3
print(15 % 4)     # 取余数（模运算） → 3
print(2 ** 10)    # 幂运算 → 1024
```

> 📘 **`**` 是 Python 中的幂运算符**。比如 `2**10` 就是 2¹⁰ = 1024。物理计算中经常用到，比如算平方 `x**2`、立方 `x**3`、开方 `x**0.5`。

### 2.2 运算优先级

和数学中一样，Python 遵循标准的运算优先级：

```python
print(2 + 3 * 4)    # 先乘后加 → 14
print((2 + 3) * 4)  # 括号改变顺序 → 20
print(10 / 2 ** 2)  # 先幂后除 → 10 / 4 = 2.5
```

> 💡 **不确定优先级时，加括号**。括号不仅保证正确，还让代码更易读。

### 2.3 整数 vs 浮点数

Python 中有两种主要的数字类型：

| 类型 | 写法示例 | 说明 |
|------|---------|------|
| `int`（整数） | `42`, `-7`, `0` | 没有小数部分 |
| `float`（浮点数） | `3.14`, `-0.001`, `1.0` | 有小数部分 |

```python
print(type(42))      # <class 'int'>
print(type(3.14))    # <class 'float'>
print(type(1.0))     # <class 'float'>，注意！有小数点就是 float
```

> ⚠️ **浮点数不是精确的**。在 Python 中试试 `0.1 + 0.2`，结果不是 `0.3`，而是 `0.30000000000000004`。这不是 Python 的 bug，而是所有计算机语言都有的浮点精度限制。处理方式见[第 2.7 节](#27-浮点数陷阱与应对)。

### 2.4 数学常数与常用函数

Python 自带一些数学功能：

```python
# 数学常数
import math       # 引入数学模块（第 11 课详细讲）

print(math.pi)    # π = 3.141592653589793
print(math.e)     # e = 2.718281828459045

# 常用数学函数
print(math.sqrt(16))    # 平方根 → 4.0
print(math.sin(math.pi / 2))  # sin(π/2) → 1.0
print(math.cos(0))      # cos(0) → 1.0
print(math.exp(1))      # e¹ → 2.718...
print(math.log(math.e)) # ln(e) → 1.0
print(math.log10(100))  # log₁₀(100) → 2.0
print(math.fabs(-5.5))  # 绝对值 → 5.5
```

> 📘 **`import math` 是什么意思？** 后面第 11 课会详细解释。简单说，Python 把一些不常用的功能放在"工具箱"里，你需要先 `import` 才能使用。就像做实验前需要从柜子里拿出仪器。

### 2.5 绝对值与取整

```python
print(abs(-5))          # 绝对值 → 5（内置函数，不需要 import）
print(round(3.14159, 2))  # 四舍五入到 2 位小数 → 3.14
print(round(3.14159))   # 四舍五入到整数 → 3
print(int(3.9))         # 直接截断小数 → 3
print(float(5))         # 整数转浮点数 → 5.0
```

### 2.6 给物理系学生的实用技巧

```python
import math

# 角度转弧度（物理中最常用的操作之一）
angle_degrees = 60
angle_radians = math.radians(angle_degrees)  # 60° → π/3
# 或者手动算：angle_radians = angle_degrees * math.pi / 180

# 弧度转角度
angle_degrees_back = math.degrees(angle_radians)  # π/3 → 60°

# 科学记数法
avogadro = 6.02214076e23     # 阿伏伽德罗常数
planck = 6.62607015e-34       # 普朗克常数
print(avogadro)  # 6.02214076e+23
```

### 2.7 浮点数陷阱与应对

前面提到 `0.1 + 0.2 ≠ 0.3`。这是因为计算机用二进制存储小数，有些十进制小数无法精确表示为二进制（就像 1/3 无法精确表示为十进制小数一样）。

```python
print(0.1 + 0.2)       # 0.30000000000000004
print(0.1 + 0.2 == 0.3)  # False！

# 正确的比较方式：检查差值是否足够小
tolerance = 1e-12       # 物理学中常用的容差值
print(abs((0.1 + 0.2) - 0.3) < tolerance)  # True
```

> 💡 **经验法则**：永远不要用 `==` 比较两个浮点数是否相等。用 `abs(a - b) < 1e-12` 来判断它们是否「足够接近」。

---

## 第 3 课：变量——给数据取个名字

### 3.1 什么是变量

**变量**就是一个带名字的「容器」，用来存放数据。你可以随时查看它里面的内容，也可以换新的内容放进去。

```python
x = 5           # 把 5 放进变量 x
print(x)        # 输出：5

x = 10          # 换成 10
print(x)        # 输出：10

x = x + 3       # 先算 x + 3 = 13，然后放回 x
print(x)        # 输出：13
```

> 📘 **`=` 不是「等于」，而是「赋值」**。`x = 5` 的意思是「把 5 赋予变量 x」，而不是数学中的等式。因此 `x = x + 1` 在编程中是合理的：先计算 x 当前值 + 1，然后把结果存回 x。

### 3.2 变量命名规则

Python 中变量名有这些规则：

```python
# ✅ 合法的变量名
time = 0.0
force_x = 10.5        # 下划线连接多个词（Python 推荐风格）
mass1 = 2.0
初始速度 = 100        # 可以用中文，但不推荐
_private = "hidden"   # 下划线开头也可以

# ❌ 不合法的变量名
# 1time = 0.0         # 不能以数字开头
# my-force = 10       # 不能包含连字符
# class = "physics"   # 不能使用 Python 关键字
```

> 💡 **命名建议**：
> - 变量名要有意义。`time` 比 `t` 好，`force_gravitational` 比 `fg` 好
> - 用下划线分隔：`kinetic_energy`、`wave_function`（这叫 snake_case，Python 标准）
> - 不要用拼音（除非你在写中文教学代码）
> - 物理量用小写（如 `mass`、`velocity`），常量用大写（如 `G = 6.67e-11`）

### 3.3 变量的类型是动态的

Python 的变量没有固定的类型——你可以随时放不同类型的值进去：

```python
x = 42          # x 现在是一个整数
print(type(x))  # <class 'int'>

x = "物理学"     # 现在 x 变成了字符串
print(type(x))  # <class 'str'>

x = [1, 2, 3]   # 现在又变成了列表
print(type(x))  # <class 'list'>
```

这是 Python 和 C/C++ 的一个重要区别。在 C 中，你需要事先声明变量的类型，而且不能再改变。Python 更灵活，但也意味着你需要自己注意变量的类型。

### 3.4 物理计算中的变量

让我们用变量来做一个物理计算——计算地球表面一个物体的重力：

```python
mass = 70.0                    # 质量（千克）
g = 9.8                        # 重力加速度（米/秒²）
weight = mass * g              # 重力 = 质量 × 重力加速度
print("物体质量:", mass, "kg")
print("重力加速度:", g, "m/s²")
print("所受重力:", weight, "N")
```

输出：
```
物体质量: 70.0 kg
重力加速度: 9.8 m/s²
所受重力: 686.0 N
```

### 3.5 多重赋值

Python 支持一行给多个变量赋值：

```python
x, y, z = 1, 2, 3
print(x, y, z)  # 1 2 3

# 物理场景：初始化位置和速度
position, velocity = 0.0, 5.0

# 交换两个变量的值（不用中间变量！）
a, b = 10, 20
a, b = b, a
print(a, b)  # 20 10
```

---

## 第 4 课：字符串——处理文字信息

### 4.1 创建字符串

字符串就是文本。在 Python 中，用单引号或双引号包裹文本：

```python
s1 = 'Hello'
s2 = "World"
s3 = "I'm a physics student"    # 用双引号可以包含单引号
s4 = 'He said "Eureka!"'         # 用单引号可以包含双引号
```

> 💡 单引号和双引号在 Python 中完全等价。选择的标准是：哪种让你的文本中少出现转义。

### 4.2 多行字符串

用三个引号 `"""` 或 `'''` 可以写多行文本：

```python
description = """
实验报告
=========
实验名称：单摆周期测量
实验日期：2026年3月
实验者：张三
"""
print(description)
```

### 4.3 字符串拼接与重复

```python
# 拼接（用 + 号）
greeting = "Hello" + " " + "World"
print(greeting)  # Hello World

# 重复（用 * 号）
separator = "-" * 40
print(separator)  # ----------------------------------------

# 拼接时自动类型转换……不行！
age = 20
# message = "我今年" + age + "岁"    # ❌ 错误！字符串不能和数字直接拼接
message = "我今年" + str(age) + "岁"  # ✅ 用 str() 把数字转成字符串
print(message)  # 我今年20岁
```

> ⚠️ **常见错误**：字符串和数字不能直接用 `+` 连接。需要用 `str()` 把数字转成字符串。

### 4.4 f-string：最高效的字符串格式化

Python 3.6 开始，`f-string` 是最推荐的字符串格式化方式，简单直观：

```python
mass = 70.0
velocity = 5.0
kinetic_energy = 0.5 * mass * velocity**2

# f-string：在引号前加 f，花括号里写变量
print(f"质量 {mass} kg 以 {velocity} m/s 运动的动能是 {kinetic_energy} J")

# 控制小数位数
print(f"动能 = {kinetic_energy:.2f} J")  # 保留两位小数：动能 = 875.00 J

# 科学记数法
plasma_frequency = 1.78e11
print(f"等离子体频率 = {plasma_frequency:.2e} Hz")  # 1.78e+11 Hz

# 对齐和填充
for n in range(1, 6):
    print(f"|{n:3d}|{n**2:5d}|{n**3:7d}|")
# 输出：
# |  1|    1|      1|
# |  2|    4|      8|
# |  3|    9|     27|
# |  4|   16|     64|
# |  5|   25|    125|
```

> 💡 **f-string 是最推荐的字符串格式化方式**，比旧式的 `%` 和 `.format()` 都更简洁高效。

### 4.5 常用字符串方法

```python
text = "  Physics Simulation  "

print(text.lower())        # 全小写 → "  physics simulation  "
print(text.upper())        # 全大写 → "  PHYSICS SIMULATION  "
print(text.strip())        # 去除首尾空格 → "Physics Simulation"
print(text.replace("Physics", "量子力学"))  # 替换 → "  量子力学 Simulation  "
print(text.startswith("  Ph"))    # 是否以此开头 → True
print("tion" in text)             # 是否包含 → True
```

---

## 第 5 课：列表——存放一组数据

### 5.1 为什么需要列表

在物理仿真中，你经常需要处理一组数据，而不是单个数字。比如：
- 100 个时间点的位置数据
- 50 个网格点的温度值
- N 个粒子的坐标

**列表**就是用来存放一组有序数据的容器。

### 5.2 创建和访问列表

```python
# 创建列表（用方括号）
temperatures = [25.3, 26.1, 24.8, 23.5, 27.2]
materials = ["铜", "铝", "铁", "玻璃"]
mixed = [1, "hello", 3.14, True]   # 列表可以混装不同类型（但不推荐）

# 访问元素（索引从 0 开始！）
print(temperatures[0])    # 第 1 个元素 → 25.3
print(temperatures[1])    # 第 2 个元素 → 26.1
print(temperatures[-1])   # 最后一个元素 → 27.2
print(temperatures[-2])   # 倒数第二个 → 23.5
```

> ⚠️ **Python 的索引从 0 开始，不是 1！** 这意味着第 1 个元素的索引是 0，第 5 个元素的索引是 4。这是所有主流编程语言的惯例。

### 5.3 切片——取列表的一部分

切片是 Python 中极其强大的功能：

```python
data = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

print(data[2:5])    # 索引 2 到 4 → [2, 3, 4]
print(data[:4])     # 开头到索引 3 → [0, 1, 2, 3]
print(data[6:])     # 索引 6 到结尾 → [6, 7, 8, 9]
print(data[::2])    # 每隔一个取 → [0, 2, 4, 6, 8]
print(data[::-1])   # 倒序 → [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
```

**切片语法**：`list[开始:结束:步长]`
- `开始`：包含，默认 0
- `结束`：**不包含**，默认列表末尾
- `步长`：默认 1

> ⚠️ 切片的结束索引是**不包含**的。`data[2:5]` 取索引 2、3、4，不取 5。这个设计一开始会觉得奇怪，但它有深刻的数学原因（让 `data[:i] + data[i:] == data` 恒成立）。

### 5.4 修改列表

```python
materials = ["铜", "铝", "铁"]

materials[1] = "银"         # 修改第 2 个元素
print(materials)            # ['铜', '银', '铁']

materials.append("金")       # 末尾添加一个元素
print(materials)            # ['铜', '银', '铁', '金']

materials.insert(1, "锌")    # 在索引 1 处插入
print(materials)            # ['铜', '锌', '银', '铁', '金']

materials.remove("铁")       # 删除值为 "铁" 的元素
print(materials)            # ['铜', '锌', '银', '金']

last = materials.pop()      # 移除并返回最后一个元素
print(last)                 # 金
print(materials)            # ['铜', '锌', '银']
```

### 5.5 列表的常用操作

```python
data = [3, 1, 4, 1, 5, 9, 2, 6]

print(len(data))           # 列表长度 → 8
print(sum(data))           # 求和 → 31
print(max(data))           # 最大值 → 9
print(min(data))           # 最小值 → 1
print(data.count(1))       # 1 出现的次数 → 2

data.sort()                # 排序（原地修改）
print(data)                # [1, 1, 2, 3, 4, 5, 6, 9]

data.reverse()             # 反转（原地修改）
print(data)                # [9, 6, 5, 4, 3, 2, 1, 1]
```

### 5.6 列表推导式 —— Python 的魔法语法

列表推导式让你用一行代码生成列表，在物理仿真中极其常用：

```python
# 基本形式：[表达式 for 变量 in 可迭代对象]

# 生成 0 到 9 的平方
squares = [i**2 for i in range(10)]
print(squares)  # [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

# 物理场景：生成 0 到 2π 之间 100 个时间点
import math
time_points = [2 * math.pi * i / 99 for i in range(100)]

# 带条件的列表推导式：[表达式 for 变量 in 可迭代对象 if 条件]
# 取 0 到 19 中的偶数
evens = [i for i in range(20) if i % 2 == 0]
print(evens)  # [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]

# 嵌套循环的列表推导式
# 生成所有 (x, y) 坐标组合，0 ≤ x < 3, 0 ≤ y < 3
grid_points = [(x, y) for x in range(3) for y in range(3)]
print(grid_points)  # [(0,0), (0,1), (0,2), (1,0), ...]
```

> 💡 列表推导式本质上是用简洁语法替代了 for 循环 + append。物理仿真中生成初始坐标、时间网格时非常方便。

### 5.7 `range()` —— 生成整数序列

`range()` 是循环中最重要的函数之一：

```python
print(list(range(5)))        # [0, 1, 2, 3, 4]    → range(stop)
print(list(range(2, 7)))     # [2, 3, 4, 5, 6]    → range(start, stop)
print(list(range(1, 10, 2))) # [1, 3, 5, 7, 9]    → range(start, stop, step)
print(list(range(10, 0, -1)))  # [10, 9, 8, ..., 1] → 可以倒序！
```

> ⚠️ `range()` 同样**不包含**结束值。`range(1, 10)` 生成 1 到 9，不包括 10。

---

## 第 6 课：判断——让程序做决策

### 6.1 比较运算符

```python
x = 10
y = 20

print(x == y)    # 等于 → False
print(x != y)    # 不等于 → True
print(x < y)     # 小于 → True
print(x > y)     # 大于 → False
print(x <= 10)   # 小于等于 → True
print(x >= 15)   # 大于等于 → False
```

> ⚠️ **`==` 是比较，`=` 是赋值**。这是初学者最常见的错误！`x = 10` 是把 10 赋给 x，`x == 10` 是判断 x 是否等于 10。

### 6.2 `if` 语句

```python
temperature = 150  # 摄氏度

if temperature > 100:
    print("水沸腾了！")
    print("准备计时。")

print("实验继续。")  # 这行无论条件是否成立都会执行
```

> 📘 **缩进是关键**：Python 用缩进（空格）来表示代码的「归属」。`if` 后面缩进的代码块只在条件为 `True` 时执行。标准缩进是 **4 个空格**（按 Tab 键，VS Code 会自动换算成 4 个空格）。

### 6.3 `if-elif-else` —— 多路分支

```python
temperature = 25

if temperature > 100:
    state = "气态"
elif temperature > 0:
    state = "液态"
else:
    state = "固态"

print(f"在当前温度 {temperature}°C，水是{state}")
```

执行逻辑：
1. 先判断 `temperature > 100`：25 > 100 → `False`，跳过
2. 判断 `temperature > 0`：25 > 0 → `True`，执行 `state = "液态"`
3. `else` 被跳过（因为前面的 `elif` 已经命中）

> 💡 `elif` 可以有任意多个，`else` 是可选的。`elif` 是 "else if" 的缩写。

### 6.4 逻辑运算符：组合多个条件

```python
# and: 两个条件都成立
# or:  至少一个条件成立
# not: 反转条件

x = 15

if x > 10 and x < 20:
    print("x 在 10 到 20 之间")

if x < 0 or x > 100:
    print("x 超出正常范围")

if not (x == 0):
    print("x 不是零")
```

**短路求值**：Python 在确保结果后就不再计算后面的条件了。
```python
# 如果 x = 0，第二个条件不会被检查（因为 False and anything = False）
# 这就避免了除以零的错误
if x != 0 and 10 / x > 2:
    print("条件成立")
```

### 6.5 物理例子：判断运动阶段

```python
velocity = -3.0  # m/s
position = 2.0   # m

# 简谐运动的判断
if abs(position) < 0.01:
    direction = "在平衡位置"
elif position > 0 and velocity < 0:
    direction = "正向负方向运动（往回走）"
elif position > 0 and velocity > 0:
    direction = "正向往正方向运动（远离平衡位置）"
elif position < 0 and velocity > 0:
    direction = "负向往正方向运动（往回走）"
else:
    direction = "负向往负方向运动（远离平衡位置）"

print(direction)
```

---

## 第 7 课：循环——重复执行的力量

### 7.1 为什么需要循环

编程最大的优势就是可以**自动化重复任务**。比如：
- 模拟 1000 个时间步的运动
- 对 10000 个粒子逐一计算受力
- 扫描 100 个不同参数下的结果

这些如果用人工做是不可能的，但用循环只需要几行代码。

### 7.2 `for` 循环 —— 遍历一个序列

```python
# 基本形式
for i in range(5):
    print(f"第 {i+1} 次迭代")
# 第 1 次迭代
# 第 2 次迭代
# 第 3 次迭代
# 第 4 次迭代
# 第 5 次迭代

# 遍历列表
materials = ["铜", "铝", "铁", "玻璃"]
for material in materials:
    print(f"当前材料：{material}")

# 同时获取索引和值（enumerate）
for i, material in enumerate(materials):
    print(f"第 {i+1} 种材料是 {material}")
```

### 7.3 `while` 循环 —— 满足条件就一直做

```python
# 基本形式
countdown = 5
while countdown > 0:
    print(f"倒计时：{countdown}")
    countdown -= 1  # 等价于 countdown = countdown - 1
print("发射！")
```

> ⚠️ **小心无限循环！** 如果条件永远不会变成 `False`，程序就会一直运行下去：
> ```python
> # ❌ 无限循环！x 永远等于 10
> x = 10
> while x > 0:
>     print(x)
>     # 忘了写 x -= 1 ！
> ```
> 如果遇到无限循环，在 VS Code 终端按 `Ctrl + C` 强制停止。

#### `for` vs `while` 的选择

| 场景 | 用什么 |
|------|--------|
| 已知具体次数（如执行 100 步） | `for i in range(100)` |
| 条件未知，需要重复到满足某条件（如误差 < 容差） | `while error > tolerance` |
| 遍历列表/序列的每个元素 | `for item in list` |

### 7.4 `break` 和 `continue`

```python
# break: 提前结束循环
for i in range(100):
    if i > 5:
        break             # i=6 时跳出循环
    print(i)
# 输出：0 1 2 3 4 5

# continue: 跳过本次循环的剩余部分，继续下一次
for i in range(8):
    if i % 2 == 0:        # 偶数则跳过
        continue
    print(i, end=" ")     # 只打印奇数
# 输出：1 3 5 7
```

### 7.5 循环的嵌套

```python
# 打印乘法表
for i in range(1, 10):
    for j in range(1, i + 1):
        print(f"{j}×{i}={i*j:2d}", end="  ")
    print()  # 换行
```

### 7.6 循环中的物理应用

#### 例1：时间推进仿真

```python
# 自由落体：y = y₀ + v₀t - ½gt²
y0 = 100.0    # 初始高度（米）
v0 = 0.0      # 初速度（米/秒）
g = 9.8       # 重力加速度

y = y0
v = v0
dt = 0.01     # 时间步长（秒）

for step in range(1000):
    # 更新速度：v = v₀ - g·dt
    v = v - g * dt
    # 更新位置：y = y₀ + v·dt
    y = y + v * dt
    
    # 碰到地面就停止
    if y <= 0:
        y = 0
        print(f"物体在 t = {step * dt:.2f} 秒时落地")
        break
    
    # 每 100 步汇报一次
    if step % 100 == 0:
        print(f"t = {step * dt:.1f}s, y = {y:.2f}m, v = {v:.2f}m/s")
```

#### 例2：级数求和 — 计算 e 的近似值

```python
# e = 1 + 1/1! + 1/2! + 1/3! + ...
import math

# 用循环求和
n_terms = 20
e_approx = 1.0
factorial = 1.0

for n in range(1, n_terms + 1):
    factorial *= n          # 累积计算 n!
    e_approx += 1.0 / factorial

print(f"e 的近似值 ({n_terms} 项)：{e_approx:.10f}")
print(f"真实的 e：         {math.e:.10f}")
print(f"误差：{abs(e_approx - math.e):.2e}")
```

---

## 第 8 课：函数——把代码打包成积木

### 8.1 什么是函数，为什么要用

你已经在用函数了——`print()`、`len()`、`range()` 都是函数。但你也可以**自己定义函数**，把一段代码打包起来重复使用。

不用函数的代码：
```python
# 计算铁球的重力
mass1 = 10.0
weight1 = mass1 * 9.8
print(f"质量 {mass1}kg 的重力是 {weight1}N")

# 计算木球的重力（又写一遍几乎一样的代码）
mass2 = 3.0
weight2 = mass2 * 9.8
print(f"质量 {mass2}kg 的重力是 {weight2}N")

# 计算水桶的重力（又写一遍……）
mass3 = 25.0
weight3 = mass3 * 9.8
print(f"质量 {mass3}kg 的重力是 {weight3}N")
```

用函数：
```python
def calc_weight(mass):
    """计算质量为 mass (kg) 的物体在地球表面的重力 (N)"""
    g = 9.8
    weight = mass * g
    return weight

# 现在只需要一行！
print(f"铁球重力：{calc_weight(10.0)}N")
print(f"木球重力：{calc_weight(3.0)}N")
print(f"水桶重力：{calc_weight(25.0)}N")
```

### 8.2 定义函数的语法

```python
def 函数名(参数1, 参数2, ...):
    """文档字符串：说明这个函数做什么"""
    # 函数体
    return 结果   # return 是可选的
```

各部分解释：
- `def`：关键字，表示「定义函数」
- `函数名`：你给函数取的名字，规则和变量名一样
- `参数`：传入的输入值（可以没有、可以多个）
- `"""文档字符串"""`：可选的说明，但强烈推荐写
- `return`：函数的输出值。如果没有 `return`，函数返回 `None`

### 8.3 参数与返回值

```python
# 没有参数的函数
def say_hello():
    print("Hello, Physics!")

say_hello()  # 调用

# 一个参数，一个返回值
def square(x):
    return x ** 2

print(square(5))  # 25

# 多个参数
def kinetic_energy(mass, velocity):
    return 0.5 * mass * velocity ** 2

print(kinetic_energy(70, 5))  # 875.0

# 返回多个值（Python 特色！）
def cartesian_to_polar(x, y):
    """直角坐标转极坐标"""
    import math
    r = math.sqrt(x**2 + y**2)
    theta = math.atan2(y, x)
    return r, theta    # 返回元组

r, angle = cartesian_to_polar(3, 4)
print(f"r = {r}, θ = {angle:.4f} rad")  # r = 5.0, θ = 0.9273 rad
```

### 8.4 默认参数

```python
# 有些参数可以有默认值，调用时可以不传
def gravity_force(mass, g=9.8):
    """计算重力，默认 g=9.8 m/s²（地球表面）"""
    return mass * g

print(gravity_force(10))       # 98.0（使用默认 g=9.8）
print(gravity_force(10, 1.62))  # 16.2（月球表面 g=1.62）
```

> ⚠️ **默认参数必须放在非默认参数的后面**。`def f(a=1, b):` 是错误的，应该是 `def f(b, a=1):`。

### 8.5 函数的「作用域」

函数内部的变量是**局部的**——外面看不到：

```python
def my_function():
    x = 100       # 这个 x 只在函数内部存在
    print(f"内部 x = {x}")

my_function()
# print(x)       # ❌ NameError! 函数外的 x 不存在

# 全局变量
GLOBAL_G = 6.67e-11   # 常量用大写命名表示「这是全局的」

def gravitational_force(m1, m2, r):
    return GLOBAL_G * m1 * m2 / r**2   # 可以读取全局变量
```

> 💡 **函数应该尽量减少对全局变量的依赖**，通过参数传入所需的值。这样函数更容易测试和复用。

### 8.6 物理函数示例

```python
import math

def coulomb_force(q1, q2, r):
    """
    计算两个点电荷之间的 Coulomb 力大小
    q1, q2: 电荷量 (库仑)
    r: 距离 (米)
    返回: 力的大小 (牛顿)，正值为排斥，负值为吸引
    """
    k = 8.987551787e9  # Coulomb 常数
    return k * q1 * q2 / r**2

def photon_energy(wavelength_nm):
    """
    计算给定波长的光子能量
    wavelength_nm: 波长 (纳米)
    返回: 能量 (焦耳)
    """
    h = 6.62607015e-34   # 普朗克常数 J·s
    c = 2.99792458e8     # 光速 m/s
    wavelength_m = wavelength_nm * 1e-9
    return h * c / wavelength_m

# 使用
print(f"两个 1μC 电荷在 1m 处的力: {coulomb_force(1e-6, 1e-6, 1):.2f} N")
print(f"500nm 光子的能量: {photon_energy(500):.2e} J")

# 转换单位：焦耳 → 电子伏特
e_ev = photon_energy(500) / 1.602e-19
print(f"           = {e_ev:.2f} eV")
```

---

## 第 9 课：元组与字典——更多组织数据的方式

### 9.1 元组（tuple）—— 不可修改的列表

元组和列表很像，但**创建后不能修改**。用圆括号：

```python
# 创建元组
point = (3.0, 4.0, 0.0)           # 三维坐标
constants = (6.67e-11, 9.8, 1.6e-19)  # 物理常数集合

# 访问（和列表一样）
print(point[0])    # 3.0
print(point[1])    # 4.0

# 但不能修改
# point[0] = 5.0   # ❌ TypeError: 'tuple' object does not support item assignment

# 元组的用途：
# 1. 表示不会改变的数据（如坐标、物理常数）
# 2. 函数返回多个值（实际上返回的是元组）
# 3. 作为字典的键（列表不行，元组可以）
```

### 9.2 元组解包

```python
# 把元组的各个元素一次性赋给多个变量
coordinates = (5.0, 10.0, -3.0)
x, y, z = coordinates
print(f"x={x}, y={y}, z={z}")

# 函数返回多个值就是返回元组
def particle_info():
    return ("电子", 9.11e-31, -1.60e-19)  # 名字、质量、电荷

name, mass, charge = particle_info()
print(f"{name}: m={mass:.2e} kg, q={charge:.2e} C")
```

### 9.3 字典（dict）—— 用「名字」而不是「编号」来访问数据

列表/元组通过索引（0, 1, 2...）访问，而字典通过**键**来访问，就像查字典一样。

```python
# 创建字典（用花括号）
particle = {
    "name": "质子",
    "mass": 1.67e-27,        # kg
    "charge": 1.60e-19,       # C
    "spin": 1/2,
    "type": "费米子"
}

# 通过「键」来访问「值」
print(particle["name"])      # 质子
print(particle["mass"])      # 1.67e-27
print(f"{particle['name']}的质量是 {particle['mass']:.2e} kg")

# 修改和添加
particle["mass"] = 1.6726e-27  # 更精确的值
particle["discovered"] = 1919  # 新增键值对

# 检查键是否存在
if "antiparticle" in particle:
    print(particle["antiparticle"])
else:
    print("字典中没有 'antiparticle' 这个键")
```

### 9.4 字典的遍历

```python
experiment = {
    "name": "Franck-Hertz 实验",
    "year": 1914,
    "phenomenon": "验证原子能级量子化"
}

# 遍历键
for key in experiment:
    print(f"{key}: {experiment[key]}")

# 遍历键和值（更推荐）
for key, value in experiment.items():
    print(f"{key:12s} → {value}")
# name         → Franck-Hertz 实验
# year         → 1914
# phenomenon   → 验证原子能级量子化
```

### 9.5 三种数据结构的对比

| 特性 | 列表 `list` | 元组 `tuple` | 字典 `dict` |
|------|------------|-------------|------------|
| 创建符号 | `[ ]` | `( )` | `{ }` |
| 可修改 | ✅ | ❌ | ✅ |
| 访问方式 | 索引 `[i]` | 索引 `[i]` | 键 `["key"]` |
| 用途 | 有序、同类的数据集合 | 坐标、固定组合 | 属性/参数存储 |
| 能否做 dict 的键 | ❌ | ✅ | ❌ |
| 物理场景 | 时间序列数据 | 三维坐标 | 粒子属性、实验参数 |

---

## 第 10 课：文件读写——保存和加载数据

### 10.1 为什么需要文件操作

仿真结果不能只存在内存里——程序一关就没了。你需要：
- 把计算数据保存到文件中
- 从文件中读取实验数据
- 输出分析报告

### 10.2 写入文件

```python
# 打开文件（'w' 表示写入模式，会覆盖已有内容）
with open("results.txt", "w", encoding="utf-8") as f:
    f.write("单摆实验数据\n")
    f.write("=" * 40 + "\n")
    f.write("长度(m) 周期(s)\n")
    
    # 写入实验数据
    for length in [0.5, 1.0, 1.5, 2.0]:
        period = 2 * 3.14159 * (length / 9.8) ** 0.5
        f.write(f"{length:.1f}     {period:.4f}\n")

print("数据已保存到 results.txt")

# with 语句会自动关闭文件，不需要手动 close
```

> 📘 **`with` 语句**是 Python 的上下文管理器，确保文件使用完毕后正确关闭。养成用 `with` 的好习惯，不要用 `f = open()` + `f.close()` 的老式写法。

### 10.3 读取文件

```python
# 读取整个文件内容
with open("results.txt", "r", encoding="utf-8") as f:
    content = f.read()
print(content)

# 逐行读取
with open("results.txt", "r", encoding="utf-8") as f:
    for line in f:
        print(line.strip())  # strip() 去掉行尾的换行符

# 读成列表，每个元素是一行
with open("results.txt", "r", encoding="utf-8") as f:
    lines = f.readlines()
print(f"文件共 {len(lines)} 行")
```

### 10.4 文件模式

| 模式 | 说明 |
|------|------|
| `'r'` | 读取（默认）——文件必须存在 |
| `'w'` | 写入——覆盖已有内容，文件不存在则创建 |
| `'a'` | 追加——在末尾追加内容 |
| `'r+'` | 读写 |

### 10.5 处理 CSV 格式的数据（常见实验数据格式）

CSV（逗号分隔值）是存储数据的标准格式。你可以用 Python 的 `csv` 模块：

```python
import csv

# 写入 CSV
data = [
    ["时间(s)", "位置(m)", "速度(m/s)"],
    [0.0, 1.0, 0.0],
    [0.1, 0.995, -0.099],
    [0.2, 0.980, -0.198],
]

with open("simulation_data.csv", "w", newline="", encoding="utf-8") as f:
    writer = csv.writer(f)
    writer.writerows(data)

# 读取 CSV
with open("simulation_data.csv", "r", encoding="utf-8") as f:
    reader = csv.reader(f)
    header = next(reader)  # 读取表头
    print(f"列名: {header}")
    
    times, positions, velocities = [], [], []
    for row in reader:
        times.append(float(row[0]))
        positions.append(float(row[1]))
        velocities.append(float(row[2]))

print(f"读取了 {len(times)} 行数据")
print(f"时间范围: {times[0]}s ~ {times[-1]}s")
```

---

## 第 11 课：引入外部工具——模块与库

### 11.1 什么是模块

Python 本身很精简，大量功能以**模块**（module）的形式存在。你需要的时候把它们"导入"进来。

```python
import math          # 导入数学模块

print(math.pi)       # 使用模块中的内容：模块.功能名
print(math.sin(0))
print(math.sqrt(16))
```

### 11.2 几种导入方式

```python
# 方式1：导入整个模块（最清晰，推荐）
import math
print(math.cos(math.pi))

# 方式2：导入模块并取别名（常用约定）
import numpy as np          # NumPy 几乎总是被 import 为 np
import matplotlib.pyplot as plt  # pyplot 几乎总是被 import 为 plt

# 方式3：从模块中导入特定功能
from math import sin, cos, pi
print(sin(pi/2))    # 不需要 math. 前缀

# 方式4：导入模块中的所有内容（不推荐！可能覆盖同名函数）
# from math import *    # ❌ 避免使用
```

> 💡 **推荐使用方式 1 或 2**。`模块名.函数名()` 的形式让代码更清晰，一看就知道函数来自哪里。物理仿真中你会有很多函数，清楚地知道哪个来自哪个库非常重要。

### 11.3 标准库——Python 自带的宝藏

Python 自带了很多有用的库，不需要安装就能用：

```python
import math          # 数学函数
import random        # 随机数
import csv           # CSV 文件处理
import json          # JSON 数据处理
import datetime      # 日期和时间
import os            # 操作系统接口（路径操作）
import glob          # 文件名模式匹配
import itertools     # 迭代工具（排列组合等）
import collections   # 高级数据结构
```

### 11.4 第三方库——需要安装的扩展

标准库之外的功能需要安装。安装方式就是 `pip install`：

```bash
pip install numpy scipy matplotlib     # 科学计算三剑客
pip install numba                      # 即时编译加速
pip install sympy                      # 符号计算
```

> 💡 安装时如果提示权限不够，加 `--user`：`pip install --user numpy`

---

## 第 12 课：NumPy 入门——数值计算的瑞士军刀

### 12.1 为什么需要 NumPy

Python 的列表处理大规模数据时太慢了。比如你要对 100 万个数字求 sin 值：

```python
# Python 列表方式（极慢）
import math
result = []
for i in range(1000000):
    result.append(math.sin(i * 0.001))

# NumPy 方式（极快 —— 快 50-100 倍！）
import numpy as np
x = np.arange(0, 1000, 0.001)
result = np.sin(x)
```

NumPy 的核心是 `ndarray`（N 维数组）——一种专门为大规模数值计算设计的数据结构。

### 12.2 创建 NumPy 数组

```python
import numpy as np

# 从列表创建
a = np.array([1, 2, 3, 4, 5])
print(a)             # [1 2 3 4 5]
print(type(a))       # <class 'numpy.ndarray'>

# 创建特殊数组
print(np.zeros(5))           # [0. 0. 0. 0. 0.]  —— 全是零
print(np.ones(5))            # [1. 1. 1. 1. 1.]  —— 全是一
print(np.zeros((3, 4)))      # 3×4 的零矩阵
print(np.eye(3))             # 3×3 单位矩阵

# 线性空间（最重要！）
print(np.linspace(0, 10, 5)) # [0. 2.5 5. 7.5 10.]  —— 等距 5 个点
print(np.arange(0, 10, 2))   # [0 2 4 6 8]  —— 指定步长
```

> 💡 **`np.linspace(开始, 结束, 点数)`** 是物理仿真中最常用的函数之一，用于生成网格点或时间序列。

### 12.3 数组的基本属性

```python
a = np.zeros((10, 3))   # 10 行 3 列的零数组

print(a.shape)    # (10, 3)  —— 形状（10 行，3 列）
print(a.ndim)     # 2        —— 维度
print(a.size)     # 30       —— 元素总数
print(a.dtype)    # float64  —— 数据类型（双精度浮点）
```

### 12.4 向量化运算——告别 for 循环

这是 NumPy 最强大的地方：**运算自动应用到数组的每个元素**。

```python
a = np.array([1.0, 2.0, 3.0, 4.0, 5.0])

# # Python 列表的写法（需要循环）
# result = []
# for i in range(len(a)):
#     result.append(a[i] * 2 + 1)

# NumPy 向量化写法（一行！）
result = a * 2 + 1
print(result)   # [ 3.  5.  7.  9. 11.]

# 数学函数也向量化了
print(np.sin(a))      # [sin(1), sin(2), sin(3), sin(4), sin(5)]
print(np.sqrt(a))     # [√1, √2, √3, √4, √5]
print(np.exp(a))      # [e¹, e², e³, e⁴, e⁵]
print(a ** 2)         # [1, 4, 9, 16, 25]
```

> 💡 **永远不要对 NumPy 数组写 Python for 循环。** 这是仿真性能的第一守则。

### 12.5 数组切片（和列表类似但更强大）

```python
arr = np.array([[1, 2, 3, 4],
                [5, 6, 7, 8],
                [9, 10, 11, 12]])

print(arr[0, :])      # 第 1 行：[1, 2, 3, 4]
print(arr[:, 1])      # 第 2 列：[2, 6, 10]
print(arr[0:2, 1:3])  # 子矩阵：[[2, 3], [6, 7]]
print(arr[-1, -1])    # 最后一个元素：12
```

### 12.6 聚合运算

```python
data = np.array([[1, 2, 3],
                 [4, 5, 6]])

print(data.sum())         # 21（全部求和）
print(data.sum(axis=0))   # [5, 7, 9]（沿第 0 轴 = 纵向 = 按列求和）
print(data.sum(axis=1))   # [6, 15]（沿第 1 轴 = 横向 = 按行求和）
print(data.mean())        # 3.5（平均值）
print(data.std())         # 标准差
print(data.min())         # 最小值
print(data.max())         # 最大值
print(data.argmax())      # 最大值的索引
```

> 📘 **`axis` 参数的理解**：`axis=0` 表示沿第 0 维（行方向）操作，结果是「压缩」了行。可以记为 `axis=0` → 沿行操作 → 消除行 → 结果比原来少一维。

### 12.7 广播（Broadcasting）—— 不同形状的数组也能运算

这是 NumPy 的高级特性，但理解它能让你的代码极其简洁：

```python
# 形状 (4,) 的数组 和 形状 (3,4) 的数组相加
row = np.array([10, 20, 30, 40])   # 形状 (4,)
matrix = np.ones((3, 4))           # 形状 (3, 4)

result = matrix + row   # row 被自动"广播"成 (3,4)
print(result)
# [[11. 21. 31. 41.]
#  [11. 21. 31. 41.]
#  [11. 21. 31. 41.]]
```

> 💡 广播规则：从最后一个维度开始比较，两个维度的尺寸必须「相等或其中一个为 1」。详细的广播理解不是初学的重点，先记住「向量加矩阵会自动扩展」就够用了。

### 12.8 物理例子：用 NumPy 做简谐运动

```python
import numpy as np

# 参数
omega = 2 * np.pi       # 角频率
A = 1.0                 # 振幅
phi = 0.0               # 初相位

# 生成时间序列（NumPy 一行搞定）
t = np.linspace(0, 2, 100)  # 0 到 2 秒，100 个点

# 计算位移、速度、加速度（全部向量化）
x = A * np.cos(omega * t + phi)          # 位移
v = -A * omega * np.sin(omega * t + phi)  # 速度
a = -A * omega**2 * np.cos(omega * t + phi)  # 加速度

# 验证能量守恒
kinetic = 0.5 * v**2
potential = 0.5 * omega**2 * x**2
total_energy = kinetic + potential

print(f"总能量均值: {total_energy.mean():.6f}")
print(f"总能量方差: {total_energy.std():.10f}")
print("（方差几乎为 0 → 能量守恒）")
```

---

## 第 13 课：Matplotlib 入门——把你的数据画出来

### 13.1 导入 Matplotlib

```python
import matplotlib.pyplot as plt
```

`plt` 是几乎全世界统一的别名，你这样写别人不会搞混。

### 13.2 你的第一张图

```python
import matplotlib.pyplot as plt
import numpy as np

# 生成数据
x = np.linspace(0, 2 * np.pi, 100)
y = np.sin(x)

# 画图
plt.plot(x, y)
plt.show()
```

运行后你会看到一张正弦波的图。

### 13.3 添加标签和标题

```python
x = np.linspace(0, 10, 200)
y1 = np.sin(x)
y2 = np.cos(x)

plt.figure(figsize=(8, 5))              # 设置图像大小（宽 8 英寸，高 5 英寸）

plt.plot(x, y1, 'b-', label='sin(x)', linewidth=1.5)   # 蓝实线
plt.plot(x, y2, 'r--', label='cos(x)', linewidth=1.5)  # 红虚线

plt.xlabel('x')                         # x 轴标签
plt.ylabel('y')                         # y 轴标签
plt.title('正弦和余弦函数')              # 标题
plt.legend()                            # 显示图例
plt.grid(alpha=0.3)                     # 网格线（alpha 控制透明度）

plt.savefig('sine_cosine.png', dpi=150, bbox_inches='tight')  # 保存图片
plt.show()
```

> 📘 **`plt.plot()` 的第三个参数是格式字符串**：
> - `'b-'` = 蓝色 (blue) 实线
> - `'r--'` = 红色 (red) 虚线
> - `'g.'` = 绿色点
> - `'k-.'` = 黑色点划线
> - 更多：`color=''`, `linestyle=''`, `marker=''` 分开写也可以

### 13.4 多子图

```python
# 创建 2 行 2 列的子图
fig, axes = plt.subplots(2, 2, figsize=(10, 8))

x = np.linspace(0, 2*np.pi, 200)

# 左上：sin
axes[0, 0].plot(x, np.sin(x), 'b-')
axes[0, 0].set_title('sin(x)')
axes[0, 0].grid(alpha=0.3)

# 右上：cos
axes[0, 1].plot(x, np.cos(x), 'r-')
axes[0, 1].set_title('cos(x)')
axes[0, 1].grid(alpha=0.3)

# 左下：sin²
axes[1, 0].plot(x, np.sin(x)**2, 'g-')
axes[1, 0].set_title('sin²(x)')
axes[1, 0].grid(alpha=0.3)

# 右下：sin(x)cos(x)
axes[1, 1].plot(x, np.sin(x)*np.cos(x), 'm-')
axes[1, 1].set_title('sin(x)cos(x)')
axes[1, 1].grid(alpha=0.3)

plt.tight_layout()    # 自动调整子图间距
plt.show()
```

### 13.5 散点图（实验数据点）

```python
# 模拟实验数据：理论值 + 噪声
x_data = np.linspace(0, 10, 30)
y_theory = 2 * x_data + 1                       # 理论：线性关系 y = 2x + 1
y_measured = y_theory + np.random.normal(0, 1.5, 30)  # 加上高斯噪声

plt.figure(figsize=(8, 5))
plt.scatter(x_data, y_measured, color='red', s=30, alpha=0.7, label='测量值')
plt.plot(x_data, y_theory, 'b--', linewidth=1.5, label='理论值')
plt.xlabel('x'); plt.ylabel('y')
plt.title('实验数据 vs 理论曲线')
plt.legend(); plt.grid(alpha=0.3)
plt.show()
```

### 13.6 物理图表：完整的谐振子分析

```python
import numpy as np
import matplotlib.pyplot as plt

# 参数
omega0 = 2.0
damping = 0.3
t = np.linspace(0, 15, 500)

# 阻尼谐振子解析解
omega1 = np.sqrt(omega0**2 - damping**2)
x = np.exp(-damping * t) * np.cos(omega1 * t)
v = -np.exp(-damping * t) * (damping * np.cos(omega1 * t) + omega1 * np.sin(omega1 * t))
energy = 0.5 * v**2 + 0.5 * omega0**2 * x**2

# 创建图表
fig, axes = plt.subplots(2, 2, figsize=(12, 9))

# 1. 位移时间序列
axes[0, 0].plot(t, x, 'b-', lw=1)
axes[0, 0].axhline(0, color='gray', lw=0.5, ls='--')
axes[0, 0].set_xlabel('时间 t (s)')
axes[0, 0].set_ylabel('位移 x (m)')
axes[0, 0].set_title('位移随时间衰减')
axes[0, 0].grid(alpha=0.3)

# 2. 相图
axes[0, 1].plot(x, v, 'r-', lw=0.8)
axes[0, 1].set_xlabel('位移 x (m)')
axes[0, 1].set_ylabel('速度 v (m/s)')
axes[0, 1].set_title('相图（螺旋衰减到原点）')
axes[0, 1].grid(alpha=0.3)

# 3. 能量衰减
axes[1, 0].plot(t, energy, 'g-', lw=1)
axes[1, 0].set_yscale('log')  # 对数坐标更好看指数衰减
axes[1, 0].set_xlabel('时间 t (s)')
axes[1, 0].set_ylabel('总能量 E (J)')
axes[1, 0].set_title('能量指数衰减（对数坐标）')
axes[1, 0].grid(alpha=0.3)

# 4. 快速傅里叶变换
from scipy.fft import fft, fftfreq
n = len(t)
dt = t[1] - t[0]
spectrum = np.abs(fft(x))
freqs = fftfreq(n, dt)

positive_mask = freqs > 0
axes[1, 1].plot(freqs[positive_mask], spectrum[positive_mask], 'm-', lw=1)
axes[1, 1].set_xlim(0, 2)
axes[1, 1].set_xlabel('频率 f (Hz)')
axes[1, 1].set_ylabel('振幅')
axes[1, 1].set_title('频谱（峰在固有频率附近）')
axes[1, 1].grid(alpha=0.3)

fig.suptitle('阻尼谐振子完整分析', fontsize=14, fontweight='bold')
plt.tight_layout()
plt.show()
```

---

## 第 14 课：面向对象编程——组织大型程序的方式

### 14.1 类与对象的概念

**类（Class）** 是蓝图/模板，**对象（Object）** 是根据蓝图制造出来的实际东西。

举个例子：
- 「谐振子」是一个**类**——它描述了谐振子的共性：有质量、有劲度系数、会振动
- 你创建的一个具体的谐振子（质量 1kg，劲度系数 10N/m）是一个**对象**

### 14.2 定义你的第一个类

```python
class HarmonicOscillator:
    """谐振子类"""
    
    def __init__(self, mass, spring_constant):
        """
        初始化方法：创建对象时自动调用
        self：指向对象本身的特殊参数
        """
        self.mass = mass                    # 存储质量
        self.k = spring_constant            # 存储劲度系数
        self.omega = (spring_constant / mass) ** 0.5  # 角频率
        self.position = 1.0                 # 初始位移
        self.velocity = 0.0                 # 初始速度
        self.time = 0.0                     # 当前时间
    
    def step(self, dt):
        """推进一个时间步（Euler 法）"""
        acceleration = -self.k / self.mass * self.position
        self.velocity += acceleration * dt
        self.position += self.velocity * dt
        self.time += dt
    
    def energy(self):
        """计算当前总能量"""
        ke = 0.5 * self.mass * self.velocity**2
        pe = 0.5 * self.k * self.position**2
        return ke + pe
    
    def get_state(self):
        """返回当前状态"""
        return (self.time, self.position, self.velocity)
```

### 14.3 使用类

```python
# 创建一个谐振子对象
osc = HarmonicOscillator(mass=1.0, spring_constant=10.0)

print(f"角频率: {osc.omega:.4f} rad/s")
print(f"初始能量: {osc.energy():.4f} J")

# 运行 1000 步
dt = 0.01
history = []
for i in range(1000):
    osc.step(dt)
    history.append(osc.get_state())

# 把历史数据提取出来
times = [h[0] for h in history]
positions = [h[1] for h in history]

print(f"最终时间: {osc.time:.2f} s")
print(f"最终能量: {osc.energy():.4f} J")
```

> 📘 **`self` 是什么？** 当你在类里面定义方法时，第一个参数必须是 `self`，它代表「调用这个方法的那个对象」。`osc.step(dt)` 实际调用中，Python 自动把 `osc` 传给 `self`。不需要你手动传。

### 14.4 继承：复用已有类

物理中很多东西有共性。比如电子、质子、中子都是粒子，有很多共同属性。

```python
class Particle:
    """基类：所有粒子的共同特性和行为"""
    def __init__(self, name, mass, charge):
        self.name = name
        self.mass = mass
        self.charge = charge
        self.position = np.zeros(3)
        self.velocity = np.zeros(3)
    
    def kinetic_energy(self):
        return 0.5 * self.mass * np.sum(self.velocity**2)
    
    def info(self):
        return f"{self.name}: m={self.mass:.2e} kg, q={self.charge:.2e} C"

class Electron(Particle):
    """电子类：继承自 Particle"""
    def __init__(self):
        # 调用父类的初始化，传入电子的标准参数
        super().__init__("电子", 9.109e-31, -1.602e-19)
        self.spin = 0.5  # 电子特有的属性
    
    def info(self):
        """重写父类方法，添加自旋信息"""
        base_info = super().info()
        return f"{base_info}, spin={self.spin}"


class Proton(Particle):
    """质子类"""
    def __init__(self):
        super().__init__("质子", 1.673e-27, 1.602e-19)
        self.spin = 0.5

# 使用
e = Electron()
p = Proton()
print(e.info())
print(p.info())
print(f"电子动能：{e.kinetic_energy():.2e} J")
```

### 14.5 什么时候需要用类

| 场景 | 用函数就够了 | 用类更好 |
|------|------------|---------|
| 小型计算（< 50 行） | ✅ | 杀鸡用牛刀 |
| 需要保存多个状态变量 | | ✅ |
| 多个类似的对象需要管理 | | ✅ |
| 代码会不断扩展 | | ✅ |
| 团队协作 | | ✅ |

---

## 第 15 课：错误处理——写出健壮的代码

### 15.1 常见的错误类型

```python
# NameError：变量名未定义
# print(undefined_variable)

# TypeError：类型错误
# result = "hello" + 42

# ValueError：值错误
# int("hello")   # "hello" 不能转换成整数

# IndexError：列表索引越界
# lst = [1, 2, 3]
# print(lst[10])

# ZeroDivisionError：除以零
# x = 1 / 0

# FileNotFoundError：文件不存在
# with open("不存在的文件.txt") as f:
#     pass
```

### 15.2 `try-except`——捕获和处理错误

```python
# 不用 try-except：一个错误就让整个程序崩溃
def safe_divide(a, b):
    try:
        result = a / b
        return result
    except ZeroDivisionError:
        print("错误：除以零！")
        return float('nan')   # 返回 NaN (Not a Number)
    except TypeError as e:
        print(f"类型错误：{e}")
        return None

print(safe_divide(10, 2))   # 5.0
print(safe_divide(10, 0))   # nan（程序没有崩溃！）
```

### 15.3 `try-except-else-finally`

```python
def load_data(filename):
    try:
        file = open(filename, 'r')
    except FileNotFoundError:
        print(f"文件 '{filename}' 不存在，使用默认数据")
        return [0.0, 0.0, 0.0]
    else:
        # 没有异常时执行
        data = file.read()
        return data
    finally:
        # 无论如何都会执行（清理操作）
        file.close()

# else 和 finally 是可选的，大多数情况下只需要 try-except
```

### 15.4 用 `assert` 做防御性检查

```python
def calculate_period(length):
    """
    计算单摆周期
    length: 摆长（米），必须为正数
    """
    assert length > 0, f"摆长必须为正数，得到 length={length}"
    import math
    return 2 * math.pi * math.sqrt(length / 9.8)

print(calculate_period(1.0))   # 正常：2.006...
# print(calculate_period(-0.5))  # 触发 AssertionError
```

> 💡 `assert` 适合在开发阶段检查「不可能出现」的条件。生产代码中应使用更温和的错误处理。

---

## 第 16 课：综合实战——谐振子仿真

### 16.1 从物理方程到完整仿真程序

让我们把前面学的所有知识串起来，写一个完整的**阻尼谐振子仿真程序**。

> **物理模型**：$m\ddot{x} + b\dot{x} + kx = 0$
> 
> 化简：$\ddot{x} + 2\beta\dot{x} + \omega_0^2 x = 0$
> 
> 其中 $\omega_0 = \sqrt{k/m}$，$\beta = b/(2m)$

### 16.2 完整程序

```python
"""
阻尼谐振子仿真 —— Python 零基础教程结业项目
==============================================
功能：
1. 使用 RK4 方法数值求解阻尼谐振子
2. 对比不同阻尼系数（欠阻尼/临界阻尼/过阻尼）
3. 可视化：位移、相图、能量
4. 保存结果到文件
"""

import numpy as np
import matplotlib.pyplot as plt
from pathlib import Path

# ==================== 物理计算函数 ====================

def oscillator_rhs(t, state, omega0, beta):
    """
    谐振子运动方程的右边项
    将二阶 ODE 化为两个一阶 ODE：
        state[0] = x  (位移)
        state[1] = v  (速度)
    返回：
        dx/dt = v
        dv/dt = -omega0²·x - 2·beta·v
    """
    x, v = state
    dxdt = v
    dvdt = -omega0**2 * x - 2 * beta * v
    return np.array([dxdt, dvdt])


def rk4_step(f, t, y, dt, *args):
    """
    四阶 Runge-Kutta 单步推进
    f: 右边项函数 (t, y, *args)
    t: 当前时间
    y: 当前状态向量
    dt: 时间步长
    *args: 额外参数传给 f
    """
    k1 = f(t, y, *args)
    k2 = f(t + dt/2, y + dt/2 * k1, *args)
    k3 = f(t + dt/2, y + dt/2 * k2, *args)
    k4 = f(t + dt, y + dt * k3, *args)
    return y + dt / 6 * (k1 + 2*k2 + 2*k3 + k4)


def run_simulation(omega0=2.0, beta=0.2, x0=1.0, v0=0.0,
                   dt=0.01, t_max=20.0):
    """
    运行一次谐振子仿真
    参数：
        omega0: 固有角频率
        beta:   阻尼系数
        x0, v0: 初始位移和初速度
        dt:     时间步长
        t_max:  仿真总时长
    返回：
        t: 时间数组
        x: 位移数组
        v: 速度数组
        e: 总能量数组
    """
    n_steps = int(t_max / dt)
    
    # 预分配数组（比 append 快得多）
    t = np.zeros(n_steps + 1)
    x = np.zeros(n_steps + 1)
    v = np.zeros(n_steps + 1)
    
    # 初始条件
    state = np.array([x0, v0])
    t[0] = 0.0
    x[0], v[0] = state
    
    # 时间推进
    for i in range(n_steps):
        state = rk4_step(oscillator_rhs, t[i], state, dt, omega0, beta)
        t[i+1] = t[i] + dt
        x[i+1], v[i+1] = state
        
        # 安全检查：如果位移发散，提前终止
        if abs(x[i+1]) > 1e6:
            print(f"警告：解在 t={t[i+1]:.2f} 处发散，终止仿真")
            return t[:i+2], x[:i+2], v[:i+2], np.zeros(i+2)
    
    # 计算能量
    e = 0.5 * v**2 + 0.5 * omega0**2 * x**2
    
    return t, x, v, e


# ==================== 主程序 ====================

if __name__ == "__main__":  # 只在直接运行这个文件时执行
    print("=" * 50)
    print("阻尼谐振子仿真")
    print("=" * 50)
    
    # 设置参数
    omega0 = 2.0    # 固有角频率
    dt = 0.01
    t_max = 20.0
    
    # 运行三种阻尼情况
    damping_cases = {
        "欠阻尼 (β=0.2)": 0.2,
        "临界阻尼 (β=2.0)": 2.0,
        "过阻尼 (β=5.0)": 5.0,
    }
    
    results = {}
    for label, beta in damping_cases.items():
        print(f"\n运行 {label}...")
        t, x, v, e = run_simulation(omega0=omega0, beta=beta, 
                                     dt=dt, t_max=t_max)
        results[label] = {"t": t, "x": x, "v": v, "e": e}
        print(f"  完成 {len(t)} 步, 最终能量 = {e[-1]:.6f}")
    
    # ==================== 可视化 ====================
    fig, axes = plt.subplots(2, 3, figsize=(15, 8))
    
    colors = ['b', 'r', 'g']
    
    for idx, (label, data) in enumerate(results.items()):
        c = colors[idx]
        
        # 位移-时间
        axes[0, 0].plot(data["t"], data["x"], color=c, lw=1, label=label)
        
        # 相图
        axes[0, 1].plot(data["x"], data["v"], color=c, lw=0.7)
        
        # 能量-时间
        axes[0, 2].plot(data["t"], data["e"], color=c, lw=1)
    
    axes[0, 0].axhline(0, color='gray', lw=0.5)
    axes[0, 0].set_xlabel('时间 t (s)')
    axes[0, 0].set_ylabel('位移 x (m)')
    axes[0, 0].set_title('位移时间序列')
    axes[0, 0].legend(fontsize=8)
    axes[0, 0].grid(alpha=0.3)
    
    axes[0, 1].set_xlabel('位移 x (m)')
    axes[0, 1].set_ylabel('速度 v (m/s)')
    axes[0, 1].set_title('相图')
    axes[0, 1].grid(alpha=0.3)
    
    axes[0, 2].set_xlabel('时间 t (s)')
    axes[0, 2].set_ylabel('总能量 E (J)')
    axes[0, 2].set_title('能量衰减')
    axes[0, 2].grid(alpha=0.3)
    
    # 第二行：欠阻尼放大分析
    data_under = results["欠阻尼 (β=0.2)"]
    t_u, x_u, v_u, e_u = data_under["t"], data_under["x"], data_under["v"], data_under["e"]
    
    # 位移前 5 秒放大
    mask = t_u <= 5
    axes[1, 0].plot(t_u[mask], x_u[mask], 'b-', lw=1)
    axes[1, 0].axhline(0, color='gray', lw=0.5)
    axes[1, 0].set_xlabel('时间 t (s)')
    axes[1, 0].set_ylabel('位移 x (m)')
    axes[1, 0].set_title('欠阻尼：前 5 秒细节')
    axes[1, 0].grid(alpha=0.3)
    
    # 能量对数坐标
    axes[1, 1].semilogy(t_u, e_u, 'b-', lw=1)
    axes[1, 1].set_xlabel('时间 t (s)')
    axes[1, 1].set_ylabel('总能量 E (J)')
    axes[1, 1].set_title('欠阻尼：能量（对数坐标）')
    axes[1, 1].grid(alpha=0.3)
    
    # 频谱分析
    from scipy.fft import fft, fftfreq
    n = len(t_u)
    dt_val = t_u[1] - t_u[0]
    spectrum = np.abs(fft(x_u))
    freqs = fftfreq(n, dt_val)
    pos = freqs > 0
    axes[1, 2].plot(freqs[pos], spectrum[pos], 'b-', lw=1)
    axes[1, 2].set_xlim(0, 1.5)
    axes[1, 2].set_xlabel('频率 f (Hz)')
    axes[1, 2].set_ylabel('振幅')
    axes[1, 2].set_title('欠阻尼：频谱')
    axes[1, 2].grid(alpha=0.3)
    
    fig.suptitle('阻尼谐振子仿真完整分析', fontsize=14, fontweight='bold')
    plt.tight_layout()
    
    # 保存图片
    output_dir = Path("output")
    output_dir.mkdir(exist_ok=True)
    plt.savefig(output_dir / "harmonic_oscillator_analysis.png", 
                dpi=150, bbox_inches='tight')
    print(f"\n图表已保存到 {output_dir / 'harmonic_oscillator_analysis.png'}")
    plt.show()
    
    # ==================== 输出结果摘要 ====================
    print("\n" + "=" * 50)
    print("结果摘要")
    print("=" * 50)
    for label, data in results.items():
        x_final = data["x"][-1]
        e_initial = data["e"][0]
        e_final = data["e"][-1]
        print(f"{label}:")
        print(f"  最终位移: {x_final:.6f} m")
        print(f"  能量保持率: {e_final/e_initial*100:.2f}%")
    
    print("\n仿真完成！")
```

### 16.3 运行结果解读

运行这个程序，你会得到：

1. **位移-时间图**：展示了欠阻尼（振荡衰减）、临界阻尼（最快回到平衡位置而不振荡）、过阻尼（缓慢回到平衡位置）
2. **相图**：欠阻尼呈螺旋线（焦点），临界阻尼和过阻尼直接趋向原点（结点）
3. **能量图**：衰减速率和阻尼系数成正比
4. **频谱图**：欠阻尼时有一个峰（阻尼使得频率略小于固有频率）

---

## 附录：常见问题与排错指南

### A.1 最常见的 10 个错误

| # | 错误信息 | 原因 | 解决方法 |
|---|---------|------|---------|
| 1 | `SyntaxError: invalid syntax` | 语法错误 | 检查括号、引号是否配对，冒号是否遗漏 |
| 2 | `NameError: name 'xxx' is not defined` | 变量未定义 | 检查拼写，确认是否在使用前定义了变量 |
| 3 | `IndentationError` | 缩进错误 | 使用 4 个空格缩进，不要混用 Tab 和空格 |
| 4 | `TypeError: can't multiply...` | 类型不匹配 | 检查数据类型，需要时用 `int()` / `float()` 转换 |
| 5 | `IndexError: list index out of range` | 索引越界 | 检查列表长度，记住索引从 0 开始 |
| 6 | `ZeroDivisionError` | 除以零 | 在除法前检查分母是否为零 |
| 7 | `AttributeError: 'xxx' object has no attribute...` | 属性不存在 | 检查对象类型和属性名拼写 |
| 8 | `ImportError: No module named 'xxx'` | 模块未安装 | `pip install xxx` |
| 9 | `KeyError: 'xxx'` | 字典键不存在 | 检查键名或用 `.get()` 方法 |
| 10 | 代码不报错但结果不对 | 逻辑错误 | 打印中间变量排查，做简单用例验证 |

### A.2 调试技巧

```python
# 技巧1：用 print 打印中间值
def buggy_function(x):
    result = x * 2 + 1
    print(f"DEBUG: x={x}, result={result}")  # 看看中间结果对不对
    return result

# 技巧2：用 assert 检查假设
def compute_sqrt(x):
    assert x >= 0, f"x 必须非负，得到 {x}"
    return x ** 0.5

# 技巧3：用小数据测试
# 如果仿真 10000 步出问题，先试试 10 步能不能跑通

# 技巧4：二分法定位 bug
# 注释掉一半代码 → 运行 → 如果正常，bug 在被注释的部分
```

### A.3 去哪里求助

1. **Python 官方文档**：https://docs.python.org/zh-cn/3/（有中文版！）
2. **Stack Overflow**：https://stackoverflow.com/（编程问答社区，几乎所有问题都有人问过）
3. **NumPy 文档**：https://numpy.org/doc/stable/
4. **Matplotlib 文档**：https://matplotlib.org/stable/gallery/
5. **ChatGPT / Claude**：把错误信息贴给 AI，通常会给出有用的建议
6. **同事/学长**：有时候人眼比 AI 更容易发现问题

### A.4 编程好习惯清单

- [ ] 变量名有意义（不用 `a`, `b`, `c`, `temp`）
- [ ] 函数短小精悍（每个函数只做一件事，< 30 行）
- [ ] 写文档字符串（`"""函数说明"""`）
- [ ] 关键步骤加注释（但不是每行都注释）
- [ ] 保持代码格式一致（用 VS Code 的自动格式化：`Alt + Shift + F`）
- [ ] 用 git 管理版本（初学者可先跳过，但要知道有这个东西）
- [ ] 在运行大计算前先用小数据测试
- [ ] 保存中间结果，避免重新计算

---

## 结语

你学完了本教程的全部 16 课，已经掌握了 Python 的核心语法、数据处理、科学计算和可视化的基础知识。

**接下来做什么？**

1. **动手写代码**。打开 VS Code，把教程里的代码亲手敲一遍（不要复制粘贴）。每个报错都是学习机会。
2. **选一个物理问题**。从你最熟悉的领域（力学、电磁学、热学...）选一个简单问题，尝试自己写仿真程序。
3. **阅读与修改**。下载别人的仿真代码，尝试理解并修改参数，看看结果如何变化。
4. **进阶学习**。当你熟悉了 Python 基础后，学习《物理仿真手册》中的数值算法（ODE 求解器、PDE 有限差分、蒙特卡洛方法等），将你的 Python 技能转化为真正的仿真能力。

> 记住：编程不是看会的，是写会的。祝你在物理仿真的道路上越走越远！🚀

---

*教程版本：v1.0 | 面向零基础物理专业学生*