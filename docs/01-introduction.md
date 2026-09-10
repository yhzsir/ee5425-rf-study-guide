[← 上一节：课前准备](00-prerequisites.md) | [返回首页](../README.md) | 下一节：[Module 2 — Transmission Lines →](02-transmission-lines.md)

# Module 1 — Introduction to RF Engineering

**对应文件**：`CityUHK-DG_EE5425_1_FoRCE_Introduction_2026ArCL_Sr1.pdf`

## 学习目标
理解RF工程的应用背景、频段划分、以及为什么RF电路设计与低频/数字电路设计方法完全不同。

## 核心知识点
1. **频谱划分**：
   - HF (3-30MHz)、VHF (30-300MHz)、UHF (300MHz-3GHz)、
     微波 Microwave (3-30GHz)、毫米波 mmWave (30-300GHz)
   - 常见应用：Wi-Fi (2.4/5/6GHz)、蓝牙(2.4GHz)、5G Sub-6/mmWave、GPS(1.5GHz)、雷达
2. **为什么需要专门的RF理论**：
   - 高频下，寄生电感/电容不可忽略，一颗电阻在GHz下可能表现得像个LC谐振电路
   - 信号在导线上是"传播"而非"瞬间到达"，存在反射、驻波
   - 功率的传输效率（阻抗匹配）比电压幅度更重要
3. **RF系统框图**：天线 → 匹配网络 → LNA(低噪放) → 混频器 → 中频放大 → ADC（接收链）；
   反过来是发射链（DAC → 上变频 → 功率放大器PA → 匹配 → 天线）
4. **关键设计指标先导概念**：增益（Gain）、噪声系数（NF）、线性度（P1dB, IP3）、
   阻抗匹配（VSWR/回波损耗）——这些会在后续模块逐一深入。

## 常见误区
- 误以为RF就是"高频版的模拟电路"，其实思维方式完全不同：低频关心电压/电流大小，
  RF更关心**功率的传输和反射**。

## 自测题
1. 说出3个你日常使用的RF应用及其大致工作频段
2. 解释为什么手机天线设计要考虑传输线效应，而普通LED电路不用考虑

---
下一节：[Module 2 — Transmission Lines and Smith Chart →](02-transmission-lines.md)
