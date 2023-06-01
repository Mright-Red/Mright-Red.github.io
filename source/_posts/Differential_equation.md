---
layout: post
title: "Differential equation"
date: 2023-06-02
---
# 椭圆型方程（17分）

$$ -(U_{xx}+U_{yy}) = f_{x,y} 
$$

**（1）五点差分格式**

□网格差分:

$$ - \frac{ {U_{k+1,j}} - {2U_{k,j}} + {U_{k-1,j}}} {h^2_x} - \frac{ {U_{k,j+1}} - {2U_{k,j}} + {U_{k,j-1}}} {h^2_y} = f_{k,j} 
$$

**（2）最大值定理证明**

$$
L△U=f ≥ 0
$$

内部不能取最小值，由极值原理可知，边界取最小值。

$$
L△U=f ≤ 0
$$

内部不能取最大值，由极值原理可知，边界取最大值。

# 热传导方程（33分）

## 一维

$$ U_t = a \cdot U_{xx}
$$

**（1）古典隐格式**

$$ \frac{U^{k+1}_{j} - U^{k}_{j}}{\tau} = a \cdot \frac{U^{k+1}_{j+1} - 2U^{k+1}_{j} +U^{k+1}_{j-1}}{h^2_x}
$$

**（2）Fourier分析**（无条件稳定）

令 $ U^k_j = \lambda^k \cdot e^{ijh} $ 带入格式中，结果：

$$ λ = \frac{1}{1 + 4r \sin^{2} \frac{h}{2}}
$$

无条件稳定

##二维

$$ U_t=a \cdot (U_{xx}+U_{yy})
$$

**（1）PR格式**

对于 x 方向的离散化：

$$ \frac{U_{k,j}^{t+\frac{1}{2}}-U_{k,j}^t}{\frac{\tau}{2}} = a\cdot\frac{U_{k+1,j}^{t+\frac{1}{2}}-2U_{k,j}^{t+\frac{1}{2}}+U_{k-1,j}^{t+\frac{1}{2}}}{h_x^2} + a\cdot\frac{U_{k,j+1}^t-2U_{k,j}^{t+\frac{1}{2}}+U_{k,j-1}^t}{h_y^2}
$$

对于 y 方向的离散化：

$$ \frac{U_{k,j}^{t+1}-U_{k,j}^{t+\frac{1}{2}}}{\frac{\tau}{2}} = a\cdot\frac{U_{k+1,j}^{t+1}-2U_{k,j}^{t+\frac{1}{2}}+U_{k-1,j}^{t+1}}{h_x^2} + a\cdot\frac{U_{k,j+1}^{t+\frac{1}{2}}-2U_{k,j}^{t+1}+U_{k,j-1}^{t+1}}{h_y^2}
$$

**（2）差分算子稳定性分析**（$h_x = h_y = h$）
令：

$$ {r = \frac{a \cdot \tau}{h^2}}
$$

$$ (I - \frac{r}{2}δ^2_x)(I - \frac{r}{2}δ^2_y) \cdot U^{t+1}_{kj} = (I + \frac{r}{2}δ^2_x)(I + \frac{r}{2}δ^2_y) \cdot U^{t}_{kj}
$$

令 $ U^{t}_{kj} = \lambda^t \cdot e^{i(σ_1+σ_2)h} $ 带入格式中，结果：

$$ λ = \frac{(I + \frac{r}{2}δ^2_x)(I + \frac{r}{2}δ^2_y)}{(I - \frac{r}{2}δ^2_x)(I - \frac{r}{2}δ^2_y)} = \frac{(1 - 4r \sin^{2} \frac{σ_1h}{2})(1 - 4r \sin^{2} \frac{σ_2h}{2})}{(1 + 4r \sin^{2} \frac{σ_1h}{2})(1 + 4r \sin^{2} \frac{σ_2h}{2})}
$$

无条件稳定

# 双曲型方程（30分）

## 一维

$$ U_t + a \cdot U_x = 0 
$$

**（1）LF格式(条件稳定 r<1)**

令：

$$ r=\frac{a \cdot \tau}{h_x} 
$$

$$U_j^{k+1} = \frac{1}{2} (U_{j-1}^k + U_{j+1}^k) - \frac{r}{2} (U_{j+1}^k - U_{j-1}^k) 
$$

**（2）Fourier分析**

令 $ U^{k}_{j} = \lambda^k \cdot e^{ijh} $ 带入格式中，结果：

$$
λ = \frac{1}{2}(e^{-ih}+e^{ih}) - \frac{r}{2}(e^{ih}-e^{-ih})
$$

$$
λ = \frac{1}{2}(2 \cosh) - \frac{r}{2}(2i \sinh)
$$

$$ λ = \cosh - i\sinh \cdot r$$

若满足稳定条件
$$ 
|λ| ≤ 1
$$

对应

$$
r ≤ 1
$$

## 二维（对流扩散方程）(f(x,t) = 0)

$$
U_t + a \cdot U_x = c \cdot U_{xx} + f(x,t)
$$

**（1）中心显格式**

$$
\frac{U^{k+1}_{j} - U^{k}_{j}} {\tau} + a \cdot \frac{U^{k}_{j+1} - U^{k}_{j-1}}{2h} = c \cdot \frac{U^{k}_{j+1} - U^{k}_{j} + U^{k}_{j-1}}{h^2}
$$

**（2）稳定性分析**

令
$$ 
u = \frac{a \tau} {2h} , v = \frac{c \tau}{h^2}
$$

$$ 
U^{k+1}_{j} = (u - \frac{v}{2}) U^{k}_{j+1} + (1 - 2u)U^k_j + (u + \frac{v}{2}) U^{k}_{j-1}
$$

当$|v| < 2u < 1 $时，满足最大值定理，$ L^∞$稳定。

Fourier分析结果是$L^2$稳定。

引入网格的Peclet数······

# 波动方程（20分）

## 一维

$$ U_{tt} = a^2 \cdot U_{xx} 
$$

**（1）古典显格式**

$$ \frac{U^{k+1}_j - 2U^k_j +U^{k-1}_j}{\tau ^ 2} = a^2 \cdot \frac{U^k_{j+1} - 2U^k_{j} + U^k_{j-1}}{h_x^2}
$$

令：

$$ r = \frac{a^2 \cdot \tau^2}{h^2_x}
$$

整理得：

$$ U^{k+1}_j = 2U^k_j - U^{k-1}_j + r(U^k_{j+1} - 2U^k_j+ U^k_{j-1})
$$

**（2）Fourier分析**

令 $ U^{k}_{j} = \lambda^k \cdot e^{ijh} $ 带入格式中，结果：

$$
λ^2 + \frac{1} {λ} = 2 - 4r \sin^2\frac{h}{2}
$$

若满足稳定条件

$$
|λ^2|≤1
$$

对应

$$
r≤1
$$