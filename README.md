# 🚀 Transformer 从零实现（PyTorch | 论文级复现）

> 📄 论文复现：《Attention Is All You Need》
> 🧠 关键词：Transformer / Attention / NLP / 深度学习

---

## 📌 项目简介

本项目基于 PyTorch **从零实现 Transformer 架构**，完整复现论文核心组件，不依赖高级封装（如 `nn.Transformer`），适用于：

* 深入理解 Transformer 原理
* 面试展示深度学习能力
* NLP / 大模型方向基础项目

---

## 🧠 模型核心思想

传统模型（RNN / LSTM）的问题：

* ❌ 无法并行计算
* ❌ 长距离依赖难建模

Transformer解决方案：

👉 完全基于 Attention：

```text
Attention is All You Need
```

---

## 🏗️ 模型架构

### 🔷 整体结构

```text
        ┌───────────────┐
        │   Input Text   │
        └──────┬────────┘
               ↓
     Embedding + PosEncoding
               ↓
        ┌───────────────┐
        │   Encoder × N │
        └──────┬────────┘
               ↓
        ┌───────────────┐
        │   Decoder × N │◄──── target + mask
        └──────┬────────┘
               ↓
        Linear + Softmax
               ↓
           Output
```

## 📂 项目结构（工程化拆分）

.
├── models/                    # 🧠 模型核心代码
│   ├── __init__.py
│   ├── dm01_input.py          # 📥 Embedding + Position Encoding
│   ├── dm02_encoder.py        # 🔷 Encoder（Multi-Head Attention + FFN）
│   ├── dm03_decoder.py        # 🔁 Decoder（Masked + Cross Attention）
│   ├── dm04_generator.py      # 🎯 输出层（Linear + Softmax）
│   └── dm05_transformer.py    # 🔗 Transformer总结构
│
├── demo.py                    # 🚀 模型运行入口（forward测试）
├── requirements.txt          # 📦 依赖环境
├── .gitignore
├── LICENSE
└── README.md
```

---

## 🔍 模块设计解析（重点）

### 1️⃣ 输入层设计（Embedding + 位置编码）

📁 `dm01_input.py`

👉 设计亮点：

* Embedding输出乘以 √d_model（论文细节还原） 
* 使用 register_buffer 存储位置编码（工程规范） 

✔ 提升模型稳定性
✔ 避免参与梯度更新

---

### 2️⃣ Encoder 设计

📁 `dm02_encoder.py`

每层结构：

```text
Input
 ↓
Multi-Head Attention
 ↓
Add & LayerNorm
 ↓
Feed Forward
 ↓
Add & LayerNorm
```

👉 工程亮点：

* 模块解耦（Attention / FFN独立）
* 支持堆叠（N层Encoder）

---

### 3️⃣ Decoder 设计

📁 `dm03_decoder.py`

相比Encoder多了：

👉 **Masked Attention + Cross Attention**

```text
Masked Self-Attn
      ↓
Encoder-Decoder Attn
      ↓
Feed Forward
```

✔ 防止信息泄露（语言模型关键点）
✔ 学习对齐关系（翻译核心）

---

### 4️⃣ Generator 输出层

📁 `dm04_generator.py`

```python
Linear → log_softmax
```

👉 输出：

* 每个token的概率分布
* shape = `[batch, seq_len, vocab_size]`

实现：

* 使用 `log_softmax` 提升数值稳定性 

---

### 5️⃣ Transformer 总装

📁 `dm05_transformer.py`

完整流程：

```text
source → Encoder → memory
target → Decoder → output
output → Generator → 概率分布
```

👉 forward流程：

* embedding
* encoder
* decoder
* generator

实现清晰模块化设计 

---

## 🧪 快速运行

```bash
python demo.py
```

---

## 📊 输出示例

```text
Transformer模型结构:
...

最终输出:
shape = [2, 6, 2000]
```

---

## ⚙️ 超参数（论文对齐）

| 参数      | 值    |
| ------- | ---- |
| d_model | 512  |
| heads   | 8    |
| N（层数）   | 6    |
| d_ff    | 1024 |
| dropout | 0.1  |

---

## 🧩 工程设计亮点

### ⭐ 1. 模块化设计

* Encoder / Decoder 解耦
* Attention 可复用
* 易扩展 Transformer变种

---

### ⭐ 2. 高可读性代码结构

* 文件职责单一
* 符合深度学习工程规范
* 易Debug / 易扩展

---

### ⭐ 3. 论文细节还原

✔ √d_model scaling
✔ sinusoidal position encoding
✔ multi-head attention
✔ mask机制

---

### ⭐ 4. 可扩展性

轻松扩展：

* BERT（Encoder-only）
* GPT（Decoder-only）
* Vision Transformer

---
