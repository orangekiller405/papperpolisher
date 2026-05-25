# Paper Polisher: Hierarchical Academic Writing Policy System for Trae

> **Stop using generic AI polishing. Start applying specific Writing Policies.**

`Paper Polisher` 是一个**分层学术写作策略系统**。它专为计算机视觉（CV）及 AI 领域的科研人员设计，旨在将非母语或初稿论文转化为符合顶级会议（CVPR, ICCV, NeurIPS）和期刊（TPAMI, IJCV, Elsevier）审美的高信息密度论文。

## 🌟 核心理念：从 Prompt 到 Policy

传统的 AI 润色往往产生平庸且带有明显 AI 痕迹的文本。`Paper Polisher` 的核心在于**分层注入规则**：
1. **Global Policy**: 负责去 AI 化（Anti-AI）、冗余压缩和公式锁定。
2. **Section Policy**: 针对 Introduction、Method、Experiments 等不同章节应用不同的论证逻辑。
3. **Style Prior**: 注入特定 Venue 的修辞先验（如 CVPR 的直接、TPAMI 的严谨）。

## 🚀 核心功能

### 1. 全文编排模式 (Orchestrator Mode)
自动识别论文结构，并根据章节属性精准触发对应的 `.md` 策略文件，确保全文逻辑一致且风格地道。

### 2. 风格挖掘机 (Style Miner)
支持根据目标期刊（如 Elsevier EAAI）和关键词，自动搜索并提取该领域 SOTA 论文的修辞特征，动态构建风格库。

### 3. 去 AI 化引擎 (Anti-AI Engine)
严格限制 `robustness`, `leverage`, `significantly` 等 20+ 个 AI 常用词的滥用，强制使用更具技术感的表达。

### 4. 公式与逻辑锚定
在润色过程中物理锁定所有 LaTeX 公式、变量引用和引用文献，确保学术严谨性不受干扰。

## 📁 目录结构

```text
paper_polisher/
├── SKILL.md                # 核心路由与调度逻辑
├── prompts/                # 分章节写作策略
│   ├── global.md           # 全文通用规则
│   ├── intro.md            # 问题定义与洞察重构
│   ├── method.md           # 公式驱动的工程描述
│   └── experiment.md       # 深度分析导向策略
├── styles/                 # 顶会/顶刊风格先验
│   ├── cvpr.md
│   ├── tpami.md
│   └── elsevier_eaai.md    # 动态挖掘生成的风格
├── banned_patterns.yaml    # 禁用词库
└── rewrite_rules.yaml      # 核心重写规则
```

## 🛠️ 如何安装到 Trae

1. 在你的 Trae 项目根目录下创建 `.trae/skills/` 文件夹（如果不存在）。
2. 将 `paper_polisher` 文件夹整体放入 `.trae/skills/`。
3. 在 Trae 的 AI 聊天框中输入：`使用 paper_polisher 润色我的论文，目标是 [CVPR/TPAMI/Elsevier]`。

## 🛡️ 安全与隐私

- **本地存储**: 所有的 Policy 文件和策略逻辑均存储在你的本地 `.trae` 文件夹中。
- **数据流向**: 仅在调用 AI 翻译/润色时，当前段落会发送给模型提供商（如 Claude/Gemini），遵循企业级隐私协议，数据不会被用于训练公共模型。

## 📝 许可证

MIT License. 仅供学术交流使用。
