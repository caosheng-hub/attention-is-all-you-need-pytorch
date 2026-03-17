# Transformer 论文复现 | 《Attention Is All You Need》
🔥 基于PyTorch从零实现Google 2017年经典论文《Attention Is All You Need》，完整拆解并复现Transformer核心架构，无高层API封装，逐模块对应论文公式与设计逻辑，深入理解大模型基础架构核心原理。

## 📑 论文背景
《Attention Is All You Need》是深度学习领域里程碑式论文，首次提出纯注意力机制的Transformer架构，彻底替代了RNN类序列模型，成为后续BERT、GPT等所有大语言模型的基础架构。
本项目严格遵循论文设计，从零实现完整的Encoder-Decoder架构，拆解每一个核心模块，做到公式-代码-逻辑一一对应。

## ✨ 核心实现亮点
1. **全链路从零实现**：无transformers等高层API调用，从词嵌入、位置编码，到多头注意力、编码器/解码器、层归一化、残差连接，全模块手动实现，完全吃透底层逻辑
2. **严格对齐论文设计**：
   - 实现论文3.2节 **Scaled Dot-Product Attention** 与 **Multi-Head Attention**
   - 实现论文3.3节 **Encoder-Decoder** 完整堆叠架构（6层Encoder + 6层Decoder）
   - 实现论文3.4节 **Feed-Forward Networks** 前馈全连接层
   - 实现论文3.5节 **Positional Encoding** 正弦余弦位置编码
   - 完整实现Padding Mask与Sequence Mask（因果掩码）双掩码机制
3. **模块化工程设计**：代码高度解耦，每个模块独立封装，可单独调用、测试、二次修改，符合工业界代码规范
4. **开箱即用**：配套完整的单模块测试与全链路测试脚本，一键运行即可验证模型前向传播逻辑

## 📁 仓库结构
