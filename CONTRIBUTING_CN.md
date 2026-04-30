# 如何贡献 AIRP

感谢您有兴趣为 AI 人民币协议（AIRP）做出贡献！本文档提供贡献指南。

> ⚠️ **当前阶段的贡献政策**
>
> 我们欢迎通过 **GitHub Issues 进行讨论**。
>
> **当前不接受外部 Pull Request。** 如果您有任何建议 — bug 报告、功能想法、规范澄清或示例建议 — 请通过 Issue 描述。如果我们认为有价值，由维护者实现并在 commit/release notes 中署名感谢您。
>
> 此政策未来会重新审视。

> **阶段状态（v1.0.0）**
>
> AIRP 处于早期规范阶段。下方流程描述的是**目标**治理模型。初期决策由 AIXP Labs 核心维护者做出；社区讨论窗口将随贡献者基数增长而扩大。

## 如何贡献

### 报告 Issue

- 使用 [GitHub Issues](https://github.com/AIXP-Labs/AIRP/issues) 报告 bug、提议功能或建议规范变更
- 规范变更请使用 `spec-change` issue 模板
- 提供清晰描述，尽可能附带示例

### 讨论驱动开发

请勿直接提交 PR，而是：

1. **打开 Issue**，描述您的提议、Bug 或想法
2. **与维护者讨论** — 明确范围、设计和方法
3. **等待审核** — 重要提议遵循下方[规范变更](#规范变更)流程
4. **若被采纳**，维护者将实现该变更并在 commit/release notes 中署名感谢您

### 规范变更

影响规范性内容（`specification/` 中任何文件）的提议遵循以下流程：

1. 带 `spec-change` 标签的 Issue，描述提议变更
2. 非平凡变更需要至少 14 天的讨论期（目标治理模型；当前讨论窗口随贡献者基数调整）
3. 重大决策需要在 `adrs/` 中记录架构决策记录（ADR）
4. 维护者进行 Axiom 0 合规审查
5. 中华人民共和国监管合规审查（PBOC / SAFE / CAC / CSRC 对齐）
6. 同步更新反映变更的文档
7. **英文版与中文版必须同步更新**

### 文档变更

非规范性内容（guides、topics、reference、examples）的建议通过 Issue 提交即可 — 错别字修正、澄清、补充示例尤其受欢迎。维护者将实现被采纳的建议，确保符合 Axiom 0 与 PRC 监管要求。

## 贡献原则

### 写作风格

- 使用清晰简洁的语言
- 遵循现有文档结构与格式
- 所有 content 值必须为人类语言（不允许不透明代码或纯机器 token）
- 中文与英文版本均为第一等级；默认 README 为中文（`README.md`），英文版为 `README_EN.md`。两者必须保持同步。

### Axiom 0 合规

每一项贡献必须符合 Axiom 0：人类主权与福祉。具体而言：

- 变更不得削弱人类对 AI 商业互动的监督
- 变更不得使 AI 代理绕过透明度要求
- 变更不得损害 Dignity Standard
- 变更必须保留人类授权商业行为的双签名要求

### Commit 信息格式

```
<type>(<scope>): <description>

[optional body]

[optional footer]
```

类型：`feat`、`fix`、`docs`、`spec`、`refactor`、`test`、`chore`

示例：
- `spec(trust): add V4 Premier trust level stake requirements`
- `docs(guide): add getting started guide for contract creation`
- `fix(spec): correct CONTRACT_PROPOSE message format example`

### 双语要求

规范变更：
- 中文版（`specification/AIRP_Protocol_cn.md`）与英文版（`specification/AIRP_Protocol.md`）必须在同一个 PR 中同步更新
- Axiom 0 中文：「人类主权与福祉」（不使用缩写）
- 保持术语一致 — 参考 `docs/reference/glossary.md`

## 写作规范

### RFC 2119 关键词

撰写规范性内容时，请使用 [RFC 2119](https://tools.ietf.org/html/rfc2119) 定义的关键词：

- **MUST** / **MUST NOT** — 绝对要求
- **SHOULD** / **SHOULD NOT** — 强烈建议（允许有据可循的例外）
- **MAY** — 真正可选

这些关键词在规范意义上**必须**大写。

### 术语规范

- 使用 "AIRP agent" 指代受治理的 AI 商业代理
- 使用 "Trust Level V0–V4"，V 前缀大写（V0 Stranger、V4 Premier — 注意：V 表示 Value/Verified，不是 T）
- "Axiom 0"、"Dignity Standard" 大写（专有名词）
- 货币：写 "CNY"（ISO 4217）或「人民币」；规范性文本中切勿缩写为 "RMB"
- 结算渠道：「Alipay 担保交易」、「WeChat Pay 担保交易」、「数字人民币（e-CNY）」 — 保留官方名称
- 监管引用：PBOC（中国人民银行）、SAFE（国家外汇管理局）、CAC（国家互联网信息办公室）、CSRC（中国证券监督管理委员会）

### 文档结构

- 每个主题文档以一段简介开头
- 字段规范用表格
- 示例代码块标注语言
- 流程示意用 Mermaid 图或邮件交互记录
- 文档之间用相对链接互相引用

### 闭合签名

所有规范文档**必须**以下行结尾：

```
Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev
```

## 开发环境

### 前置条件

- Git
- Python 3.8+（用于 MkDocs 文档站点）
- MkDocs Material 主题（`pip install mkdocs-material`）

### 构建文档

```bash
# 安装依赖
pip install mkdocs-material

# 本地预览
mkdocs serve

# 构建静态站点
mkdocs build
```

## 行为准则

所有贡献者必须遵守 [行为准则](CODE_OF_CONDUCT.md)。Axiom 0 承诺适用于所有贡献。

## 贡献的许可

提交 Issue 或任何其他内容（包括规范建议、Issue 中的代码片段或设计建议）即表示您同意维护者可以在 [Apache License 2.0](LICENSE) 条款下使用您提交的内容，与本项目使用相同的许可证。

## 提问

- 一般问题请通过 [GitHub Discussion](https://github.com/AIXP-Labs/AIRP/discussions) 提出
- 私密咨询请通过 [Security Advisory](https://github.com/AIXP-Labs/AIRP/security/advisories/new) 提交

---

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev
