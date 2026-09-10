[← 上一节：Module 6 Stability and Oscillators](06-stability-oscillators.md) | [返回首页](../README.md) | 下一节：[学习计划与资源 →](08-study-plan.md)

# Module 7 — Measurements

**对应文件**：
- `EE5425_CityUHK-DG_7_Measurements_2026Ar0.pdf`
- `EE5425_CityUHK-DG_7_Network Analyzer Display.pdf`

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

## 自测题
1. 简述VNA的SOLT校准的作用和基本步骤。
2. 在Smith圆图显示模式下，如果测得的S11轨迹几乎贴着圆图边缘，说明什么问题？
3. 简述Y-factor法测量噪声系数的原理。

---
下一节：[学习计划与推荐资源 →](08-study-plan.md)
