---
layout: post
title: "Differential Review"
date: 2023-05-18
---
# 椭圆型方程（17分）

$$ -(U_{xx}+U_{yy}) = f_{x,y} \tag{1}
$$

## 五点差分格式

□网格差分:

$$ - \frac{ {U_{k+1,j}} - {2U_{k,j}} + {U_{k-1,j}}} {h^2_x} - \frac{ {U_{k,j+1}} - {2U_{k,j}} + {U_{l,j-1}}} {h^2_y} = f_{k,j} \tag{2}
$$

假设$h_x = h_y = h$:

$$ \frac{4U_{k,j} - U_{k+1,j} -U_{k+1,j} - U_{k,j+1} -U_{k,j-1}}{h^2} = f_{k,j} \tag{3}
$$

## 九点差分格式（2选1）

◇网格差分:

假设$h_x = h_y = h$:

$$ \frac{4U_{k,j} - U_{k+1,j+1} -U_{k-1,j+1} - U_{k+1,j-1} -U_{k-1,j-1}}{2h^2} = f_{k,j} \tag{4}
$$

九点差分：
$$ \frac{2}{3} \cdot (3) + \frac{1}{3} \cdot (4) = f_{k,j} \tag{5}$$

## Fourier稳定性分析

五点差分：（条件稳定）
令 $ \lambda^k \cdot e^{i(\alpha k + \beta j)} = U^k_j$, 带入（3）,其中$f_{i,j} = 0$, 得到:

$$ λ^k e^{i(αk+βj)} = \frac{1}{4} \cdot (λ^k e^{i(α(k+1)+βj)} + λ^k e^{i(α(k-1)+βj)} + λ^k e^{i(αk+β(j+1))} + λ^k e^{i(αk+β(j-1))}) \tag{6}
$$

化简：

$$ λ = \frac{1}{4}(e^{i\alpha} + e^{-i\alpha} + e^{i\beta} + e^{-i\beta}) \tag{7}
$$

继续：

$$ λ = \cos(α) + \cos(β) \tag{8}
$$

结果：

$|λ|<2$ 时，格式稳定。

## 极值原理（离散型）（五点差分格式为例）

对于内部网格点：
$$U_{k,j} = \text{min or max} \implies U_{k \pm 1,j} < U_{k,j} \quad \text{and} \quad U_{k,j \pm 1} < U_{k,j} \quad (\text{for minimum}) \tag{8}
$$

$$U_{k,j} = \text{min or max} \implies U_{k \pm 1,j} > U_{k,j} \quad \text{and} \quad U_{k,j \pm 1} > U_{k,j} \quad (\text{for maximum}) \tag{9}
$$

对于边界网格点：
$$ U_{i,j} = \text{min or max} \implies U_{i\pm1,j} < U_{i,j} \quad (\text{for minimum}) \tag{11}
$$

$$ U_{i,j} = \text{min or max} \implies U_{i\pm1,j} > U_{i,j} \quad (\text{for maximum}) \tag{12}
$$

## 证明极值在边界上或者恒为常数

# 热传导方程（33分）

## 一维

$$ U_t = a \cdot U_{xx} \tag{1}
$$

### 古典显格式

$$ \frac{U^{k+1}_j - U^k_j}{\tau} = a \cdot \frac{U^k_{j+1} - 2U^k_j +U^k_{j-1}}{h^2_x} \tag{2}
$$

令:

$$ r = \frac{a \cdot \tau}{h^2_x} \tag{3}
$$

整理得：

$$ U^{k+1}_{j} = r \cdot U^{k}_{j+1} +(1 - 2r) \cdot U^{k}_{j} + r \cdot U^{k}_{j-1} \tag{4}
$$

### 古典隐格式

$$ \frac{U^{k+1}_{j} - U^{k}_{j}}{\tau} = a \cdot \frac{U^{k+1}_{j+1} - 2U^{k+1}_{j} +U^{k+1}_{j-1}}{h^2_x} \tag{5}
$$

令:

$$ r = \frac{a \cdot \tau}{h^2_x} \tag{6}
$$

整理得：

$$ U^{k}_{j} = -r \cdot U^{k+1}_{j+1} +(1 + 2r) \cdot U^{k+1}_{j} - r \cdot U^{k+1}_{j-1} \tag{7}
$$

### CN格式（3选1）

$$ \frac{U^{k+1}_{j} - U^{k}_{j}}{\tau} = \frac{a}{2} \cdot (\frac{U^{k}_{j+1} - 2U^{k}_{j} +U^{k}_{j-1}}{h^2_x} + \frac{U^{k+1}_{j+1} - 2U^{k+1}_{j} +U^{k+1}_{j-1}}{h^2_x}) \tag{8}
$$

