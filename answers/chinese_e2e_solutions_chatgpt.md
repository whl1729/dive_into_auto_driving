这几年国内自动驾驶（更准确地说是“高阶辅助驾驶”）的技术路线，正在快速从：

* 模块化（感知 → 预测 → 规划 → 控制）
  演进到：
* 端到端（End-to-End）
  再进一步演进到：
* 世界模型 / VLA（Vision-Language-Action）路线

目前中国头部玩家，大致可以分成 4 类：

| 公司   | 当前主路线              | 特点        |
| ---- | ------------------ | --------- |
| 华为   | 世界模型 + 端到端 + GOD网络 | 工程化最强     |
| 小鹏汽车 | 纯视觉端到端 + 大模型化      | 最接近 Tesla |
| 理想汽车 | VLM/VLA 驾驶大模型      | 最激进 AI 化  |
| 地平线  | 一段式端到端             | 强芯片+软硬协同  |
| 小米集团 | 借鉴小鹏/Tesla路线       | 快速追赶      |
| 蔚来   | NAD + 世界模型探索       | 保守演进      |

下面我按公司详细讲。

---

# 一、华为 ADS：世界模型 + GOD 网络 + PDP

## 1. 华为的核心思路

华为 ADS 2.0/3.0 的核心思想是：

> “神经网络负责理解世界，规则系统负责安全兜底。”

它不是完全纯端到端。

而是：

```text
传感器
 ↓
GOD 网络（通用障碍物检测）
 ↓
RCR / 道路拓扑推理
 ↓
PDP（预测决策规划）
 ↓
控制
```

ADS 3.0 开始进一步强化：

* 端到端神经网络
* 类人驾驶
* 世界模型能力
* 车位到车位

华为特别强调：

* “拟人化”
* “全国都能开”
* “复杂异形障碍物”

([地平线开发者社区][1])

---

## 2. GOD 网络是什么

GOD（General Obstacle Detection）：

本质上是：

> “不再依赖人工定义障碍物类别”

传统系统：

```text
car
truck
pedestrian
cone
...
```

华为：

```text
任何能影响驾驶的东西
```

包括：

* 石头
* 动物
* 掉落物
* 异形施工设备

这与 Tesla Occupancy Network 非常像。

---

## 3. 华为的特点

### 优势

#### （1）工程能力极强

华为最强的其实是：

* 数据闭环
* OTA
* 云训练
* 车端部署
* 软硬协同

这是传统 AI 公司难以比的。

---

#### （2）激光雷达 + 多传感器融合

华为目前仍然坚持：

* 激光雷达
* 毫米波
* 摄像头

不是 Tesla 那种纯视觉。

原因：

华为更强调：

```text
L2 量产安全性
```

而不是技术理想主义。

---

#### （3）规则系统仍然很多

虽然宣传“端到端”，但业内普遍认为：

```text
华为 = 神经网络 + 大量工程规则
```

这也是它当前量产表现很强的重要原因。

---

## 4. 华为相关论文/技术源头

华为公开论文不算特别多，但其路线与以下论文/技术高度相关：

### （1）Tesla Occupancy Network

这是全球端到端感知的重要转折点。

核心思想：

```text
不再检测目标
而是理解整个三维空间
```

论文：

* Tesla AI Day 2022
* Occupancy Networks

---

### （2）BEVFormer

Computer Vision 经典论文：

* BEVFormer (ECCV 2022)

核心：

```text
把多摄像头图像统一到鸟瞰图（BEV）
```

国内几乎所有智驾公司都受其影响。

论文：

