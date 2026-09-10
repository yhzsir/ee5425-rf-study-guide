[← 上一节：Module 7 Measurements](07-measurements.md) | [返回首页](../README.md)

# 8. 推荐学习节奏（12周计划）

| 周次 | 内容 | 目标 |
|---|---|---|
| 1 | 课前准备（复数/相量/电路基础）+ Module 1 | 建立RF思维模式 |
| 2-3 | Module 2：传输线方程、反射系数、Smith圆图规则 | 能独立读圆图、算VSWR |
| 4-5 | Module 3：L型/λ4/单支节/双支节匹配 | 能独立设计一个匹配网络并验算 |
| 6 | Module 4：S参数 | 能计算增益/回波损耗dB值，理解S参数意义 |
| 7-8 | Module 5上：小信号放大器设计+增益圆 | 能做单向化最大增益设计 |
| 9 | Module 5下：LNA噪声匹配 + 偏置网络 | 理解噪声/增益折中 |
| 10 | Module 6：稳定性K因子+稳定圆 | 能判断放大器是否稳定 |
| 10-11 | Module 6：振荡器 | 理解起振/稳态条件 |
| 11 | Module 5(功率放大器补充) | 了解PA效率/线性度概念 |
| 12 | Module 7：测量 + 全课程串讲复习 | 用做过的习题自测，查漏补缺 |

> 建议：每学完一个Module，立即找对应的Worksheet/Tutorial PDF动手做题，
> 光看讲义记不住，Smith圆图必须亲手画（可以先用软件如Keysight ADS或
> 在线Smith Chart工具核对手算结果）。

---

# 9. 推荐工具与外部资源

## 软件工具
- **Smith圆图**（手算/画图）：可打印本课程提供的 `Black and White Smith Chart.pdf` 反复练习
- **在线Smith圆图计算器**：如 `www.will-kelsey.com/smith_chart/`，用于快速验证手算结果
- **ADS (Advanced Design System)** 或 **Keysight/NI AWR Microwave Office**：
  RF仿真软件，用于验证匹配网络、放大器设计（如果学校有license，强烈建议用起来）
- **QUCS / QUCS-S**：开源微波仿真软件，免费替代方案

## 参考教材（网络知识补充推荐）
- David M. Pozar, *Microwave Engineering*（微波工程"圣经"，Smith圆图、S参数、
  放大器/振荡器设计章节非常系统）
- Guillermo Gonzalez, *Microwave Transistor Amplifiers: Analysis and Design*
  （放大器设计部分讲得非常细，和本课程Module 5高度契合）
- Reinhold Ludwig & Gene Bogdanov, *RF Circuit Design: Theory and Applications*
  （入门友好，适合零基础）

## 视频资源
- YouTube搜索 "Smith Chart tutorial"、"RF amplifier design gain circle"、
  "stability circle RF amplifier" 等关键词，配合看动画演示理解圆图旋转方向

---

# 10. 考试/作业注意事项

1. **单位和归一化**：几乎所有计算题第一步是"除以Z0归一化"，
   最后一步是"乘回Z0反归一化"，丢这一步是最常见的失分点。
2. **圆图作图题**：保持标注清晰（标出出发点、旋转方向、终点、对应的电长度λ），
   即使最终数值有小误差，清晰的作图过程通常仍能拿到大部分分数。
3. **dB换算**：功率比用10log，电压/电流/S参数（波的比值）用20log，别混。
4. **公式默写**：K因子、Δ、Γ、VSWR、G_T等核心公式建议直接背下来，
   考试时间往往不够从头推导。
5. **善用Worksheet和Tutorial**：这些是老师精心设计的例题，通常和考试题型高度相似，
   建议至少刷两遍（第一遍跟着做，第二遍自己独立重做验证是否真掌握）。

---

*本学习指南整理自 EE5425 课程官方大纲 PDF 目录结构，并结合公开射频工程知识补充讲解。
如发现内容与老师课堂实际内容有出入，请以老师课件和现场讲解为准。*

[← 上一节：Module 7 Measurements](07-measurements.md) | [返回首页](../README.md)