令:

$$ r = \frac{a \cdot \tau}{h^2_x} \tag{9}
$$

整理省略。

### Fourier稳定性分析

令 $ \lambda^k \cdot e^{ijh} = U^k_j$ 分别带入不同格式中，结果：

显格式：（$ L^2$ 稳定必要条件为 $ |λ|<=1$ , 即 $ r<= \frac{1}{2}$）

$$ λ = 1 - 4r \sin^{2} \frac{h}{2} \tag{10}
$$

隐格式：(无条件稳定)

$$ λ = \frac{1}{1 + 4r \sin^{2} \frac{h}{2}} \tag{11}
$$

CN格式：（无条件 $ L^2$ 稳定）

$$ λ = \frac{1 - 2r \sin^{2} \frac{h}{2}}{1 + 2r \sin^{2} \frac{h}{2}} \tag{12}
$$
## 二维

$$ U^t=a \cdot (U_{xx}+U_{yy}) \tag{1}
$$

### PR格式

将方程 (1) 中的时间导数离散化为：

$$ \frac{U^{t+1}-U^t}{\tau}=a\cdot(U_{xx}^{t+\frac{1}{2}}+U_{yy}^{t+\frac{1}{2}}) \tag{2}
$$

对于 x 方向的离散化，将 $U_{xx}^{t+1/2}$ 进行隐式差分：

$$ \frac{U_{k,j}^{t+\frac{1}{2}}-U_{k,j}^t}{\frac{\tau}{2}} = a\cdot\frac{U_{k+1,j}^{t+\frac{1}{2}}-2U_{k,j}^{t+\frac{1}{2}}+U_{k-1,j}^{t+\frac{1}{2}}}{h_x^2} + a\cdot\frac{U_{k,j+1}^t-2U_{k,j}^{t+\frac{1}{2}}+U_{k,j-1}^t}{h_y^2} \tag{3}
$$

对于 y 方向的离散化，将 $U_{yy}^{t+1/2}$ 进行隐式差分：

$$ \frac{U_{k,j}^{t+1}-U_{k,j}^{t+\frac{1}{2}}}{\frac{\tau}{2}} = a\cdot\frac{U_{k+1,j}^{t+1}-2U_{k,j}^{t+\frac{1}{2}}+U_{k-1,j}^{t+1}}{h_x^2} + a\cdot\frac{U_{k,j+1}^{t+\frac{1}{2}}-2U_{k,j}^{t+1}+U_{k,j-1}^{t+1}}{h_y^2} \tag{4}
$$

### LOD格式

令

$$ {r = \frac{a \cdot \tau}{h_x^2}},{v = \frac{a \cdot \tau}{h_y^2}} \tag{5}
$$

将方程 (1) 中的时间导数离散化为：

$$ \frac{U^{t+1}-U^t}{\tau} = a\cdot(U_{xx}^{t+1}+U_{yy}^{t+1}) \tag{6}
$$

对于 x 方向的离散化：

$$ U_{k,j}^{t+1} = \frac{1}{4}(U_{k+1,j}^{t+1}+U_{k-1,j}^{t+1}+U_{k,j+1}^t+U_{k,j-1}^t) - \frac{r}{2}(U_{k+1,j}^{t+1}-2U_{k,j}^{t+1}+U_{k-1,j}^{t+1}) - \frac{v}{2}(U_{k,j+1}^t-2U_{k,j}^t+U_{k,j-1}^t) \tag{7}
$$

对于 y 方向的离散化：

$$ U_{k,j}^{t+1} = \frac{1}{4}(U_{k+1,j}^t+U_{k-1,j}^t+U_{k,j+1}^{t+1}+U_{k,j-1}^{t+1}) - \frac{r}{2}(U_{k+1,j}^t-2U_{k,j}^t+U_{k-1,j}^t) - \frac{v}{2}(U_{k,j+1}^{t+1}-2U_{k,j}^{t+1}+U_{k,j-1}^{t+1}) \tag{8}
$$

### 稳定性分析（差分算子）

设:差分算子为$ \mathcal{L}$

PR格式：(条件稳定)

离散化方程:

$$ \frac{U^{t+1}-U^t}{\tau}=a\cdot \mathcal{L} (U^{t+\frac{1}{2}}) \tag{9}
$$

LOD格式：

离散化方程：

$$ \frac{U^{t+1}-U^t}{\tau}=a\cdot \mathcal{L} (U^{t}) - \frac{a \cdot \tau}{2} \cdot \mathcal{L}^2(U^t) \tag{10}
$$
## 三维

### LOD格式

### 稳定性分析（差分算子）

