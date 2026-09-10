[← 上一节：Module 1 Introduction](01-introduction.md) | [返回首页](../README.md) | 下一节：[Module 3 — Matching →](03-matching.md)

# Module 2 — Transmission Lines and Smith Chart

**对应文件**：
- `EE5425_CityUHK-DG_2_FoRCE_TL&SC_2026ArS0.pdf`（主讲义）
- `EE5425_CityUHK-DG_2_FoRCE_Tutorial on Terminated Transmission Lines.pdf`
- `EE5425_CityUHK-DG_2 FoRCE Worksheet 1 Transmission Lines.pdf`
- `Black and White Smith Chart.pdf` / `Colour Admittance on Impedance Smith Chart.pdf`（圆图工具）

这是**全课程最重要的基础模块**，Smith圆图会贯穿到Module 3、5、6。

## 2.1 传输线方程
传输线用分布参数模型：单位长度电阻R'、电感L'、电导G'、电容C'。
电报方程（Telegrapher's Equations）推出电压/电流沿线满足波动方程，
解为正向波+反向波的叠加：

```
V(z) = V+ e^(-γz) + V- e^(+γz)
I(z) = (V+/Z0) e^(-γz) - (V-/Z0) e^(+γz)
```

其中：
- γ = α + jβ 为传播常数（α衰减常数，β相位常数）
- **特性阻抗** Z0 = √[(R'+jωL')/(G'+jωC')]，无损线时 Z0 = √(L'/C')

## 2.2 反射系数 Γ
在终端负载 Z_L 处：

```
Γ_L = (Z_L - Z0) / (Z_L + Z0)
```

距负载 d 处的反射系数（无损线）：

```
Γ(d) = Γ_L · e^(-j2βd)
```

**关键直觉**：相位里的"2"来自"入射+反射"的**往返路程**，
所以移动 d=λ/2 时相位转一整圈360°，圆图上回到原位置（阻抗周期性 λ/2 重复）。

## 2.3 输入阻抗公式（终端接任意负载）

```
Z_in(d) = Z0 · [Z_L + jZ0·tan(βd)] / [Z0 + jZ_L·tan(βd)]
```

特殊情形（记住这4个，考试常考）：
| 终端 | 输入阻抗（长度d） |
|---|---|
| 短路 Z_L=0 | Z_in = jZ0·tan(βd) → 感性(d<λ/4) |
| 开路 Z_L=∞ | Z_in = -jZ0·cot(βd) → 容性(d<λ/4) |
| 匹配 Z_L=Z0 | Z_in = Z0（无论多长都不变） |
| d=λ/4 | Z_in = Z0²/Z_L（阻抗反演器/变换器） |
| d=λ/2 | Z_in = Z_L（周期重复） |

## 2.4 驻波比 VSWR
```
VSWR = (1+|Γ|)/(1-|Γ|)，  |Γ| = (VSWR-1)/(VSWR+1)
```
物理意义：入射波与反射波叠加形成驻波，波腹(V_max)与波节(V_min)之比。
VSWR=1 完全匹配，VSWR=∞ 全反射（短路/开路）。

## 2.5 Smith圆图（本课程灵魂工具）
Smith圆图是把归一化阻抗平面 z=Z/Z0 通过双线性变换 Γ=(z-1)/(z+1) 映射到
单位圆内的Γ平面上的一张"阻抗-反射系数"对照图。

**必须记住的圆图规则**：
1. 圆图中心 = 匹配点（Γ=0，z=1）
2. 圆图最右点 = 开路（z=∞），最左点 = 短路（z=0）
3. 上半圆 = 感性（+jX），下半圆 = 容性（−jX）
4. 顺时针转 = 朝向发生器（toward generator，即沿传输线往信号源方向移动）
5. 逆时针转 = 朝向负载（toward load）
6. 转一圈360° = 移动 λ/2；转180° = 移动 λ/4
7. 圆图外圈刻度通常标"wavelengths toward generator/load"，直接读弧长对应的电长度

**导纳圆图（Y-Smith Chart）**：把阻抗圆图旋转180°即为导纳图（因为 z→1/z 对应
Smith圆图上点旋转180°，对应课程文件 `Colour Admittance on Impedance Smith Chart.pdf`）。
在做并联匹配（并联电感/电容/短截线）时必须切换到导纳图或使用ZY合一圆图。

## 常见误区
- 分不清"朝向负载"和"朝向发生器"的圆图刻度方向 —— 建议用课程文件
  `Get Your Directions Right_r2.pdf`（Module 3附带但和圆图方向强相关）反复练习。
- 用阻抗图直接读并联元件的导纳值（必须先转换到导纳图或用倒易对称点）。

## 自测题
1. 一条50Ω无损线，终端接100Ω电阻，求Γ_L和VSWR。
2. 在Smith圆图上，从z=1+j1出发，顺时针转90°，落在什么位置？对应移动了多少个λ？
3. 短路短截线长度为λ/8，其输入阻抗是感性还是容性？数值是多少（用Z0表示）？

---
下一节：[Module 3 — Smith Chart, ELL and TRL Matching →](03-matching.md)
