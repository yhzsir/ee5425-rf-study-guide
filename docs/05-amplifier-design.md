[← 上一节：Module 4 S-Parameters](04-s-parameters.md) | [返回首页](../README.md) | 下一节：[Module 6 — Stability and Oscillators →](06-stability-oscillators.md)

# Module 5 — Amplifier Design

**对应文件**（数量最多，是本课程的应用核心）：
- `EE5425_CityUHK-DG_5_FoRCE_AMP_2026Ar0.pdf`（主讲义：放大器设计理论）
- `EE5425_CityUHK-DG_5a_FoRCE_ZP_YP_2026Ar0.pdf`（Z参数/Y参数辅助）
- `Tutorial on Microstrip and Amplifier Gains.pdf`
- `Tutorial on Amplifier Design.pdf`（5_2, 5S, 5_3 supplement 共3份不同角度）
- `Worksheet Small Signal Amplifier Design.pdf`
- `Worksheet Bias network.pdf`（偏置电路设计）
- `EE5425_CityUHK-DG_8_FoRCE_POWERAMP_2026B_Simplified_S.pdf` + Tutorial on Power Amplifiers（功率放大器，进阶）

## 5.1 小信号放大器设计流程
1. **选晶体管**，获取其S参数（在工作频点、工作偏置下）
2. **稳定性检查**（见Module 6，K因子），确保不会自激振荡
3. **画增益圆（Gain Circles）**：在Smith圆图上画出定增益轨迹，
   帮助在增益与匹配复杂度之间取舍
4. **设计输入/输出匹配网络**（用Module 3的方法），使源阻抗/负载阻抗
   变换到晶体管所需的最佳阻抗
5. **设计偏置网络（Bias Network）**：给晶体管提供合适的直流工作点，
   同时RF信号不能泄漏进直流电源（用RF choke电感和去耦电容隔离）

## 5.2 功率增益的几种定义（重点公式，考试常考）
- **Transducer Gain G_T**：实际负载得到的功率 / 信号源能提供的最大功率（最常用，
  综合考虑了输入失配和输出失配）
- **Power Gain G_P**：负载得到的功率 / 网络输入端实际吸收的功率（不考虑输入失配）
- **Available Gain G_A**：网络能提供的最大功率 / 信号源能提供的最大功率

```
G_T = [(1-|Γs|²)/|1-Γin·Γs|²] · |S21|² · [(1-|ΓL|²)/|1-S22·ΓL|²]
```
（Γs为源反射系数，ΓL为负载反射系数，Γin为放大器输入端看进去的反射系数）

**单向化假设（Unilateral，S12≈0）** 下公式简化为：
```
G_T,U = Gs · G0 · GL
Gs = (1-|Γs|²)/|1-S11Γs|²,  G0=|S21|²,  GL=(1-|ΓL|²)/|1-S22ΓL|²
```
这是初学者最先掌握的简化设计方法：分别做输入、输出的"共轭匹配"，
Γs=S11*，ΓL=S22*，可得最大单向功率增益 G_T,U,max。

## 5.3 低噪声放大器（LNA）设计
- 目标：在满足一定增益的前提下**最小化噪声系数NF**
- 噪声系数圆（Noise Figure Circles）：在Smith圆图上画出等NF轨迹，
  与增益圆叠加，在两者之间找折中点（LNA设计通常不能同时兼顾最小噪声匹配
  和最大增益匹配，因为最佳噪声源阻抗Γ_opt通常≠共轭匹配点S11*）
- Friis公式（级联噪声系数，前级增益越高，后级噪声贡献越小）：
```
F_total = F1 + (F2-1)/G1 + (F3-1)/(G1·G2) + ...
```
—— 这说明**第一级LNA的噪声系数和增益直接决定整个接收链的噪声性能**，
这也是为什么LNA要尽量靠近天线放置。

## 5.4 偏置网络设计要点
- RF Choke（高值电感）：在直流通路上，对RF信号呈现高阻抗，隔离RF不进电源
- 旁路电容（Bypass/Decoupling Capacitor）：为RF信号提供交流接地路径
- 常见拓扑：有源偏置（用电流镜/反馈稳定工作点）vs 无源偏置（电阻分压，简单但受温漂影响大）

## 5.5 微带线相关（放大器物理实现）
放大器的匹配网络在实际PCB/MMIC上常用微带线（microstrip）实现短截线/变换线段，
需要用到：
- 特性阻抗计算（依赖 W/h, ε_r）
- 有效介电常数 ε_eff 和微带波长 λ_g
- 微带损耗（导体损耗、介质损耗、辐射损耗）

## 5.6 功率放大器（Power Amplifier, PA）简介（进阶模块8内容）
- 与小信号放大器不同，PA工作在大信号状态，需要考虑：
  - 效率（Efficiency）：η = P_out/P_DC，功率附加效率 PAE = (P_out-P_in)/P_DC
  - 工作类别（Class A/B/AB/C）：导通角不同，效率与线性度的折中
  - 1dB压缩点(P1dB)、三阶交调点(IP3)——非线性失真指标
  - 负载牵引（Load-pull）技术：实验寻找最佳负载阻抗（不是简单共轭匹配）

## 常见误区
- 把"共轭匹配（Conjugate Match）"和"最小噪声匹配"混为一谈——二者在LNA设计中通常不重合
- 忽略偏置网络对RF性能的影响，认为偏置只是"直流的事"

## 自测题
1. 已知某晶体管S11=0.3∠140°, S22=0.4∠-60°, S21=3∠60°, S12≈0（单向化），求最大单向功率增益(dB)。
2. 解释为什么LNA设计中最佳噪声匹配点和最大增益匹配点通常不是同一个Γs。
3. 画出一个基本的RF放大器偏置网络示意图，标出RF choke和旁路电容位置。

---
下一节：[Module 6 — Stability and Oscillators →](06-stability-oscillators.md)
