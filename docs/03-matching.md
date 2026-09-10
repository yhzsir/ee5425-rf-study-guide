[← 上一节：Module 2 Transmission Lines](02-transmission-lines.md) | [返回首页](../README.md) | 下一节：[Module 4 — S-Parameters →](04-s-parameters.md)

# Module 3 — Smith Chart, ELL and TRL Matching

**对应文件**：
- `EE5425_CityUHK-DG_3_FoRCE_ELL&PI&TAP&SS&DS_2020Ar0.pdf`（L型/Pi型/Tap/单双支节匹配全集）
- `Tutorial on Smith Chart and Ell Matching.pdf`
- `Tutorial on Smith Chart and Transmission Line Matching.pdf`
- `Tutorial on More Transmission Line Matching.pdf`
- `Single Stub Matching Example.pdf` / `4 Ways Single Stub Matching Example.pdf`
- `Get the right ELL_r2.pdf`（如何选对L型匹配拓扑）
- `Worksheet 2 Impedance Matching.pdf`

## 学习目标
掌握**阻抗匹配**的核心技术——把任意负载阻抗变换到系统特性阻抗（通常50Ω），
使反射系数Γ=0，实现最大功率传输、消除驻波。

## 3.1 为什么要匹配
- 失配会造成反射，反射功率浪费、可能损坏功放、引起驻波导致电压/电流局部过高
- 匹配的目标：Γ_in = 0，即把负载"变换"到中心点

## 3.2 L型（ELL）匹配网络
用两个电抗元件（L或C）组成"L"形网络，是最简单的匹配拓扑。

**设计口诀（Get the right ELL）**：
- 若归一化负载电阻 r_L > 1（负载在圆图"电阻大于1"的区域外），
  先并联一个元件把它拉到 r=1 圆上，再串联一个元件消去剩余电抗
- 若 r_L < 1，则反过来：先串联元件把它移到 g=1（导纳圆）上，再并联消去电纳
- **判断用电感还是电容**：看你要在圆图上顺时针还是逆时针移动到目标点
  - 串联电感：沿等R圆顺时针（增加+jX）
  - 串联电容：沿等R圆逆时针（增加-jX）
  - 并联电感：沿等G圆逆时针（增加-jB）
  - 并联电容：沿等G圆顺时针（增加+jB）

> 记忆技巧：串联元件在阻抗图上移动，并联元件必须切到导纳图（或ZY圆图）上移动。

## 3.3 四分之一波长变换器（Quarter-wave Transformer）
只能匹配**纯电阻**负载：

```
Z0' = √(Z0 · R_L)
```

其中 Z0' 是变换段的特性阻抗。若负载有电抗，需先用一段传输线转到纯阻性点
（在Smith圆图上找到与实轴的交点）再接λ/4线。

## 3.4 单支节匹配（Single Stub Matching）
用一段**串联传输线** + 一段**并联短截线**（开路或短路）实现匹配，两个自由变量：
1. 串联线长度 d：把负载沿圆图旋转，使其落在 g=1 （导纳=1的圆）上
2. 短截线长度 l：抵消此时的电纳 jB

短截线可选短路或开路，通常短路短截线更常用（开路端在微带上有辐射/边缘电容误差）。
**注意**：单支节匹配通常有两个解（沿g=1圆有两个交点），对应课程文件
"4 Ways Single Stub Matching Example" 展示了短路/开路×两个交点=4种组合。

## 3.5 双支节匹配（Double Stub Matching）
当支节位置固定（如器件间距固定，不能任意选d）时使用，用两个位置固定、
长度可调的短截线实现匹配。图解法比单支节复杂，需要"旋转辅助圆"（auxiliary circle）。
—— 若课程覆盖到此，请重点看 `ELL&PI&TAP&SS&DS` 讲义中的 DS 部分图解步骤。

## 3.6 Pi型、T型（Tap）匹配
用于需要宽带匹配或同时做阻抗变换+滤波（如兼顾谐波抑制）的场合，
本质是L型网络的级联/组合，Q值（品质因数）决定带宽。

## 常见误区
- 忘记先判断负载在圆图上落在哪个区域（r>1 or r<1），导致L网络拓扑选错
- 单位混淆：忘记先做归一化（除以Z0）再上圆图，匹配完成后忘记反归一化算出实际元件值
- 短截线用错开路/短路（微带电路中，短路短截线要打过孔via，工艺上有时更愿意用开路）

## 自测题
1. 负载 Z_L = 25 - j30 Ω（Z0=50Ω），设计一个L型网络将其匹配到50Ω，说明选用的元件类型和拓扑。
2. 用λ/4变换器匹配75Ω电阻负载到50Ω系统，求变换段特性阻抗。
3. 解释为何单支节匹配一般有两个解，工程上如何选择（提示：短截线越短越好，带宽越宽）。

---
下一节：[Module 4 — S-Parameters →](04-s-parameters.md)