* [https://arxiv.org/abs/2203.17270](https://arxiv.org/abs/2203.17270)

---

### （3）UniAD

这是中国自动驾驶领域影响极大的论文。

论文：

* UniAD: Planning-oriented Autonomous Driving
* [https://arxiv.org/abs/2212.10156](https://arxiv.org/abs/2212.10156)

核心思想：

```text
统一：
感知
预测
规划
```

很多国内公司都明显受 UniAD 影响。

---

# 二、小鹏：最像 Tesla 的中国公司

## 1. 小鹏的技术路线

小鹏汽车 是国内最早大规模推进：

```text
纯视觉 + 端到端
```

的公司之一。

其路线与 Tesla FSD v12 非常接近。

小鹏经历了：

```text
高精地图
→ 无图 NGP
→ XNet
→ XNGP
→ 端到端大模型
```

---

## 2. XNet 是什么

XNet 本质上是：

```text
大一统感知网络
```

以前：

* 车道线模型
* 红绿灯模型
* 障碍物模型

是分开的。

XNet：

```text
统一多任务网络
```

类似：

* BEVFormer
* Occupancy Network

路线。

---

## 3. 小鹏为何越来越像 Tesla

现在小鹏：

* 去高精地图
* 去激光雷达（部分车型）
* 强化纯视觉
* 强化数据驱动
* 强化大模型

Reddit 社区很多讨论认为：

小鹏正在从“激光雷达派”转向“Tesla 派”。 ([Reddit][2])

---

## 4. 小鹏相关论文

### （1）BEVFormer

直接影响极大。

---

### （2）UniAD

规划导向统一架构。

---

### （3）Tesla FSD v12 思想

虽然不是论文，但行业影响巨大：

核心：

```text
从“写规则”
变成“模仿人类”
```

---

### （4）Diffusion Policy 路线

最近小鹏很可能开始引入：

* diffusion trajectory
* generative planning

这也是全球趋势。

相关论文：

### DiffVLA

Artificial Intelligence

论文：

* DiffVLA
* [https://arxiv.org/abs/2505.19381](https://arxiv.org/abs/2505.19381)

([arXiv][3])

---

# 三、理想：最激进的 VLA 路线

## 1. 理想正在从“端到端”走向“司机大模型”

理想汽车 现在最核心的关键词：

```text
VLM / VLA
```

即：

```text
Vision-Language-Action
```

理想现在的目标已经不是：

```text
“自动驾驶”
```

而是：

```text
“AI Driver”
```

官方甚至明确提出：

```text
用 GPT 的方式做自动驾驶
```

([IT之家][4])

---

## 2. 理想路线的本质

传统端到端：

```text
图像
→ 轨迹
```

VLA：

```text
图像
+ 语言
+ 世界知识
→ 驾驶行为
```

例如：

```text
“前面公交车可能会停”
“外卖员可能突然横穿”
```

这是“认知驾驶”。

---

## 3. 理想为什么要搞 VLA

因为传统端到端有一个巨大问题：

```text
缺乏常识推理
```

例如：

* 警察手势
* 临时施工
* 学校门口
* 特殊社会规则

VLA 试图用：

```text
LLM 的世界知识
```

解决这个问题。

---

## 4. 理想相关论文

### （1）RT-2（Google DeepMind）

机器人/VLA 开山之作。

论文：

* RT-2: Vision-Language-Action Models
* [https://arxiv.org/abs/2307.15818](https://arxiv.org/abs/2307.15818)

核心：

```text
把机器人动作 token 化
```

这对汽车行业影响极大。

---

### （2）AutoVLA

这是自动驾驶 VLA 非常新的代表。

论文：

* AutoVLA
* [https://arxiv.org/abs/2506.13757](https://arxiv.org/abs/2506.13757)

([arXiv][5])

其核心：

```text
推理 + 轨迹生成
统一到一个 autoregressive model
```

---

### （3）DriveWorld-VLA

论文：

* DriveWorld-VLA
* [https://arxiv.org/abs/2602.06521](https://arxiv.org/abs/2602.06521)

核心：

```text
世界模型 + VLA
```

([arXiv][6])

这是目前最前沿方向。

---

# 四、地平线：一段式端到端

## 1. 地平线 HSD

地平线 的 HSD：

强调：

```text
一段式端到端
```

即：

```text
光子输入
→ 轨迹输出
```

官方明确这样描述。 ([地平线机器人][7])

---

## 2. 什么叫“一段式”

行业里很多“伪端到端”：

```text
感知网络
+
规划网络
+
规则模块
```

地平线强调：

```text
统一网络
```

减少：

* 信息损失
* 延迟
* 人工规则

---

## 3. 地平线最大的优势

其实不是算法。

而是：

```text
芯片 + 算法
```

它是国内少数：

```text
软硬协同
```

能力特别强的公司。

类似：

* Tesla
* NVIDIA

路线。

---

# 五、小米：快速追赶 Tesla/小鹏路线

小米集团 目前公开技术不如前几家多。

但整体路线明显是：

```text
学习 Tesla + 小鹏
```

特点：

* 强调端到端
* 强调数据闭环
* 强调 OTA
* 强调大模型

小米真正强的地方可能是：

```text
互联网工程能力
+
消费电子生态
```

而不是最前沿算法。

---

# 六、国内端到端技术的大趋势

现在整个中国自动驾驶行业正在经历：

---

## 第一阶段：模块化

```text
感知
→ 预测
→ 规划
```

代表：

* 传统 Mobileye
* 早期华为
* 早期小鹏

---

## 第二阶段：端到端

```text
图像
→ 轨迹
```

代表：

* Tesla FSD v12
* 小鹏 XNGP
* 地平线 HSD

---

## 第三阶段：VLA / 世界模型

```text
图像
+ 语言
+ 世界知识
→ 驾驶
```

代表：

* 理想
* 部分华为研究
* 学术界最新方向

---

# 七、目前真正的难点是什么

很多人误以为：

```text
自动驾驶难点是感知
```

其实现在最大的难点已经变成：

---

## 1. Long-tail（长尾场景）

例如：

* 警察指挥
* 事故现场
* 临时施工
* 行人博弈

---

## 2. 社会交互

真正困难的是：

```text
理解“人”
```

例如：

* 加塞意图
* 礼让
* 博弈
* 默契

---

## 3. 世界模型

未来趋势：

```text
车辆先“想象未来”
再决策
```

类似：

```text
AlphaGo 的 rollout
```

---

# 八、你可以重点阅读的论文（推荐顺序）

如果你想系统理解国内端到端自动驾驶的发展，我非常推荐：

| 论文              | 重要性   | 作用        |
| --------------- | ----- | --------- |
| BEVFormer       | ★★★★★ | BEV 感知基础  |
| UniAD           | ★★★★★ | 中国端到端核心论文 |
| Tesla Occupancy | ★★★★★ | 世界模型雏形    |
| RT-2            | ★★★★★ | VLA 开山    |
| DiffVLA         | ★★★★  | VLA+扩散    |
| AutoVLA         | ★★★★  | 推理+动作统一   |
| DriveWorld-VLA  | ★★★★  | 世界模型+VLA  |

---

相关链接：

* BEVFormer
  [https://arxiv.org/abs/2203.17270](https://arxiv.org/abs/2203.17270)

* UniAD
  [https://arxiv.org/abs/2212.10156](https://arxiv.org/abs/2212.10156)

* RT-2
  [https://arxiv.org/abs/2307.15818](https://arxiv.org/abs/2307.15818)

* DiffVLA
  [https://arxiv.org/abs/2505.19381](https://arxiv.org/abs/2505.19381)

* AutoVLA
  [https://arxiv.org/abs/2506.13757](https://arxiv.org/abs/2506.13757)

* DriveWorld-VLA
  [https://arxiv.org/abs/2602.06521](https://arxiv.org/abs/2602.06521)

如果你愿意，我还可以进一步讲：

1. 「端到端」到底在自动驾驶里意味着什么
2. Tesla FSD v12 为什么影响这么大
3. 国内公司为什么都开始搞 VLA
4. 世界模型（World Model）在自动驾驶中的作用
5. UniAD 为什么是中国自动驾驶论文里程碑
6. 扩散模型（Diffusion）为什么开始进入自动驾驶
7. 各家公司在数据闭环上的差异
8. 华为 vs Tesla vs 小鹏 的本质区别

[1]: https://developer.horizon.auto/blog/13259?utm_source=chatgpt.com "华为ADS智驾方案分析 - 地平线开发者社区"
[2]: https://www.reddit.com/r/Xpeng/comments/1m0bsp4?utm_source=chatgpt.com "Musings on Xpeng's recent development"
[3]: https://arxiv.org/abs/2505.19381?utm_source=chatgpt.com "DiffVLA: Vision-Language Guided Diffusion Planning for Autonomous Driving"
[4]: https://www.ithome.com/0/915/584.htm?utm_source=chatgpt.com "理想汽车 2025 辅助驾驶观察：VLA 模型实现认知涌现，加速向具身智能演进 - IT之家"
[5]: https://arxiv.org/abs/2506.13757?utm_source=chatgpt.com "AutoVLA: A Vision-Language-Action Model for End-to-End Autonomous Driving with Adaptive Reasoning and Reinforcement Fine-Tuning"
[6]: https://arxiv.org/abs/2602.06521?utm_source=chatgpt.com "DriveWorld-VLA: Unified Latent-Space World Modeling with Vision-Language-Action for Autonomous Driving"
[7]: https://www.horizon.auto/solutions/horizon-superdrive?utm_source=chatgpt.com "地平线SuperDrive_高阶智能驾驶_城区NOA-地平线HorizonRobotics"
