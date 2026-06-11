# Python 仿真编程速成指南 —— 从零写出专业仿真代码

> 面向物理专业学生的 Python 速成手册。不讲废话，只教写仿真最需要的部分。
> 配合《物理仿真速成指南》食用效果最佳。

---

## 目录

1. [为什么 Python 是物理仿真的首选](#1-为什么-python-是物理仿真的首选)
2. [Python 语法骨架（会这些就够了）](#2-python-语法骨架会这些就够了)
3. [NumPy：仿真代码的血液](#3-numpy仿真代码的血液)
4. [SciPy：仿真工具箱](#4-scipy仿真工具箱)
5. [Matplotlib：让数据说话](#5-matplotlib让数据说话)
6. [仿真代码的设计模式](#6-仿真代码的设计模式)
7. [性能优化实战](#7-性能优化实战)
8. [调试与排错](#8-调试与排错)
9. [速查表：30 个仿真高频操作](#9-速查表30-个仿真高频操作)
10. [完整项目模板](#10-完整项目模板)

---

## 1. 为什么 Python 是物理仿真的首选

| 特性 | Python | C++ | MATLAB |
|------|--------|-----|--------|
| 上手难度 | ★☆☆ | ★★★ | ★★☆ |
| 科学计算生态 | NumPy/SciPy 无敌 | 需自己造轮子 | 自带但付费 |
| 可视化 | Matplotlib/Mayavi | 困难 | 自带 |
| 运行速度 | 中（可加速） | 极快 | 中 |
| 科研用比例 | 70%+ 且增长中 | 遗留代码 | 工程多 |
| 与其他工具对接 | AI、实验仪器、数据处理 | 有限 | 封闭 |

**结论：** 用 Python 写原型和日常计算，瓶颈处用 Numba 加速，永不后悔。

---

## 2. Python 语法骨架（会这些就够了）

### 2.1 变量与基本类型

```python
# 数值
x = 3.14          # 浮点
n = 100           # 整数
flag = True       # 布尔
z = 2 + 3j        # 复数（量子力学必备！）

# 序列
a = [1, 2, 3--890 , 4]            # 列表（可变）

t6 = (1, 2, 3)               # 元组（不可变）
s = "hello"                 # 字符串（不可变）

# 列表推导式 —— Python 的灵魂语法
squares = [i**2 for i in range(10)]                # [0, 1, 4, 9, ...]
evens = [i for i in range(20) if i % 2 == 0]       # 条件筛选
pairs = [(x, y) for x in range(3) for y in range(2)]  # 嵌套
```

### 2.2 函数定义（关键：可返回多个值）

```python
def compute_energy_and_force(positions):
    """计算系统的能量和力，返回元组"""
    energy = 0.0
    forces = np.zeros_like(positions)
    # ... 计算 ...
    return energy, forces  # 一行返回多个值！

# 调用
E, F = compute_energy_and_force(r)  # 直接解包
```

### 2.3 条件与循环

```python
# if-elif-else
if condition:
    ...
elif other_condition:
    ...-lse:
    ...

# for 循环（仿真中最常见的写法）
for i in range(n_steps):
    # 时间推进
    ...

# while 循环（用在收敛判断）
while error > tolerance:
    # 迭代求解
    ...
```

### 2.4 类 —— 组织仿真代码的最佳方式

```python
class HarmonicOscillator:
    """谐振子仿真器"""
    
    def __init__(self, omega0=1.0, damping=0.0):
        self.omega0 = omega0
        self.damping = damping
        self.x = 1.0      # 位移
        self.v = 0.0      # 速度
        self.t = 0.0      # 时间
        self.history = [] # 记录历史
    
    def step(self, dt):
        """RK4 单步推进"""
        # ... RK4 实现 ...
        self.t += dt
        self.history.append((self.t, self.x, self.v))
    
    def run(self, t_max, dt=0.01):
        """运行仿真到指定时间"""
        while self.t < t_max:
            self.step(dt)
        return np.array(self.history)

# 使用
osc = HarmonicOscillator(omega0=2.0, damping=0.3)
data = osc.run(t_max=10)
```

### 2.5 Python 中需要特别小心的坑

```python
# 坑1：可变默认参数
def bad(lst=[]):          # ❌ 所有调用共享同一个列表
    lst.append(1)
    return lst

def good(lst=None):        # ✅
    if lst is None:
        lst = []
    lst.append(1)
    return lst

# 坑2：浮点比较
0.1 + 0.2 == 0.3           # False！（浮点误差）
abs(0.1 + 0.2 - 0.3) < 1e-12  # True ✅

# 坑3：复制（仿真中经常踩）
import copy
a = [1, 2, [3, 4]]
b = a.copy()               # 浅复制，b[2] 和 a[2] 是同一个
c = copy.deepcopy(a)       # 深复制，完全独立 ✅
```

---

## 3. NumPy：仿真代码的血液

> **如果你只学一个库，学 NumPy。** 整个 Python 科学计算生态都建立在 NumPy 的 ndarray 之上。

### 3.1 创建数组

```python
import numpy as np

# 从列表创建
a = np.array([1, 2, 3, 4, 5])

# 特殊数组
np.zeros(10)              # 全0：[0,0,0,0,0,0,0,0,0,0]
np.ones(5)                # 全1
np.eye(3)                 # 3×3 单位矩阵
np.diag([1, 2, 3])        # 对角矩阵
np.empty(100)             # 未初始化（快，但须立即赋值）

# 序列
np.arange(0, 10, 0.1)     # [0, 0.1, 0.2, ..., 9.9] —— 最常用
np.linspace(0, 1, 100)    # 0到1等距100个点 —— 网格生成必备

# 网格
x, y = np.meshgrid(np.linspace(0,1,50), np.linspace(0,1,50))
# → 50×50 的二维坐标网格，矢量化计算场必备

# 随机
np.random.uniform(0, 1, 100)     # 均匀分布
np.random.normal(0, 1, 100)      # 正态分布
np.random.randint(0, 100, 50)    # 整数随机
np.random.seed(42)                # 固定种子，实验可重复
```

### 3.2 数组的形状操作（仿真中天天用）

```python
a = np.arange(12)          # [0,1,2,...,11]  形状: (12,)

a.reshape(3, 4)            # 变成 3×4 矩阵
a.reshape(-1, 1)           # 变成列向量 (-1 = 自动推断)
a[:, np.newaxis]           # 同上，升维

# 拼接
np.concatenate([a, b])     # 沿现有轴拼接
np.stack([a, b], axis=0)   # 沿新轴堆叠

# 切片（和列表一样，但更强大）
arr = np.arange(20).reshape(4, 5)
arr[0, :]      # 第一行
arr[:, -1]     # 最后一列
arr[1:3, 2:4]  # 子矩阵
arr[::2, ::2]  # 每隔一个取

# 花式索引
idx = [0, 2, 3]
arr[idx]       # 取第 0,2,3 行
mask = arr > 5
arr[mask]      # 取所有 >5 的元素
```

### 3.3 向量化运算 —— NumPy 的精髓

```python
# 所有运算都是逐元素的
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

a + b     # [5, 7, 9]      逐元素加
a * b     # [4, 10, 18]    逐元素乘（不是矩阵乘！）
a ** 2    # [1, 4, 9]      逐元素平方
np.sin(a) # [sin(1), sin(2), sin(3)]

# 矩阵运算
A @ B           # 矩阵乘法（Python 3.5+）
np.dot(A, B)    # 同上
np.linalg.norm(v)        # 向量模长
np.linalg.eig(M)         # 特征值分解
np.linalg.solve(A, b)    # 解 Ax = b
```

### 3.4 广播（Broadcasting）—— 不写循环的秘密武器

```python
# 不同形状的数组也能运算！
a = np.array([[1,2,3], [4,5,6]])   # (2, 3)
b = np.array([10, 20, 30])         # (3,)
a + b  # 自动把 b 扩展成 (2,3)，然后逐元素相加
# 结果: [[11, 22, 33], [14, 25, 36]]

# 仿真典型场景：算所有点对距离
positions = np.random.randn(100, 3)  # 100 个三维粒子
# 每个粒子到原点的距离（一行搞定）
distances = np.linalg.norm(positions, axis=1)  # → (100,)

# 所有粒子之间的 pairwise 距离
diff = positions[:, np.newaxis, :] - positions[np.newaxis, :, :]  # (100, 100, 3)
pairwise_dist = np.linalg.norm(diff, axis=2)  # (100, 100)
```

### 3.5 聚合运算

```python
a = np.array([[1, 2, 3], [4, 5, 6]])

a.sum()         # 全部求和: 21
a.sum(axis=0)   # 按列求和: [5, 7, 9]
a.sum(axis=1)   # 按行求和: [6, 15]
a.mean()        # 均值
a.std()         # 标准差
a.min()         # 最小值
a.argmax()      # 最大值的位置（索引）
np.cumsum(a)    # 累积和

# 仿真中最常用的：按条件统计
np.sum(arr > threshold)          # 有多少个超过阈值
np.mean(arr[arr > 0])            # 正值的均值
np.where(arr > 0, arr, 0)        # 把所有负值替换为0
```

---

## 4. SciPy：仿真工具箱

### 4.1 积分与ODE —— 最核心的功能

```python
from scipy.integrate import solve_ivp, quad, dblquad
from scipy.optimize import root, minimize, curve_fit

# --- 数值积分 ---
result, error = quad(lambda x: np.sin(x)**2, 0, np.pi)
# result = π/2, error = 估计误差

# --- ODE 求解 ---
def pendulum(t, y, g, L):
    """单摆: θ'' = -g/L sin(θ)"""
    theta, omega = y
    return [omega, -g/L * np.sin(theta)]

sol = solve_ivp(
    pendulum,
    t_span=(0, 10),          # 积分时间范围
    y0=[np.pi/3, 0],         # 初始 [角度, 角速度]
    args=(9.8, 1.0),         # 传给 pendulum 的额外参数
    method='RK45',           # 默认自适应RK45
    rtol=1e-8, atol=1e-10,   # 相对/绝对误差容限
    dense_output=True,        # 生成插值函数，可在任意点取值
    max_step=0.01             # 最大步长限制
)

# 获取解
t_eval = np.linspace(0, 10, 1000)
y = sol.sol(t_eval)          # 在 t_eval 点插值

# --- 求解非线性方程 ---
def f_to_solve(x):
    return x**3 - 2*x - 5     # 求 x³ - 2x - 5 = 0 的根

solution = root(f_to_solve, x0=2.0)  # x0 是初始猜测
print(solution.x)  # 精确的根

# --- 曲线拟合（实验数据处理必备）---
def model(x, a, b, c):
    return a * np.exp(-b * x) + c

x_data = np.array([0, 1, 2, 3, 4, 5])
y_data = np.array([2.1, 1.5, 1.2, 1.0, 0.9, 0.85])

popt, pcov = curve_fit(model, x_data, y_data, p0=[1, 0.5, 0.5])
# popt = [a, b, c] 最优参数
# pcov = 协方差矩阵（对角线是参数方差）
```

### 4.2 线性代数与稀疏矩阵

```python
from scipy import sparse
from scipy.sparse.linalg import spsolve

# 构建一维 Laplace 算子的稀疏矩阵
N = 100
main_diag = -2 * np.ones(N)
off_diag = np.ones(N-1)

# 用 COO 格式构建
diagonals = [main_diag, off_diag, off_diag]
A = sparse.diags(diagonals, [0, -1, 1], shape=(N, N))  # 三对角！只有 ~3N 个非零元

# 对比：稠密矩阵存储 = 10000 个元素，稀疏 = 298 个元素

# 解稀疏线性系统
b = np.ones(N)
x = spsolve(A, b)  # 自动选最优求解算法
```

### 4.3 信号处理与 FFT

```python
from scipy.fft import fft, fftfreq, ifft

# 时域信号
N = 1000
dt = 0.01
t = np.arange(N) * dt
signal = np.sin(2*np.pi*5*t) + 0.5*np.sin(2*np.pi*20*t) + 0.1*np.random.randn(N)

# FFT
spectrum = fft(signal)
freqs = fftfreq(N, dt)  # 频率轴

# 功率谱
power = np.abs(spectrum)**2

# 只保留正频率
positive = freqs > 0
plt.plot(freqs[positive], power[positive])
plt.xlabel('频率 (Hz)')
# 会在 5 Hz 和 20 Hz 看到两个峰
```

### 4.4 插值 —— 实验数据的连续化

```python
from scipy.interpolate import interp1d, RegularGridInterpolator

# 1D 插值
x = np.array([0, 1, 2, 3, 4])
y = np.array([0, 1, 4, 9, 16])
f = interp1d(x, y, kind='cubic')  # 线性/二次/三次
print(f(2.5))  # 在任意点取值 → 约 6.25

# 3D 插值（场仿真后处理必备）
x = np.linspace(0, 10, 20)
y = np.linspace(0, 10, 30)
z = np.linspace(0, 10, 40)
data = np.random.randn(20, 30, 40)  # 三维标量场

interpolator = RegularGridInterpolator((x, y, z), data)
point = [5.5, 3.2, 7.8]
value = interpolator(point)  # 在任意三维点取值
```

---

## 5. Matplotlib：让数据说话

### 5.1 基础绘图模板

```python
import matplotlib.pyplot as plt

# 仿真绘图的标准模板
fig, axes = plt.subplots(2, 2, figsize=(12, 8))  # 创建 2×2 子图

# 左上：时间序列
axes[0, 0].plot(t, x, 'b-', linewidth=1.5, label='位移')
axes[0, 0].plot(t, v, 'r--', linewidth=1.5, label='速度')
axes[0, 0].axhline(0, color='gray', linewidth=0.5)  # 零线
axes[0, 0].set_xlabel('时间 t'); axes[0, 0].set_ylabel('响应')
axes[0, 0].legend(); axes[0, 0].grid(alpha=0.3)

# 右上：相图
axes[0, 1].plot(x, v, 'k-', linewidth=1)
axes[0, 1].set_xlabel('位移 x'); axes[0, 1].set_ylabel('速度 v')
axes[0, 1].set_title('相图')

# 左下：频谱
axes[1, 0].semilogy(freqs, power, 'b-')
axes[1, 0].set_xlabel('频率'); axes[1, 0].set_ylabel('功率谱密度')

# 右下：能谱
axes[1, 1].plot(E_k, 'r-')
axes[1, 1].set_xlabel('波数 k'); axes[1, 1].set_ylabel('E(k)')

plt.tight_layout()
plt.savefig('result.png', dpi=150, bbox_inches='tight')
plt.show()
```

### 5.2 2D 场可视化（电磁场/流场必备）

```python
# 三种画二维标量场的方式

# 方式1：pcolormesh（最快，适合大数据）
plt.pcolormesh(X, Y, field, shading='auto', cmap='RdBu_r')
plt.colorbar(label='场值')

# 方式2：contourf（平滑填充）
plt.contourf(X, Y, field, levels=50, cmap='viridis')

# 方式3：imshow（像素级，最快）
plt.imshow(field, extent=[xmin, xmax, ymin, ymax],
           origin='lower', cmap='hot', aspect='auto')

# 叠加矢量场（流线）
plt.streamplot(X, Y, U, V, density=1.5, color='white', linewidth=0.5)

# 叠加矢量场（箭头）—— 本项目 bio_savart 就在用
plt.quiver(X[::skip, ::skip], Y[::skip, ::skip],
           U[::skip, ::skip], V[::skip, ::skip],
           scale=50, alpha=0.7)
```

### 5.3 3D 可视化

```python
from mpl_toolkits.mplot3d import Axes3D

fig = plt.figure(figsize=(10, 8))
ax = fig.add_subplot(111, projection='3d')

# 3D 散点
ax.scatter(x, y, z, c=energy, cmap='plasma', s=10, alpha=0.8)

# 3D 线图（轨迹）
ax.plot(trajectory[:,0], trajectory[:,1], trajectory[:,2], 'b-', lw=0.5)

# 3D 曲面
X, Y = np.meshgrid(np.linspace(-2, 2, 50), np.linspace(-2, 2, 50))
Z = X * np.exp(-X**2 - Y**2)
ax.plot_surface(X, Y, Z, cmap='coolwarm', alpha=0.8)

ax.set_xlabel('X'); ax.set_ylabel('Y'); ax.set_zlabel('Z')
plt.show()
```

### 5.4 动画（演示仿真演化过程）

```python
import matplotlib.animation as animation

fig, ax = plt.subplots(figsize=(8, 6))
line, = ax.plot([], [], 'b-', lw=2)
time_text = ax.text(0.02, 0.95, '', transform=ax.transAxes)

def init():
    ax.set_xlim(-2, 2)
    ax.set_ylim(-2, 2)
    line.set_data([], [])
    return line, time_text

def animate(frame):
    # 每一帧更新的内容
    t = frame * dt
    x = np.cos(omega * t)    # 你的仿真数据
    y = np.sin(omega * t)
    line.set_data(x, y)
    time_text.set_text(f't = {t:.2f}s')
    return line, time_text

ani = animation.FuncAnimation(
    fig, animate, frames=500, init_func=init,
    interval=20, blit=True
)

# 保存为视频
ani.save('simulation.mp4', writer='ffmpeg', fps=30, dpi=150)
plt.show()
```

---

## 6. 仿真代码的设计模式

### 6.1 模式一：时间推进循环（最经典）

```python
class Simulation:
    def __init__(self, dt=0.01):
        self.dt = dt
        self.state = None       # 系统状态
        self.time = 0.0
        self.history = []       # 存储历史
    
    def initialize(self):
        """设置初始条件"""
        ...
    
    def compute_rhs(self, state):
        """计算状态的时间导数"""
        ...
    
    def step(self):
        """单步推进"""
        rhs = self.compute_rhs(self.state)
        self.state += rhs * self.dt
        self.time += self.dt
        self.history.append(np.copy(self.state))
    
    def run(self, n_steps):
        """运行仿真"""
        self.initialize()
        for _ in range(n_steps):
            self.step()
        return np.array(self.history)
```

### 6.2 模式二：面向对象的物理系统

```python
class Particle:
    """单个粒子"""
    def __init__(self, mass, position, velocity):
        self.m = mass
        self.r = np.array(position, dtype=float)
        self.v = np.array(velocity, dtype=float)
        self.f = np.zeros(3)  # 当前受力

class NBodySystem:
    """多粒子系统"""
    def __init__(self):
        self.particles: list[Particle] = []
    
    def add_particle(self, m, r, v):
        self.particles.append(Particle(m, r, v))
    
    def compute_forces(self):
        """计算所有粒子间相互作用力"""
        for p in self.particles:
            p.f = np.zeros(3)
        # 两两相互作用
        for i, pi in enumerate(self.particles):
            for j, pj in enumerate(self.particles[i+1:], i+1):
                dr = pj.r - pi.r
                dist = np.linalg.norm(dr)
                force = self.force_law(dist) * dr / dist
                pi.f += force
                pj.f -= force  # 牛顿第三定律
    
    def velocity_verlet_step(self, dt):
        """Verlet 时间推进"""
        for p in self.particles:
            p.v += 0.5 * p.f / p.m * dt
            p.r += p.v * dt
        self.compute_forces()
        for p in self.particles:
            p.v += 0.5 * p.f / p.m * dt
```

### 6.3 模式三：网格/场（PDE 仿真用）

```python
class ScalarField2D:
    """二维标量场（热传导/电势/波函数模方）"""
    def __init__(self, nx, ny, dx, dy):
        self.nx, self.ny = nx, ny
        self.dx, self.dy = dx, dy
        self.data = np.zeros((nx, ny))  # 场值
        self.x = np.linspace(0, nx*dx, nx)
        self.y = np.linspace(0, ny*dy, ny)
        self.X, self.Y = np.meshgrid(self.x, self.y)
    
    def laplacian(self):
        """五点差分 Laplace 算子"""
        lap = np.zeros_like(self.data)
        # 内部点
        lap[1:-1, 1:-1] = (
            self.data[2:, 1:-1] + self.data[:-2, 1:-1] +
            self.data[1:-1, 2:] + self.data[1:-1, :-2] -
            4 * self.data[1:-1, 1:-1]
        ) / (self.dx * self.dy)
        return lap
    
    def enforce_boundary(self, bc_type='dirichlet', value=0):
        """施加边界条件"""
        if bc_type == 'dirichlet':
            self.data[0, :] = value
            self.data[-1, :] = value
            self.data[:, 0] = value
            self.data[:, -1] = value
```

### 6.4 模式四：配置驱动（参数扫描必备）

```python
# config.py
CONFIG = {
    'system': {
        'n_particles': 100,
        'box_size': [10.0, 10.0, 10.0],
        'temperature': 300,
    },
    'potential': {
        'type': 'lennard_jones',
        'epsilon': 1.0,
        'sigma': 1.0,
        'cutoff': 2.5,
    },
    'simulation': {
        'dt': 0.001,
        'n_steps': 100000,
        'save_interval': 100,
        'seed': 42,
    },
    'output': {
        'directory': 'results/run_01/',
        'save_trajectory': True,
        'save_energy': True,
    }
}

# 使用
params = CONFIG['simulation']
dt = params['dt']
n_steps = params['n_steps']
```

---

## 7. 性能优化实战

### 7.1 性能瓶颈诊断（先测再优化！）

```python
import cProfile
import pstats

# 方法1：cProfile
cProfile.run('my_simulation.run(1000)', 'profile_stats')
p = pstats.Stats('profile_stats')
p.sort_stats('cumulative').print_stats(20)  # 显示最耗时的 20 个函数

# 方法2：IPython 内置
%prun my_simulation.run(1000)

# 方法3：逐行分析
# 安装：pip install line_profiler
# 然后在函数前加 @profile 装饰器
```

### 7.2 加速手段排序（按投入产出比）

| 手段 | 加速比 | 难度 | 何时用 |
|------|--------|------|--------|
| **向量化** | 10-100× | 低 | 始终 |
| **Numba @jit** | 10-200× | 极低 | 有 for 循环时 |
| **用对数据结构** | 2-10× | 中 | 大规模稀疏矩阵 |
| **NumPy 内置函数** | 2-5× | 低 | 避免自己写聚合 |
| **多进程** | N× (N=核心数) | 中 | 参数扫描 |
| **Cython** | 50-200× | 高 | Numba 不够用 |
| **GPU (CuPy/PyTorch)** | 100-500× | 高 | 大规模矩阵运算 |

### 7.3 Numba：一行装饰器，十倍加速

```python
from numba import jit, njit, prange

# 基本用法：加一行装饰器
@njit  # = @jit(nopython=True)，要求只能用 Numba 支持的类型
def compute_pairwise_forces(positions, eps=1.0, sigma=1.0):
    """计算 N 个粒子的 LJ 力（O(N²) 循环）"""
    N = len(positions)
    forces = np.zeros_like(positions)
    potential_energy = 0.0
    
    for i in range(N):
        for j in range(i + 1, N):
            dr = positions[j] - positions[i]
            r2 = dr[0]*dr[0] + dr[1]*dr[1] + dr[2]*dr[2]
            
            if r2 < 6.25:  # 截断半径内
                r2i = sigma*sigma / r2
                r6i = r2i * r2i * r2i
                ff = 48.0 * eps * r6i * (r6i - 0.5) / r2
                f = ff * dr
                forces[i] += f
                forces[j] -= f
                potential_energy += 4.0 * eps * r6i * (r6i - 1.0)
    
    return forces, potential_energy
# 第一次调用会编译（慢），之后和 C 一样快

# 并行 for 循环（多核加速）
@njit(parallel=True)
def compute_many_trajectories(initial_states, n_steps, dt):
    n_traj = len(initial_states)
    results = np.zeros((n_traj, n_steps, 3))
    
    for i in prange(n_traj):  # prange = 并行 range
        state = initial_states[i]
        for step in range(n_steps):
            state = rk4_step(state, dt)
            results[i, step] = state
    
    return results
```

### 7.4 常见加速技巧清单

```python
# ❌ 慢
for i in range(N):
    result[i] = np.cos(theta[i])

# ✅ 快：向量化
result = np.cos(theta)

# ❌ 慢：每次循环都创建新数组
for step in range(n):
    data = data + dt * rhs(data)  # 每次创建临时数组

# ✅ 快：原地更新
for step in range(n):
    np.add(data, dt * rhs(data), out=data)

# ❌ 慢：循环里 Python 求和
total = 0
for i in range(N):
    total += arr[i]

# ✅ 快
total = np.sum(arr)   # 或用 arr.sum()

# ❌ 慢：循环里 append
history = []
for step in range(n):
    history.append(state.copy())

# ✅ 快：预分配
history = np.zeros((n,) + state.shape)
for step in range(n):
    ...
    history[step] = state  # 直接写入，不 append
```

---

## 8. 调试与排错

### 8.1 仿真代码常见 Bug 清单

| 症状 | 可能原因 | 排查方法 |
|------|----------|----------|
| 结果全是 NaN | 除以0、步长太大、数值发散 | 打印中间值，二分法缩小步长 |
| 能量不守恒 | 辛结构破坏、用错积分器 | 换 Verlet / 检查力的计算 |
| 结果"看起来对"但不准确 | 一阶精度、CFL 不满足 | 做网格收敛性测试 |
| 程序越来越慢 | 隐性 O(N²)、内存泄漏 | 用 cProfile 找热点 |
| 随机种子固定但结果不同 | 某处用了未控制的随机 | 用 `np.random.seed()` 全局固定 |
| 并行结果和串行不一致 | 竞争条件、随机数不同步 | 串行验证通过后再并行化 |

### 8.2 数值验证的黄金法则

```python
def verify_convergence(simulator, resolutions=[16, 32, 64, 128, 256]):
    """
    网格收敛性验证：
    将网格分辨率加倍，解应趋于一致。
    误差随网格缩小的阶数应等于方法精度阶数。
    """
    results = []
    for N in resolutions:
        sim = simulator(N)
        sim.run()
        results.append(sim.get_result())
    
    # 计算相邻分辨率之间的差异
    errors = []
    for i in range(len(results) - 1):
        err = np.linalg.norm(results[i+1] - results[i]) / np.linalg.norm(results[i+1])
        errors.append(err)
    
    # 检查收敛阶
    # 如果是二阶方法，分辨率加倍 → 误差应减少约 4 倍
    for i in range(len(errors) - 1):
        order = np.log2(errors[i] / errors[i+1])
        print(f"分辨率 {resolutions[i]}→{resolutions[i+1]}, 收敛阶 ≈ {order:.2f}")
    
    return errors

def verify_energy_conservation(trajectory, dt):
    """验证能量守恒（哈密顿系统必备检查）"""
    energy = total_energy(trajectory)
    drift = (energy[-1] - energy[0]) / energy[0]
    std = np.std(energy) / np.mean(energy)
    print(f"能量漂移: {drift:.2e}")
    print(f"能量涨落/均值: {std:.2e}")
    # Verlet 算法：漂移应极小，涨落 ∝ dt²
```

### 8.3 防御性编程

```python
# 使用 assert 检查关键假设
def rk4_step(f, t, y, dt):
    assert dt > 0, f"时间步必须为正，得到 dt={dt}"
    assert np.all(np.isfinite(y)), "状态向量包含 NaN 或 Inf"
    
    k1 = f(t, y)
    k2 = f(t + dt/2, y + dt/2 * k1)
    k3 = f(t + dt/2, y + dt/2 * k2)
    k4 = f(t + dt, y + dt * k3)
    
    y_new = y + dt/6 * (k1 + 2*k2 + 2*k3 + k4)
    
    # 检查结果
    if not np.all(np.isfinite(y_new)):
        raise ValueError(f"在 t={t} 处 RK4 步产生非有限值，尝试减小 dt")
    
    return y_new

# 使用 logging 替代 print
import logging
logging.basicConfig(level=logging.INFO, 
                    format='%(asctime)s [%(levelname)s] %(message)s')

logger = logging.getLogger(__name__)
logger.info(f"开始仿真: dt={dt}, N={N}")
logger.debug(f"步骤 {step}: E={energy:.6f}")
logger.warning(f"能量偏差超过 1%！")
```

---

## 9. 速查表：30 个仿真高频操作

```python
# ===== 数组操作 =====
np.zeros((N, 3))                       # 创建 N×3 零数组（粒子坐标）
np.ones(N) * value                     # 全填充某值
np.linspace(0, L, Nx)                  # 生成一维网格
np.meshgrid(x, y, indexing='ij')       # 生成二维网格
arr.reshape(N, -1)                     # 重塑形状
np.concatenate([a, b], axis=0)         # 拼接数组

# ===== 数学运算 =====
np.sqrt(x**2 + y**2 + z**2)           # 向量的模
np.dot(a, b)                           # 点积
np.cross(a, b)                         # 叉积
np.linalg.norm(arr, axis=1)            # 批量求模
np.exp(-beta * energy)                 # Boltzmann 因子
np.where(condition, A, B)              # 条件选择

# ===== 随机 =====
np.random.seed(42)                     # 固定随机
np.random.uniform(low, high, N)        # 均匀分布
np.random.normal(0, 1, (N, 3))         # 正态分布坐标
np.random.choice(arr, size=N)          # 从数组中随机抽样

# ===== 统计 =====
np.mean(arr, axis=0)                   # 均值
np.std(arr)                            # 标准差
np.histogram(data, bins=50)            # 直方图
np.corrcoef(x, y)                      # 相关系数

# ===== 文件 IO =====
np.save('data.npy', arr)               # 保存 NumPy 数组（最快）
arr = np.load('data.npy')              # 加载
np.savetxt('data.csv', arr, delimiter=',')  # 保存文本
arr = np.loadtxt('data.csv', delimiter=',') # 加载文本

# ===== 时间 =====
import time
t0 = time.time()
# ... 你的代码 ...
elapsed = time.time() - t0
print(f"耗时: {elapsed:.2f}s")
```

---

## 10. 完整项目模板

```python
"""
仿真项目模板 —— 直接复制，填入你的物理即可运行
用法: python my_simulation.py
"""

import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp
from pathlib import Path
import json
from datetime import datetime

# ==================== 配置 ====================
CONFIG = {
    "physics": {
        "param1": 1.0,
        "param2": 0.5,
    },
    "numerics": {
        "dt": 0.01,
        "t_max": 10.0,
        "method": "RK45",
        "rtol": 1e-8,
        "atol": 1e-10,
    },
    "initial_condition": [1.0, 0.0],
    "output": {
        "save_dir": "results",
        "save_data": True,
        "save_fig": True,
        "dpi": 150,
    }
}


# ==================== 物理模型 ====================
def equations_of_motion(t, y, param1, param2):
    """
    在这里写你的运动方程
    y 是状态向量，返回 dy/dt
    """
    x, v = y  # 根据你的系统解包
    dxdt = v
    dvdt = -param1 * x - param2 * v  # 例：阻尼谐振子
    return [dxdt, dvdt]


# ==================== 仿真运行 ====================
def run_simulation(config):
    """运行仿真，返回结果"""
    cfg = config
    t_span = (0, cfg["numerics"]["t_max"])
    y0 = cfg["initial_condition"]
    args = (cfg["physics"]["param1"], cfg["physics"]["param2"])
    
    sol = solve_ivp(
        equations_of_motion,
        t_span,
        y0,
        args=args,
        method=cfg["numerics"]["method"],
        rtol=cfg["numerics"]["rtol"],
        atol=cfg["numerics"]["atol"],
        dense_output=True,
    )
    
    # 均匀采样输出
    dt_out = cfg["numerics"]["dt"]
    t_out = np.arange(0, cfg["numerics"]["t_max"], dt_out)
    y_out = sol.sol(t_out)
    
    return t_out, y_out


# ==================== 后处理与分析 ====================
def analyze_and_plot(t, y, config):
    """分析结果并绘图"""
    x, v = y[0], y[1]
    energy = 0.5 * v**2 + 0.5 * config["physics"]["param1"] * x**2
    
    fig, axes = plt.subplots(2, 2, figsize=(12, 8))
    
    # 时间序列
    axes[0, 0].plot(t, x, 'b-', lw=1, label='x(t)')
    axes[0, 0].plot(t, v, 'r--', lw=1, label='v(t)')
    axes[0, 0].set_xlabel('t'); axes[0, 0].legend(); axes[0, 0].grid(alpha=0.3)
    
    # 相图
    axes[0, 1].plot(x, v, 'k-', lw=0.5)
    axes[0, 1].set_xlabel('x'); axes[0, 1].set_ylabel('v')
    axes[0, 1].set_title('Phase Portrait')
    
    # 能量
    axes[1, 0].plot(t, energy, 'g-', lw=1)
    axes[1, 0].set_xlabel('t'); axes[1, 0].set_ylabel('E')
    axes[1, 0].set_title(f'Energy drift: {(energy[-1]-energy[0])/energy[0]:.2e}')
    axes[1, 0].grid(alpha=0.3)
    
    # 频谱
    from scipy.fft import fft, fftfreq
    dt = t[1] - t[0]
    spectrum = np.abs(fft(x))**2
    freqs = fftfreq(len(t), dt)
    positive = freqs > 0
    axes[1, 1].semilogy(freqs[positive], spectrum[positive], 'm-', lw=1)
    axes[1, 1].set_xlabel('f'); axes[1, 1].set_ylabel('Power')
    axes[1, 1].set_xlim(0, 5)
    
    plt.tight_layout()
    return fig


# ==================== 保存结果 ====================
def save_results(t, y, fig, config):
    """保存数据和图像"""
    save_dir = Path(config["output"]["save_dir"])
    timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
    run_dir = save_dir / f"run_{timestamp}"
    run_dir.mkdir(parents=True, exist_ok=True)
    
    # 保存配置
    with open(run_dir / "config.json", 'w') as f:
        json.dump(config, f, indent=2)
    
    # 保存数据
    np.savez(run_dir / "data.npz", t=t, y=y)
    
    # 保存图像
    fig.savefig(run_dir / "result.png", dpi=config["output"]["dpi"])
    
    print(f"结果已保存至: {run_dir}")
    return run_dir


# ==================== 主程序 ====================
def main():
    print("=" * 50)
    print("仿真开始")
    print("=" * 50)
    
    # 运行仿真
    t, y = run_simulation(CONFIG)
    print(f"仿真完成: {len(t)} 个时间步, t ∈ [{t[0]:.1f}, {t[-1]:.1f}]")
    
    # 分析绘图
    fig = analyze_and_plot(t, y, CONFIG)
    
    # 保存
    save_results(t, y, fig, CONFIG)
    
    plt.show()
    print("完成！")


if __name__ == "__main__":
    main()
```

---

## 附录：从本项目文件学仿真代码

阅读本项目以下文件，理解真实仿真项目的结构和写法：

| 文件 | 学到什么 |
|------|----------|
| `biot_savart_demo.py` | 物理公式→数值积分的完整过程 |
| `biot_savart_app.py` | 如何把仿真封装成交互式应用 |
| `biot_field_evolution.py` | ODE 求解器做时间演化 |
| `magnetic_field_visualizer.py` | 矢量场的 2D/3D 可视化 |
| `biot_to_maxwell_v2.py` | 从特殊定律到普遍定律的数值验证 |
| `solenoid_ampere_derivation.py` | 螺线管磁场与安培定理的数值计算 |
| `gui/main_window.py` | 仿真程序的 GUI 框架 |
| `utils/verification.py` | 数值结果的验证方法 |

**建议阅读顺序：** `biot_savart_demo.py` → `biot_field_evolution.py` → `magnetic_field_visualizer.py` → `biot_savart_app.py`

---

## 结语

**仿真的 Python 编程，核心就三句话：**

1. **用 NumPy 数组表达一切**——粒子坐标、场值、网格、历史记录
2. **向量化压倒循环**——能用 NumPy 内置函数的绝不写 Python for 循环；必须写循环的就加 `@njit`
3. **类来组织，函数来执行**——物理系统→类，时间推进→方法，分析绘图→独立函数

不要试图背下所有 API。记住这个速查表的章节标题，用的时候回来翻。写够三个完整的仿真项目之后，这些就会变成肌肉记忆。

*配合《物理仿真速成指南》一起看：那个讲"为什么"和"算什么"，这个讲"怎么写"。*