# 双曲型方程（30分）

## 一维

$$ U_t + a \cdot U_x = 0 \tag{1}
$$

### 迎风格式

当$ a>0$时：

$$ \frac{U^{k+1}_j-U ^k _j} {\tau} = a \cdot \frac{U^k_j-U^{k}_{j-1}} {h_x} \tag{2}
$$

当$ a<0$时：

$$ \frac{U^{k+1}_{j}-U^k_j}{\tau} = a \cdot \frac{U^{k}_{j+1}-U^{k}_j}{h_x} \tag{3}
$$

### LF格式

令：

$$ r=\frac{a \cdot \tau}{h_x} \tag{4}
$$

$$U_j^{k+1} = \frac{1}{2} (U_{j-1}^k + U_{j+1}^k) - \frac{r}{2} (U_{j+1}^k - U_{j-1}^k) \tag{5}
$$

### B-W格式

$$U_j^{k+1} = U_j^k - r(U_j^k - U_{j-1}^k) \tag{6}
$$

### LW格式

$$U_j^{k+1} = U_j^k - \frac{r}{2} (U_{j+1}^k - U_{j-1}^k) + \frac{r^2}{2} (U_{j+1}^k - 2U_j^k + U_{j-1}^k) \tag{7}
$$

### Fourier稳定性分析

## 二维

$$ U_t + a \cdot U_x +b \cdot U_y = 0 \tag{1}
$$

### 迎风格式

令：

$$ {r=\frac{a \cdot \tau}{h_x}} , {v=\frac{a \cdot \tau}{h_y}}
$$

$$ U_{k,j}^{t+1} = U_{k,j}^t - r \cdot (U_{k,j}^t - U_{k-1,j}^t)  - v \cdot (U_{k,j}^t - U_{k,j-1}^t) \tag{2}
$$

### 显式中心差分格式（$L^{\infty}$稳定）

$$ U_{k,j}^{t+1} = U_{k,j}^t - r \cdot \frac{U_{k+1,j}^t - U_{k-1,j}^t}{2}  - v \cdot \frac{U_{k,j+1}^t - U_{k,j-1}^t}{2} \tag{3}
$$

### 最大值定理条件

### Fourier稳定性分析

# 波动型方程（20分）

## 一维

$$ U_{tt} = a^2 \cdot U_{xx} \tag{1}
$$

### 古典显格式

$$ \frac{U^{k+1}_j - 2U^k_j +U^{k-1}_j}{\tau ^ 2} = a^2 \cdot \frac{U^k_{j+1} - 2U^k_{j} + U^k_{j-1}}{h_x^2} \tag{2}
$$

令：

$$ r = \frac{a^2 \cdot \tau^2}{h^2_x}
$$

整理得：

$$ U^{k+1}_j = 2U^k_j - U^{k-1}_j + r(U^k_{j+1} - 2U^k_j+ U^k_{j-1}) \tag{3}
$$

### 古典隐格式

$$ \frac{U^{k+1}_j - 2U^k_j +U^{k-1}_j}{\tau ^ 2} = a^2 \cdot \frac{U^{k+1}_{j+1} - 2U^{k+1}_{j} + U^{k+1}_{j-1}}{h_x^2} \tag{2}
$$

令：

$$ r = \frac{a^2 \cdot \tau^2}{h^2_x}
$$

整理得：

$$ U^{k-1}_j = 2U^k_j + 2U^{k+1}_j - r(U^{k+1}_{j+1} -2U^{k+1}_j + U^{k+1}_{j-1}) \tag{3}
$$

### 加权格式

对（2）时间上加权平均：

$$ θ \cdot U^{k+1}_{j} + (1-2θ) \cdot U^{k}_{j} + θ \cdot U^{k-1}_{j} = r \cdot (U^{k}_{j+1} - 2U^{k}_{j} + U^{k}_{j-1})
$$

### 稳定性分析

## 二维

$$ U_{tt} = a^2 \cdot (U_{xx}+U_{yy}) \tag{1}
$$

### ADI格式

令：

$$ r = \frac{a^2 \cdot \tau}{h^2_x} , v = \frac{a^2 \cdot \tau}{h^2_y}
$$
将二维波动方程（式(1)）在 $x$ 方向和 $y$ 方向上分别进行半隐式离散化：

$$ 2U_{tt}^{k+\frac{1}{2}} = r \cdot U_{xx}^{n+\frac{1}{2}} + v \cdot U_{yy}^{n} \tag{2}
$$

$$ U_{tt}^{k+1} = r \cdot U_{xx}^{n+\frac{1}{2}} + v \cdot U_{yy}^{n+1} \tag{3} 
$$