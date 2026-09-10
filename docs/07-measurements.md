[← 上一节：Module 6 Stability and Oscillators](06-stability-oscillators.md) | [返回首页](../README.md) | 下一节：[学习计划与资源 →](08-study-plan.md)

# Module 7 — Measurements

**对应文件**：
- `EE5425_CityUHK-DG_7_Measurements_2026Ar0.pdf`
- `EE5425_CityUHK-DG_7_Network Analyzer Display.pdf`

## 📺 推荐视频
- [Understanding VNA Calibration Basics（Rohde & Schwarz）](https://www.youtube.com/watch?v=bLfbg2p7PaE) — SOLT校准原理与步骤（12分钟）
- [Mini-Circuits eVNA Vector Network Analyzer - SOLT Calibration](https://www.everythingrf.com/videos/details/4572-mini-circuits-evna-vector-network-analyzer-solt-calibration) — 全2端口SOLT校准实操演示
- [Understanding Spectrum Analyzers – Noise Figure（Rohde & Schwarz）](https://www.everythingrf.com/videos/details/4921-understanding-spectrum-analyzers-noise-figure) — 用频谱分析仪做Y-factor噪声系数测量的简明介绍

## 🎓 老师的话：这一章把前六章"落地"到实验室
学到这里，你已经掌握了大量理论工具（阻抗、S参数、匹配、增益、稳定性），
但工程师最终要面对的问题是——**这些量要怎么被实际测出来？测出来的数据
有多可信？** 这正是Module 7要回答的问题。很多同学以为测量只是"操作仪器"，
是纯粹的实验技能，与考试无关；但实际上VNA校准（SOLT）背后的数学
（消除仪器本身误差项）和Y-factor噪声测量的推导，本身就是对前面知识的
一次很好的复习和检验——如果你能看懂"为什么校准要用Open/Short/Load/Thru
四种标准件"，说明你已经把反射系数和S参数的概念内化了。

**给自学者、也是给未来工程师的建议**：如果条件允许，一定要找机会摸一次
真实的VNA（哪怕是学校实验室的旧仪器），亲手做一次SOLT校准、看着
Smith圆图上的S11轨迹随频率移动——课本上的抽象公式，在你亲眼看到
仪器屏幕上圆图轨迹跳动的那一刻，才会真正变成你的直觉。

## 7.1 常用RF测量仪器
| 仪器 | 测量内容 |
|---|---|
| 频谱分析仪 (Spectrum Analyzer) | 信号在频域的功率分布，可看谐波、杂散、调制信号带宽 |
| 矢量网络分析仪 (VNA, Vector Network Analyzer) | S参数（幅度+相位），阻抗、增益、隔离度 |
| 驻波仪/滑动线 (Slotted Line) | 早期测量驻波比的经典方法，现已较少用，但原理仍是考点 |
| 功率计 (Power Meter) | 绝对功率测量 |

## 7.2 网络分析仪（VNA）测量原理
- VNA内部通过定向耦合器分离入射波(a)和反射波(b)，直接计算S参数
- **校准（Calibration）非常关键**：SOLT校准（Short-Open-Load-Thru）用已知标准件
  消除仪器和电缆本身的系统误差，把"参考面"移到待测器件（DUT）端口
- Smith圆图显示模式：VNA可以直接把S11实时显示在Smith圆图上，
  这也是为什么Smith圆图在实验室实测中依然是最直观的工具

## 7.3 常见测量与显示格式
- Log Magnitude（dB）：常用于看增益/损耗随频率变化
- Smith Chart 格式：看阻抗匹配情况
- Polar格式：看反射系数的幅度和相位
- 群时延（Group Delay）：dφ/dω，衡量相位线性度/信号失真

## 7.4 噪声系数测量
- Y-factor法：用已知噪声源（ENR已知）分别测"噪声源开/关"时的输出噪声功率比值Y，
  反推被测器件（DUT）的噪声系数

## 常见误区
- 忘记校准或校准面选错，导致测量结果包含线缆/连接器误差
- 混淆"回波损耗(dB, 正值表示好)"和"反射系数(线性值，0~1)"的正负号与含义

## 例题讲解

**例题1：Y-factor法计算噪声系数**

用一个ENR（Excess Noise Ratio）= 15dB的噪声源测量DUT，测得噪声源"开"时输出功率
P_on = -40dBm，"关"时输出功率 P_off = -46dBm。求DUT的噪声系数NF(dB)。

*解：*

先算Y因子（线性功率比）：
```
P_on(dBm)=-40 → 转线性(mW): 10^(-40/10)=10^-4 = 0.0001 mW
P_off(dBm)=-46 → 10^(-46/10)=10^-4.6 ≈ 0.0000251 mW
Y = P_on/P_off = 0.0001/0.0000251 ≈ 3.98
```
ENR转线性：
```
ENR(线性) = 10^(15/10) = 10^1.5 ≈ 31.62
```
噪声系数公式（Y-factor法）：
```
F = ENR / (Y-1) = 31.62 / (3.98-1) = 31.62/2.98 ≈ 10.61
```
转dB：
```
NF(dB) = 10log(10.61) ≈ 10.26 dB
```

> **考试技巧**：Y-factor法核心思路是"用已知的噪声源提供的额外噪声（ENR）作为标尺，
> 通过开/关两次功率测量算出增益和固有噪声的组合效应"。做题时最容易出错的地方是
> dB与线性值的混用——ENR、NF最终都用dB表示，但公式 F=ENR/(Y-1) 中所有量必须先转成
> **线性值**代入，算完F后再取10log转回dB。

**例题2：回波损耗与Smith圆图轨迹判断**

VNA测得某天线在工作频段内 S11 从 -2dB 变化到 -15dB。分别说明这两个端点对应的
匹配情况，以及在Smith圆图上大致的轨迹特征。

*解：*
```
S11=-2dB → |S11| = 10^(-2/20) = 10^(-0.1) ≈ 0.794 → VSWR=(1+0.794)/(1-0.794)≈8.7（严重失配）
S11=-15dB → |S11| = 10^(-15/20) = 10^(-0.75) ≈ 0.178 → VSWR=(1+0.178)/(1-0.178)≈1.43（较好匹配）
```
- **回波损耗越负（数值越大），匹配越好**；-2dB说明几乎全反射，天线在该频点严重失配；
  -15dB是常见的"可接受"匹配门槛（工程上常用-10dB作为及格线）。
- 在Smith圆图上：|S11|=0.794对应的轨迹点**非常靠近圆图外边缘**（半径0.794，接近1）；
  |S11|=0.178对应的点则**靠近圆图中心**（半径0.178，接近0）。
  若整个扫频轨迹大部分贴着圆图边缘，说明该天线在此频段内普遍失配严重，
  需要重新设计匹配网络或检查天线本身谐振点是否偏移。

> **考试技巧**：记住回波损耗(RL, dB)和反射系数模|Γ|的关系 RL=-20log|Γ|，
> 这是本模块和Module 4（S参数）、Module 2（VSWR）之间的贯穿公式，
> 三个量（RL、|Γ|、VSWR）之间可以互相换算，是考试高频考点。

## 自测题
**1.** 简述VNA的SOLT校准的作用和基本步骤。

<details><summary>点击查看答案</summary>

**作用**：消除VNA仪器本身、电缆、连接器带来的系统性测量误差
（方向性误差、源失配误差、频响误差等），使测得的S参数真正反映
被测器件（DUT）本身的特性，而不是"仪器+DUT"混合的结果。
**基本步骤**：依次接入四种已知标准件——**S**hort（短路）、
**O**pen（开路）、**L**oad（匹配负载，通常50Ω）、**T**hru（直通），
VNA用这些已知标准的测量结果反推出误差模型的各项误差系数，
后续测量DUT时自动扣除这些误差，得到校准后的"干净"S参数。

</details>

**2.** 在Smith圆图显示模式下，如果测得的S11轨迹几乎贴着圆图边缘，说明什么问题？

<details><summary>点击查看答案</summary>

Smith圆图边缘对应|Γ|=1，即反射系数模接近1，几乎全反射，
说明被测器件（如天线）在该频段**严重失配**——绝大部分入射功率
被反射回来，几乎没有功率被有效吸收/辐射出去。需要重新设计
匹配网络，或检查器件本身的谐振点是否偏移到了别的频率。

</details>

**3.** 简述Y-factor法测量噪声系数的原理。

<details><summary>点击查看答案</summary>

用一个已知噪声等效比（ENR）的噪声源，分别在"开启（热态，输出较高噪声
功率）"和"关闭（冷态，输出较低噪声功率，近似环境温度对应的热噪声）"
两种状态下，测量DUT输出端的噪声功率，记为N_hot和N_cold，
定义 Y = N_hot/N_cold（Y-factor）。结合已知的ENR值，
可以反解出DUT自身贡献的噪声系数（噪声系数越低的DUT，
Y值理论上应该越大，因为DUT自身引入的额外噪声更少）。

</details>

**4.** ENR=20dB的噪声源，测得Y=6，求DUT的噪声系数(dB)。

<details><summary>点击查看答案</summary>

先把ENR转成线性值：ENR(线性) = 10^(20/10) = 100
Y-factor法基本公式（假设Tcold=T0=290K的标准情况）：

```
F(线性) = ENR / (Y-1) = 100/(6-1) = 100/5 = 20
NF(dB) = 10log(20) ≈ 13.01 dB
```

</details>

---
下一节：[学习计划与推荐资源 →](08-study-plan.md)
