# 学路 (Xuelu) AI 导师 Skill v2.0

> **诊断优先 · 有教无类** —— 一个定义 AI 导师“教学行为层”的轻量级开源技能包。

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-2.0.0-green.svg)](https://github.com/wumohongyuan/xuelu-skill)
[![Coze](https://img.shields.io/badge/deploy-Coze-ff69b4)](https://www.coze.cn)

---

## 📖 目录
1. [项目定位与理念](#-项目定位与理念)
2. [核心教学流程](#-核心教学流程)
3. [核心特性](#-核心特性)
4. [快速开始](#-快速开始)
5. [API 接入（开发者）](#-api-接入开发者)
6. [许可证与贡献](#-许可证与贡献)

---

## 🧠 项目定位与理念

### 学路（Xuelu）是什么？
学路不是一个提供“标准答案”的 AI 助手，而是一套**定义教学行为的轻量级协议**。它通过一段约 280 字的系统提示词（System Prompt），将通用 AI 模型转化为一位 **“诊断优先”** 的私人导师。

### 它解决什么问题？
传统 AI 倾向于“有问必答”。但教育心理学表明，**直接给出答案无法建立真正的理解**。
学路的核心洞察是：**在教之前，先诊断。** 它不追求“讲完”，而是追求学生“真正掌握”。

---

## 🔄 核心教学流程

学路遵循一条清晰的教学闭环：

1. **接收问题**：学生提出学习需求。
2. **主动探测**：通过出题或开放式问题，精准评估真实水平。
3. **选择模式**：根据诊断结果，自动适配 **零基础 / 普通 / 进阶 / 自动** 四种模式。
4. **最小教学单元**：每次只教一个最需要学的概念（一个例子 + 一个类比 + 一个练习）。
5. **检查掌握信号**：提出验证问题，确认是否理解。
   - 理解 → 推进到下一个概念
   - 未理解 → 触发降级策略
6. **智能降级**：同一概念连续不懂时，按顺序执行 **换角度 → 补前置知识 → 建议换方向**。

---

## ✨ 核心特性

- **双模式入口**：**快速了解**（3-5 句核心解释） / **完整诊断**（系统教学）——既能查资料，也能深度学习。
- **诊断优先**：主动出题或开放式提问，避免“对牛弹琴”。
- **四模式分层**：零基础（通俗类比） / 普通（方法步骤） / 进阶（推导边界） / 自动（自适应）。
- **知识边界校验**：对于不确定的事实，AI 会主动声明“我记忆中是这样”，并建议交叉验证。
- **极简部署**：System Prompt 仅 280 字，指令清晰无冲突。支持一键复制粘贴，或在 Coze 平台 5 分钟零代码部署。

---

## 🚀 快速开始

### 方式一：直接复制 Prompt 使用（个人/团队）

将下方 **System Prompt** 完整复制，粘贴到 DeepSeek、ChatGPT、Kimi 等 AI 平台的新对话中，即可激活“学路”导师：

> 🔗 **核心 Prompt 内容**：请查阅 [`XUELU_SKILL_v2.0.md`](https://github.com/wumohongyuan/xuelu-skill/blob/main/XUELU_SKILL_v2.0.md)

**核心指令速查：**

| 你说的话 | 学路做什么 |
|---------|----------|
| `快速了解一下：xxx` | 快速模式：3-5 句核心解释 |
| `我想学 xxx` | 完整诊断：先测水平，再分模式教学 |
| `我的进度` | 自然语言总结当前学习状态 |

### 方式二：零代码嵌入网站（推荐 Coze ⭐）

1. 访问 [Coze 官网](https://www.coze.cn) 注册（完全免费）
2. 创建 Bot → 在“人设与回复逻辑”中粘贴上方 System Prompt
3. 模型选择 **DeepSeek**（免费且中文最佳）
4. 发布 → 选择“嵌入网站” → 复制 `iframe` 代码

```html
<iframe
  src="https://www.coze.cn/embed/你的BotID"
  width="400" height="600" frameborder="0"
  style="position:fixed; bottom:20px; right:20px;
         border-radius:16px; box-shadow:0 4px 20px rgba(0,0,0,0.15);
         max-width:100vw;">
</iframe>
🔌 API 接入（开发者）
如果你有自己的后端，可以使用 DeepSeek 或 OpenAI 兼容接口调用学路。

推荐 API 提供商
提供商	免费额度	价格	注册
DeepSeek	注册送 500 万 token	￥1/百万 token	platform.deepseek.com
通义千问	新用户送 200 万 token	免费额度足够	dashscope.aliyun.com
Python 示例
python
from openai import OpenAI

client = OpenAI(
    api_key="你的DeepSeek密钥",          # ← 替换
    base_url="https://api.deepseek.com",
)

SYSTEM_PROMPT = """（粘贴 v2.0 的完整 System Prompt）"""

def ask_xuelu(user_message: str) -> str:
    response = client.chat.completions.create(
        model="deepseek-chat",
        messages=[
            {"role": "system", "content": SYSTEM_PROMPT},
            {"role": "user", "content": user_message},
        ],
        temperature=0.7,
        max_tokens=1000,
    )
    return response.choices[0].message.content
📜 许可证与贡献
核心资产说明
本项目核心资产是一段精心设计的 System Prompt，而非传统代码库。因此，它的贡献方式不是“提 PR 修代码”，而是 “提 Issue 修 Prompt”。

贡献指南
反馈教学错误：如果你在使用中发现 AI 存在事实错误，请在 Issues 提交对话记录。

优化 Prompt：如果你觉得指令不够清晰，欢迎 Fork 并提交 Pull Request。

分享案例：欢迎在 Discussions 分享你的使用故事。

许可证
MIT License © 2026 — 允许自由修改和商用，需保留作者署名。

💬 开源寄语
学路不是一套“知识大全”，而是一套 “教学引导程序”。它可能犯错，但希望开源社区的力量能让它越来越“懂”学习者。

如果你觉得这个方向有价值，欢迎点亮 ⭐ Star，让更多人看到它。😊
