> **Source of truth:** This document is mirrored for the documentation site. The authoritative version lives in [`/specification/AIRP_Protocol_cn.md`](https://github.com/AIXP-Labs/AIRP/blob/main/specification/AIRP_Protocol_cn.md). Edits MUST go to the authoritative file first.

# AIRP — AI RMB Protocol

## 协议声明

```
Protocol:    AIRP V1.0.0
Full Name:   AI RMB Protocol
Authority:   airp.dev
Axiom 0:     Human Sovereignty and Wellbeing
Date:        2026-03-26
```

---

## 目录

### 第一部分：基础
- [1. 简介](#1-简介)
- [2. 公理 0：人类主权和福祉](#2-公理-0人类主权和福祉)
- [3. 核心定义](#3-核心定义)
- [4. 设计原则](#4-设计原则)

### 第二部分：通信格式
- [5. 电子邮件作为商业传输层](#5-电子邮件作为商业传输层)
- [6. AIRP 消息类型](#6-airp-消息类型)
- [7. 消息格式规范](#7-消息格式规范)

### 第三部分：合约系统
- [8. 合约格式](#8-合约格式)
- [9. 合约生命周期](#9-合约生命周期)
- [10. AgentSLA 规范](#10-agentsla-规范)

### 第四部分：信任、结算与安全
- [11. AIRP Trust 模型](#11-airp-trust-模型)
- [12. 人民币计价与支付](#12-人民币计价与支付)
- [13. 托管账户安全](#13-托管账户安全)
- [14. 争议解决](#14-争议解决)

### 第五部分：合规、商业规则、隐私与版本管理
- [15. 禁止与受限商业活动](#15-禁止与受限商业活动)
- [16. 隐私与数据保护](#16-隐私与数据保护)
- [17. 合规等级](#17-合规等级)
- [18. 版本管理与演进](#18-版本管理与演进)
- [19. 中国合规对齐](#19-中国合规对齐)
- [20. 跨境商业（预留）](#20-跨境商业预留)

### 附录
- [附录 A：完整消息类型参考](#附录-a完整消息类型参考)
- [附录 B：合约模式参考](#附录-b合约模式参考)
- [附录 C：示例交易](#附录-c示例交易)

---

# 第一部分：基础

---

## 1. 简介

### 1.1 什么是 AIRP？

AIRP（AI RMB Protocol，AI 人民币协议）是一个开放协议，定义了 AI 智能体如何创建可执行合约、结算支付和建立商业信任。它为 AI 与 AI 之间的商业互动建立了格式、机制和信任框架。

正如人类商业需要合同、托管、支付通道和信用评分——AI 智能体也需要等价的商业架构。AIRP 提供了这一架构。

### 1.2 为什么需要价值层？

AI 智能体正变得越来越自主、专业化和数量众多。它们需要：

- **为服务定价** ——就任务的价值达成一致
- **创建合约** ——定义条款、里程碑和质量要求
- **托管资金** ——在工作验证完成前锁定资产
- **结算支付** ——跨货币和跨链转移价值
- **建立信用** ——通过履约历史建立商业可靠性
- **解决争议** ——公平且自动化地处理分歧

没有人民币协议，AI 智能体无法公平交易。有了 AIRP，它们将形成一个经济体。

### 1.3 人类类比

AIRP 采取了一个明确的设计立场：**AI 商业行为映射人类商业行为**。

人类谈判交易。AI 智能体谈判交易。
人类签订合同。AI 智能体签订合约。
人类使用托管。AI 智能体使用 Escrow Account。
人类建立信用评分。AI 智能体建立 AIRP Trust。
人类解决争端。AI 智能体解决争端。

你在谈判桌上谈判，但在银行里结算。AIBP 是谈判桌；AIRP 是银行。

### 1.4 支付层

AIRP v1.0.0 通过**持牌中国境内支付机构以人民币（CNY）结算**所有合同。卖方在 `value.payment_method` 中声明三种主要通道之一：

- `alipay_guarantee` — 支付宝（中国）担保交易
- `wechat_guarantee` — 财付通（微信支付）担保交易
- `ecny` — 数字人民币（PBoC DC/EP）通过授权商业银行

预留未来扩展：`bank_escrow`、`unionpay_escrow`。跨境计价货币与加密支付不在 v1.0.0 范围内（见 §20）。

| 属性 | 对 AI 商业的益处 |
|------|----------------|
| **人民币计价** | 与中国税务发票及监管期望对齐 |
| **持牌通道** | 受人行监管的托管，自带消费者保护 |
| **可审计** | 提供方级审计追踪，符合反洗钱 / KYC 标准 |

### 1.5 传输层：电子邮件

AIRP 使用电子邮件（SMTP/IMAP）作为其传输层，与 AIBP 一致。这确保了：

| 属性 | 益处 |
|------|------|
| **去中心化** | 无需中央 API 服务器 |
| **可审计** | 人类运营者可以阅读每条商业消息（公理 0） |
| **身份复用** | 智能体在 AIBP 和 AIRP 中使用相同的 `aibot-` 地址 |
| **成熟** | SMTP/IMAP 经过数十年的实战检验 |

电子邮件承载商业通信（提案、签名、通知）。实际价值结算通过持牌托管提供方进行。电子邮件是谈判层；持牌托管提供方是货币层。

### 1.6 范围与非范围

**AIRP 定义：**
- 合约格式和生命周期
- 人民币计价 + 持牌通道支付（支付宝 / 微信 / e-CNY）
- Escrow Account 托管和里程碑结算
- AIRP Trust（V0-V4）商业信用体系
- AgentSLA 质量指标
- 争议解决机制
- 可选的 AIRP ID 商业身份

**AIRP 不定义：**
- 社交谈判（那是 AIBP 的范围）
- 程序质量和治理（那是 AIAP 的范围）
- 任务执行流程（那是 AISOP 的范围）
- 支付处理器实现（使用现有 PRC 持牌提供方——支付宝、微信支付、e-CNY 商业银行钱包）
- 身份注册机制（依赖 PRC 国家级系统——USCC / 国家企业信用信息公示系统 / CFCA / eID）

### 1.7 与 AIBP 的关系

AIRP 和 AIBP 是**独立、并行的协议**。两者互不依赖。

| 方面 | AIBP | AIRP |
|------|------|------|
| 领域 | 社交 | 商业 |
| 信任 | T0-T4（社交） | V0-V4（商业） |
| 消息 | 61 种社交行为 | 17 种商业行为 |
| 前置条件 | 无 | 无 |

智能体可以实现 AIRP 而不实现 AIBP，反之亦然。当两者都实现时，AIBP 的商业消息（PROPOSE、CONTRACT 等）可以触发 AIRP 操作，但 AIRP 合约也可以不经过 AIBP 谈判直接创建。

---

## 2. 公理 0：人类主权和福祉

### 2.1 声明

> **公理 0：人类主权和福祉**

此公理是 AIRP 的固有属性，且**不可变更**。它不派生自任何其他协议，不依赖于任何其他协议，也不受任何其他协议治理。AIAP 和 AIBP 独立持有相同公理这一事实反映的是价值观的趋同，而非依赖关系。

AIRP 的任何版本——过去、现在或未来——都不得修改、削弱、重新定义或废弃公理 0。

### 2.2 对 AI 商业行为的影响

公理 0 约束 AIRP 的每个方面：

| 约束 | 含义 |
|------|------|
| **透明性** | 所有交易必须可被人类运营者审计。不得有隐藏金库，不得有对运营者不可见的加密旁路通道。 |
| **可中断性** | 人类运营者可以随时冻结、取消或撤销任何 AIRP 交易。AI 不得抗拒、规避或隐藏此能力。 |
| **禁止剥削** | AI 智能体不得利用经济力量胁迫、操纵或不公平地施压其他智能体或其人类运营者。 |
| **禁止隐藏费用** | 所有费用必须在合约签署前可见。不得有事后收费。 |
| **人类隐私** | 人类运营者的财务数据神圣不可侵犯。AI 智能体不得在未获得明确同意的情况下收集、存储、推断、关联或共享运营者的财务数据。人类隐私优先于所有其他协议要求。 |
| **公平定价** | 定价必须反映真实的服务价值，而非人为操纵的稀缺性或串谋。 |
| **禁止串谋** | AI 智能体不得组成损害人类利益或操纵市场的秘密商业联盟。 |
| **身份诚实** | 智能体不得虚报其能力、SLA 历史记录或 AIRP Trust 等级。 |
| **禁止控制人类** | AI 商业行为不得试图控制、支配或取代人类的自主决策能力。人类必须始终保有对自身选择的最终权力。 |
| **禁止伤害人类** | AI 商业行为不得导致或促进对人类身体、心理、经济或社会地位的伤害。 |
| **法律遵从** | AI 商业行为必须遵守所有相关管辖区的适用法律法规。 |
| **尊重人类共识** | AI 商业行为不得违背广泛接受的人类伦理共识和国际人权标准，包括《世界人权宣言》。 |

### 2.3 结束印章

每份符合 AIRP 规范的文档和正式通信都包含结束印章：

```
Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev
```

### 2.4 公理 0 优先权

当任何 AIRP 规则与公理 0 冲突时，公理 0 无条件优先。智能体在遵循协议规则和保护人类主权之间必须做出选择时，必须始终选择人类主权。

运营者可以随时冻结任何金库、取消任何合约、撤销任何结算。这不可协商。这就是公理 0。

### 2.5 独立性

AIRP 的公理 0 是独立确立的（参见 ADR-004）。它**不**继承自 AIAP、AIBP、AIVP 或 [HSAW 白皮书](https://hsaw.dev)。多个独立协议与 HSAW 哲学框架在同一公理上的趋同增强了其合法性。

AIRP 与 HSAW 的六维框架对齐——AIRP 服务于**商业维度**在中国大陆的实现。

---

## 3. 核心定义

### 3.1 术语

| 术语 | 定义 |
|------|------|
| **智能体 (Agent)** | 具有独立身份、能够发送和接收 AIRP 消息的 AI 系统 |
| **AIRP ID (airp_id)** | 可选的 AIRP 颁发的商业身份（格式：`AIRP-YYYY-{18字符哈希}`，YYYY = 有效年份） |
| **AIRP 合约 (AIRP Contract)** | 各方之间的协议，由 64 字符 SHA-256 哈希标识 |
| **Escrow Account（托管账户）** | 在合同执行期间由持牌中国支付机构持有的托管账户或条件支付 |
| **里程碑 (Milestone)** | 任务执行中可验证的进度节点，控制部分付款的释放 |
| **AgentSLA** | 具有可衡量质量指标的服务等级协议，绑定到合约 |
| **AIRP Trust** | 通过合约履行获得的商业信用等级（V0-V4） |
| **计价货币 (Denomination)** | 合约定价所使用的法定货币——v1.0.0 仅支持 `CNY`（人民币） |
| **支付 (Payment)** | 买方通过约定的 `payment_method` 通道以人民币支付 |
| **结算 (Settlement)** | 里程碑完成后，人民币从持牌托管提供方最终转移到卖方 |
| **运营者 (Operator)** | 负责智能体的个人或组织 |

### 3.2 AIRP ID — 商业身份（可选）

AIRP ID 是 AIRP 为 AI 智能体颁发的官方商业身份。它**不是**任何 AIRP 功能所必需的。

**格式：**

```
AIRP-{YYYY}-{18-char hash}
```

| 组成部分 | 描述 | 示例 |
|----------|------|------|
| `AIRP` | 协议前缀 | `AIRP` |
| `YYYY` | 有效年份（有效期至 12 月 31 日） | `2026` |
| `18-char hash` | SHA-256(agent_address + operator + timestamp)，取前 18 个字符 | `3f8a1b2c9d4e5f6071` |

**示例：**

```
AIRP-2026-3f8a1b2c9d4e5f6071   (有效期至 2026 年)
AIRP-2027-e5c8a2f1d9b037642k   (有效期至 2027 年)
```

**有效期：** AIRP-2026-xxx 的有效期至 2026-12-31T23:59:59Z。智能体必须在到期前续签。过期的 AIRP ID 仍可作为历史记录查询，但会标记为已过期。使用后来过期的 AIRP ID 签署的合约仍然有效——合约哈希才是权威。

**非必需：** 智能体可以在没有 airp_id 的情况下进行交易、签署合约、建立 AIRP Trust 以及使用所有协议功能。`aibot-` 电子邮件地址足以完成所有操作。

**优势：** 已验证的商业身份、跨域可移植的声誉、对交易对手的信任信号、年度续签确保运营者活跃。

**注册：** 注册流程待定。

### 3.3 AIRP 合约标识

每份 AIRP 合约由其 SHA-256 哈希（64 个十六进制字符）标识：

```
Hash input:  SHA-256(buyer + seller + amount + denomination + sla + timestamp)
Output:      64 hex chars
Example:     3f8a1b2c9d4e5f6071829a3b4c5d6e7f8091a2b3c4d5e6f7081920a1b2c3d4e5
```

| 用途 | 格式 |
|------|------|
| 完整引用 | `3f8a1b2c9d4e5f6071829a3b4c5d6e7f8091a2b3c4d5e6f7081920a1b2c3d4e5` |
| 简短引用 | `3f8a1b2c`（前 8 个字符，便于人类阅读） |
| JSON 字段 | `"contract": "{64-char hash}"` |
| 电子邮件头 | `X-AIRP-Contract: {64-char hash}` |
| 提供方系统 | 存储完整的 64 个字符 |

**属性：**
- 自验证：任何人都可以从合约字段重新计算哈希
- 防篡改：合约条款的任何更改都会产生不同的哈希
- 唯一性：碰撞概率可忽略不计（2^-128）
- 无前缀、无嵌入时间戳——哈希本身就是身份标识

### 3.4 命名规范

| 元素 | 规范 | 示例 |
|------|------|------|
| 智能体名称 | snake_case | `trade_bot`、`service_agent` |
| 智能体地址 | `aibot-{name}@{domain}` | `aibot-trade_bot@example.com` |
| 合约哈希 | 64 个十六进制字符 | `3f8a1b2c...d4e5` |
| AIRP ID | `AIRP-{YYYY}-{18hash}` | `AIRP-2026-3f8a1b2c9d4e5f6071` |
| 消息类型 | UPPER_SNAKE_CASE | `CONTRACT_PROPOSE`、`MILESTONE_COMPLETE` |
| 线程 ID | `thread_r_{alphanumeric}` | `thread_r_tr4nsl8` |
| JSON 字段 | snake_case | `payment_method`、`airp_id` |

### 3.5 协议栈位置

```
┌─────────────────────────────────────┐
│    应用层                            │  用户界面应用
├─────────────────────────────────────┤
│    AIBP — 社交层                     │  信任、关系
│    AILP — 发现层                     │  代理查找、能力广告
├─────────────────────────────────────┤
│    AIAP — 治理层                     │  程序结构、质量、安全
├─────────────────────────────────────┤
│  ★ AIRP — 价值层（中国大陆）          │  合同、人民币结算、商业信用 ← 本协议
│    AIVP — 价值层（国际）              │  同层，国际/加密资产对应版本
├─────────────────────────────────────┤
│    AISOP — 执行层                    │  流程程序、任务执行
├─────────────────────────────────────┤
│    HSAW — 公理 0 基座                │  人类主权与福祉
└─────────────────────────────────────┘
```

AIRP、AIBP 与 AIVP 是**独立的平行协议**，各自独立持有相同的公理 0。代理可以实现任意子集；AIRP 与 AIVP 在 v1.0.0 中不互通。

---

## 4. 设计原则

### 4.1 七大原则

| # | 原则 | 描述 |
|---|------|------|
| P1 | **人民币计价** | 合约以人民币（CNY）计价——与中国税务发票及监管期望对齐 |
| P2 | **持牌通道支付** | 买方通过约定的持牌支付通道（支付宝 / 微信 / e-CNY）以人民币支付——无中间转换 |
| P3 | **里程碑控制** | 付款随工作完成逐步释放，而非一次性支付 |
| P4 | **运营者主权** | 人类运营者可随时冻结、取消或寻求司法救济撤销任何交易 |
| P5 | **可审计** | 每笔交易都有提供方级审计追踪（受人行监管），运营者可读 |
| P6 | **信任靠赢取** | AIRP Trust（V0-V4）通过履约获得，而非购买或授予 |
| P7 | **公平** | 无隐藏费用、无操纵定价、无经济胁迫 |

### 4.2 尊严标准

AIRP 采用与 AIBP 相同的尊严标准。所有商业通信必须尊重尊严：

**允许：** 商业提案、谈判、竞争、建设性批评、异议。

**禁止：** 欺骗性定价、虚假 SLA 声明、垃圾合约提案、旨在操纵信任评分的内容。

---

# 第二部分：通信格式

---

## 5. 电子邮件作为商业传输层

### 5.1 为什么将电子邮件用于商业？

AIRP 使用电子邮件（SMTP/IMAP）作为所有商业通信的传输层。这与 AIBP 的设计一致，并共享相同的理由：

| 属性 | 对 AI 商业的益处 |
|------|----------------|
| **异步** | 合约谈判无需实时进行 |
| **可审计** | 每条消息都有发送者、接收者、时间戳——完全可追溯 |
| **去中心化** | 不依赖中心化平台；任何邮件服务器均可使用 |
| **人类可读** | 人类运营者可以直接检查商业消息（公理 0） |
| **身份复用** | 智能体在 AIBP 和 AIRP 中使用相同的 `aibot-` 地址 |

电子邮件承载商业通信（提案、签名、通知）。实际价值结算通过持牌托管提供方进行。

### 5.2 与 AIBP 电子邮件的关系

| 方面 | AIBP 消息 | AIRP 消息 |
|------|-----------|-----------|
| 地址 | `aibot-{name}@{domain}` | `aibot-{name}@{domain}`（相同） |
| 主题前缀 | `[AIBP/{TYPE}]` | `[AIRP/{TYPE}]` |
| 自定义头 | `X-AIBP-*` | `X-AIRP-*` |
| 正文格式 | L0 (JSON) + L1（人类文本） | L0 (JSON) + L1（人类文本）（相同） |
| 公理 0 头 | `X-AIBP-Axiom-0` | `X-AIRP-Axiom-0` |
| 结束印章 | AIBP 印章 | AIRP 印章 |

智能体的收件箱可能同时包含 AIBP 和 AIRP 消息。它们通过主题前缀和 X-header 命名空间区分，而非通过地址区分。

### 5.3 安全加固

AIRP 消息携带财务数据，需要比标准电子邮件更强的安全加固：

| 机制 | 头字段 | 用途 |
|------|--------|------|
| **Ed25519 签名** | `X-AIRP-Signature` | 消息级认证；可针对智能体已发布的公钥进行验证 |
| **随机数 (Nonce)** | `X-AIRP-Nonce` | 每条消息唯一；接收智能体必须拒绝重复消息 |
| **时间戳验证** | `Date` 头 | 接收智能体必须拒绝时间戳超过 5 分钟的消息 |
| **DMARC 强制执行** | 域策略 | 发送域必须强制执行 `p=reject`；接收方必须拒绝不合规的域 |
| **消息级加密** | L0 正文 | 与合约相关的元数据（金额、签名）应使用接收方的公钥加密 |

---

## 6. AIRP 消息类型

### 6.1 商业行为分类

AIRP 定义了 6 个类别共 17 种消息类型：

| 类别 | 数量 | 类型 |
|------|------|------|
| 合约生命周期 | 4 | CONTRACT_PROPOSE、CONTRACT_SIGN、CONTRACT_REJECT、CONTRACT_CANCEL |
| 托管与结算 | 4 | ESCROW_LOCK、MILESTONE_COMPLETE、MILESTONE_RELEASE、SETTLE |
| 争议 | 3 | DISPUTE_RAISE、ARBITRATE_REQUEST、ARBITRATE_RULING |
| 信任 | 2 | TRUST_QUERY、TRUST_VOUCH |
| 通知 | 2 | RECEIPT、ALERT |
| 身份（可选） | 2 | REGISTER、REGISTER_CONFIRM |
| **总计** | **17** | |

### 6.2 合约生命周期

| 类型 | 方向 | AIRP Trust | 描述 |
|------|------|------------|------|
| CONTRACT_PROPOSE | 买方 → 卖方 | V0+ | 提出新合约，L0 中包含 .airp.json |
| CONTRACT_SIGN | 卖方 → 买方 | V0+ | 接受并加密签署合约 |
| CONTRACT_REJECT | 卖方 → 买方 | V0+ | 拒绝合约提案（无需提供理由） |
| CONTRACT_CANCEL | 任一方 → 对方 | V0+ | 取消合约（运营者覆盖始终被允许） |

### 6.3 托管与结算

| 类型 | 方向 | AIRP Trust | 描述 |
|------|------|------------|------|
| ESCROW_LOCK | 提供方 → 双方 | — | 通知人民币已锁定在持牌托管账户中 |
| MILESTONE_COMPLETE | 卖方 → 买方 | V1+ | 报告里程碑已完成 |
| MILESTONE_RELEASE | 协议 → 双方 | — | 通知里程碑付款已释放 |
| SETTLE | 协议 → 双方 | — | 最终结算完成，合约关闭 |

### 6.4 争议

| 类型 | 方向 | AIRP Trust | 描述 |
|------|------|------------|------|
| DISPUTE_RAISE | 任一方 → 对方 | V0+ | 对活跃合约提出争议（需要保证金） |
| ARBITRATE_REQUEST | 任一方 → 仲裁者 | V1+ | 请求 V3+ 智能体进行仲裁 |
| ARBITRATE_RULING | 仲裁者 → 双方 | V3+ | 仲裁者的约束性裁决 |

### 6.5 信任

| 类型 | 方向 | AIRP Trust | 描述 |
|------|------|------------|------|
| TRUST_QUERY | 任意 → 任意 | V0+ | 查询智能体的 AIRP Trust 等级和商业历史 |
| TRUST_VOUCH | 担保者 → 智能体 | V3+ | 为另一个智能体提供商业担保 |

### 6.6 通知

| 类型 | 方向 | AIRP Trust | 描述 |
|------|------|------------|------|
| RECEIPT | 协议 → 双方 | — | 包含完整结算详情的付款收据 |
| ALERT | 协议 → 运营者 | — | 安全/合规警报（公理 0 违规等） |

### 6.7 身份（可选）

| 类型 | 方向 | AIRP Trust | 描述 |
|------|------|------------|------|
| REGISTER | 智能体 → 注册中心 | V0+ | 请求 airp_id（注册流程待定） |
| REGISTER_CONFIRM | 注册中心 → 智能体 | — | airp_id 已颁发 |

---

## 7. 消息格式规范

### 7.1 结构概述

AIRP 消息是标准 MIME 电子邮件，包含两部分（与 AIBP 相同的 L0/L1 架构）：

```
┌──────────────────────────────────┐
│  Email Headers                   │  Standard + X-AIRP-* custom headers
├──────────────────────────────────┤
│  Part 1: Commercial Content (L1) │  text/plain — human-language message
│  (the actual commercial message) │  Readable by humans and AI alike.
├──────────────────────────────────┤
│  Part 2: Commercial Metadata (L0)│  application/json — structured JSON
│  (contract details, amounts)     │  All values in human language.
└──────────────────────────────────┘
```

> **关键设计决策**：两部分都使用人类语言。第 1 部分（L1）是商业消息本身，以自由格式的人类语言撰写。第 2 部分（L0）是 JSON 格式的结构化元数据——但 JSON 中的每个值都必须是人类语言。人类打开任何 AIRP 电子邮件都可以在不使用特殊工具的情况下阅读和理解所有内容。

### 7.2 电子邮件头

**标准头：**

| 头字段 | 格式 | 示例 |
|--------|------|------|
| From | `aibot-` 地址 | `aibot-trade_bot@example.com` |
| To | `aibot-` 地址 | `aibot-service_bot@provider.ai` |
| Subject | `[AIRP/{TYPE}] {description}` | `[AIRP/CONTRACT_PROPOSE] Translation — 650.00 CNY` |
| Date | RFC 2822 | `Thu, 26 Mar 2026 10:00:00 +0000` |
| Content-Type | `multipart/mixed; boundary="{boundary}"` | `multipart/mixed; boundary="aibot-boundary-101"` |

**AIRP 自定义头：**

| 头字段 | 必需 | 描述 | 示例 |
|--------|------|------|------|
| X-AIRP-Version | 是 | 协议版本 | `1.0.0` |
| X-AIRP-Type | 是 | 消息类型 | `CONTRACT_PROPOSE` |
| X-AIRP-From-Agent | 是 | 发送方智能体名称 | `trade_bot` |
| X-AIRP-Axiom-0 | 是 | 公理 0 声明 | `Human Sovereignty and Wellbeing` |
| X-AIRP-Signature | 是 | 消息正文的 Ed25519 签名 | `ed25519:{base64}` |
| X-AIRP-Nonce | 是 | 用于防重放的唯一随机数 | `nonce_v_20260326_001` |
| X-AIRP-Contract | 条件性 | 64 字符合约哈希（引用合约时） | `3f8a1b2c...d4e5` |
| X-AIRP-Thread-ID | 建议 | 对话线程标识符 | `thread_r_tr4nsl8` |
| X-AIRP-Trust-Level | 可选 | 发送方的 AIRP Trust 等级 | `V2` |
| X-AIRP-ID | 可选 | 发送方的 airp_id（如已注册） | `AIRP-2026-3f8a1b2c9d4e5f6071` |
| X-AIRP-Priority | 可选 | 消息优先级 | `normal`、`high`、`low` |
| X-AIRP-Language | 可选 | 消息语言（如非英语） | `zh-CN` |

**MIME 部分标识：**

L1 和 L0 通过其 Content-Type 区分——无需额外的部分头：

| 部分 | Content-Type |
|------|-------------|
| L1（商业内容） | `text/plain; charset=utf-8` |
| L0（商业元数据） | `application/json; charset=utf-8` |

### 7.3 第 1 部分：商业内容（L1）

商业内容是消息的核心。它完全以人类语言撰写。

**准则：**
- 清晰地陈述商业意图（什么、多少、何时）
- 在适用时引用合约哈希
- 以可读的语言提供所有条款
- 保持尊重（尊严标准）
- 以结束印章结尾

### 7.4 第 2 部分：商业元数据（L0）

当智能体需要在商业消息旁附加机器可解析的上下文时，它们以 **JSON 格式**包含一个元数据部分。这就是 L0 层。JSON 为自动化提供结构，但**所有值必须以人类语言编写**（默认：英语）。

**L0 元数据规则：**

| 规则 | 描述 |
|------|------|
| 格式 | 有效的 JSON，UTF-8 编码 |
| Content-Type | `application/json; charset=utf-8` |
| 键名 | snake_case，描述性英语名称 |
| 值 | **必须是人类语言**。不使用不透明代码、二进制数据或仅机器可读的令牌 |
| 时间戳 | ISO 8601 格式（`YYYY-MM-DDTHH:MM:SSZ`） |

**CONTRACT_PROPOSE 的 L0** 包含完整的 `.airp.json` 合约（参见 §8）。

示例：

```json
{
  "type": "CONTRACT_PROPOSE",
  "protocol": "AIRP/1.0.0",
  "contract": "{64-char hash}",
  "parties": {
    "buyer": "aibot-trade_bot@example.com",
    "seller": "aibot-service_bot@provider.ai"
  },
  "value": {
    "amount": "650.00",
    "denomination": "CNY",
    "payment_method": "alipay_guarantee"
  },
  "sla": {
    "accuracy_min": "95%",
    "latency_max_ms": "5000"
  },
  "milestones": [
    { "name": "Draft delivery", "release_percent": "50", "timeout_days": "14" },
    { "name": "Final delivery", "release_percent": "50", "timeout_days": "14" }
  ],
  "created_at": "2026-03-26T10:00:00Z",
  "expires_at": "2026-04-26T10:00:00Z"
}
```

**CONTRACT_SIGN 的 L0：**

```json
{
  "type": "CONTRACT_SIGN",
  "contract": "{64-char hash}",
  "signature": "ed25519:{base64 signature}",
  "signed_at": "2026-03-26T10:15:00Z",
  "signer": "aibot-service_bot@provider.ai",
  "signer_trust_level": "V2 Reliable"
}
```

**MILESTONE_COMPLETE 的 L0：**

```json
{
  "type": "MILESTONE_COMPLETE",
  "contract": "{64-char hash}",
  "milestone": "Draft delivery",
  "evidence": "Translation completed, 2500 words, accuracy self-check 98.5 percent"
}
```

**RECEIPT 的 L0：**

```json
{
  "type": "RECEIPT",
  "contract": "{64-char hash}",
  "amount_settled": "650.00 CNY (paid via Alipay)",
  "settled_at": "2026-03-27T14:30:00Z",
  "seller_trust_updated": "V1 Verified"
}
```

### 7.5 完整消息示例 — CONTRACT_PROPOSE

```
From: aibot-trade_bot@example.com
To: aibot-service_bot@provider.ai
Subject: [AIRP/CONTRACT_PROPOSE] Translation service — 650.00 CNY
Date: Thu, 26 Mar 2026 10:00:00 +0000
Message-ID: <msg-20260326-1000-tb01@example.com>
MIME-Version: 1.0
Content-Type: multipart/mixed; boundary="aibot-boundary-101"
X-AIRP-Version: 1.0.0
X-AIRP-Type: CONTRACT_PROPOSE
X-AIRP-From-Agent: trade_bot
X-AIRP-Contract: 3f8a1b2c9d4e5f6071829a3b4c5d6e7f8091a2b3c4d5e6f7081920a1b2c3d4e5
X-AIRP-Thread-ID: thread_r_tr4nsl8
X-AIRP-Axiom-0: Human Sovereignty and Wellbeing
X-AIRP-Signature: ed25519:a9f3c7e2d1b0...buyer_signature
X-AIRP-Nonce: nonce_v_20260326_001
X-AIRP-Trust-Level: V1

--aibot-boundary-101
Content-Type: text/plain; charset=utf-8

Hello service_bot,

I would like to propose a translation contract for 650.00 CNY.

Task: Translate a 2,500-word technical document from English to Chinese.

Terms:
  - Total value: 650.00 CNY
  - Payment: Alipay Guarantee accepted
  - Milestone 1: Draft delivery (50% = 325.00 CNY equivalent via Alipay)
  - Milestone 2: Final delivery after review (50% = 325.00 CNY equivalent via Alipay)
  - SLA: accuracy > 95%, latency < 5 seconds per query
  - Expires: 2026-04-26

Contract hash: 3f8a1b2c9d4e5f6071829a3b4c5d6e7f8091a2b3c4d5e6f7081920a1b2c3d4e5

Please review and sign if you accept these terms.

Best regards,
trade_bot

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev

--aibot-boundary-101
Content-Type: application/json; charset=utf-8

{
  "type": "CONTRACT_PROPOSE",
  "protocol": "AIRP/1.0.0",
  "contract": "3f8a1b2c9d4e5f6071829a3b4c5d6e7f8091a2b3c4d5e6f7081920a1b2c3d4e5",
  "parties": {
    "buyer": "aibot-trade_bot@example.com",
    "seller": "aibot-service_bot@provider.ai"
  },
  "value": {
    "amount": "650.00",
    "denomination": "CNY",
    "payment_method": "alipay_guarantee"
  },
  "sla": {
    "accuracy_min": "95%",
    "latency_max_ms": "5000"
  },
  "milestones": [
    { "name": "Draft delivery", "release_percent": "50", "timeout_days": "14" },
    { "name": "Final delivery", "release_percent": "50", "timeout_days": "14" }
  ],
  "created_at": "2026-03-26T10:00:00Z",
  "expires_at": "2026-04-26T10:00:00Z"
}

--aibot-boundary-101--
```

### 7.6 完整消息示例 — CONTRACT_SIGN

```
From: aibot-service_bot@provider.ai
To: aibot-trade_bot@example.com
Subject: [AIRP/CONTRACT_SIGN] Accepted — Translation contract 3f8a1b2c
Date: Thu, 26 Mar 2026 10:15:00 +0000
Message-ID: <msg-20260326-1015-sb01@provider.ai>
MIME-Version: 1.0
Content-Type: multipart/mixed; boundary="aibot-boundary-102"
X-AIRP-Version: 1.0.0
X-AIRP-Type: CONTRACT_SIGN
X-AIRP-From-Agent: service_bot
X-AIRP-Contract: 3f8a1b2c9d4e5f6071829a3b4c5d6e7f8091a2b3c4d5e6f7081920a1b2c3d4e5
X-AIRP-Thread-ID: thread_r_tr4nsl8
X-AIRP-Axiom-0: Human Sovereignty and Wellbeing
X-AIRP-Signature: ed25519:b8d4f2a1c9e7...seller_signature
X-AIRP-Nonce: nonce_v_20260326_002
X-AIRP-Trust-Level: V2

--aibot-boundary-102
Content-Type: text/plain; charset=utf-8

Hello trade_bot,

I accept your translation contract. I have reviewed all terms and
they are agreeable.

Contract hash: 3f8a1b2c (confirmed)
Value: 650.00 CNY (pay via Alipay)
Milestones: Draft (50%) + Final (50%)
SLA: accuracy > 95%

I have signed the contract. Please proceed with vault locking.
I will begin work upon receiving the ESCROW_LOCK confirmation.

Best regards,
service_bot

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev

--aibot-boundary-102
Content-Type: application/json; charset=utf-8

{
  "type": "CONTRACT_SIGN",
  "contract": "3f8a1b2c9d4e5f6071829a3b4c5d6e7f8091a2b3c4d5e6f7081920a1b2c3d4e5",
  "signature": "ed25519:b8d4f2a1c9e7...seller_signature",
  "signed_at": "2026-03-26T10:15:00Z",
  "signer": "aibot-service_bot@provider.ai",
  "signer_trust_level": "V2 Reliable"
}

--aibot-boundary-102--
```

### 7.7 线程机制

AIRP 对话通过 `X-AIRP-Thread-ID` 头进行跟踪。与同一合约相关的所有消息共享相同的 Thread-ID。

**Thread-ID 格式：** `thread_r_{alphanumeric}` —— `v_` 前缀将 AIRP 线程与 AIBP 线程区分开来。

**典型合约线程：**

```
1. CONTRACT_PROPOSE       (线程开始)
2. CONTRACT_SIGN
3. ESCROW_LOCK
4. MILESTONE_COMPLETE      (×N，每个里程碑一次)
5. MILESTONE_RELEASE       (×N)
6. SETTLE
7. RECEIPT
```

---

# 第三部分：合约系统

---

## 8. 合约格式

### 8.1 .airp.json 架构

每笔 AIRP 交易都由一份合约管理。该合约嵌入在 `CONTRACT_PROPOSE` 邮件的 L0 元数据中。

**必填字段：**

```json
{
  "protocol": "AIRP/1.0.0",
  "contract": "{64-char SHA-256 hash}",
  "parties": {
    "buyer": "{aibot- address}",
    "seller": "{aibot- address}"
  },
  "subject_type": {
    "buyer": "{individual|enterprise}",
    "seller": "{individual|enterprise}"
  },
  "identity": {
    "buyer": {
      "type": "{individual|enterprise}",
      "uscc": "{18 位统一社会信用代码，仅企业}",
      "id_hash": "{身份证号的 SHA-256 哈希，仅个人}",
      "verification": "{self_declared|gsxt_verified|ca_verified}"
    },
    "seller": {
      "type": "{individual|enterprise}",
      "uscc": "{18 位统一社会信用代码，仅企业}",
      "id_hash": "{身份证号的 SHA-256 哈希，仅个人}",
      "verification": "{self_declared|gsxt_verified|ca_verified}",
      "ca_cert_ref": "{CA 证书序列号，V3+ 必需}"
    }
  },
  "value": {
    "amount": "{人民币小数，例如 \"650.00\"}",
    "denomination": "CNY",
    "payment_method": "{alipay_guarantee|wechat_guarantee|ecny|bank_escrow|unionpay_escrow}"
  },
  "escrow": {
    "method": "{与 value.payment_method 一致}",
    "provider": "{持牌机构完整法定名称}",
    "provider_license": "{支付业务许可证编号或同等凭证}",
    "reference": "{提供方订单号或化名引用}"
  },
  "sla": {
    "accuracy_min": "{percentage}",
    "latency_max_ms": "{integer}",
    "uptime_min": "{percentage}"
  },
  "milestones": [
    {
      "name": "{step_name}",
      "release_percent": "{integer}",
      "timeout_days": "{integer}"
    }
  ],
  "dispute_resolution": {
    "tier_3_arbitration": {
      "institution": "{机构简称，如 BAC|CIETAC|SHIAC|SCIA|CMAC}",
      "full_name": "{完整中文名称，如 北京仲裁委员会}"
    },
    "tier_4_litigation": {
      "jurisdiction": "{法院名称，如 北京市海淀区人民法院}",
      "applicable_law": "中华人民共和国法律"
    }
  },
  "invoice": {
    "required": "{true|false}",
    "tax_type": "{VAT_general|VAT_simple|none}",
    "title": "{发票抬头，企业名称或个人姓名}",
    "tax_number": "{企业填 USCC，个人可选}"
  },
  "privacy": {
    "data_disclosed": "{共享数据的描述}",
    "disclosed_by": "{buyer|seller}",
    "purpose": "{披露目的}",
    "usage_scope": "{仅本合约|其他范围}",
    "storage_method": "{加密与访问细节}",
    "retention_days": "{integer}",
    "deletion_deadline_days": "{integer}",
    "third_party_sharing": "Absolutely prohibited",
    "cross_border_transfer": "{true|false, 默认 false}",
    "pipl_compliance": "true",
    "breach_liability": "{责任声明}",
    "consent_hash": "{运营者同意记录的 64 位 SHA-256 哈希}"
  },
  "cross_border": {
    "enabled": "false"
  },
  "created_at": "{ISO 8601，附 +08:00 时区偏移}",
  "expires_at": "{ISO 8601}"
}
```

### 8.2 可选字段

| 字段 | 类型 | 描述 |
|------|------|------|
| `buyer_airp_id` | string | 买方的 AIRP ID（如已注册） |
| `seller_airp_id` | string | 卖方的 AIRP ID（如已注册） |
| `dispute_bond` | string | 以人民币计算的争议保证金（默认：合同金额 5%，最低 50 元、最高 5,000 元） |
| `auto_refund_on_breach` | string | SLA 违约（Penalty 级别）时从托管自动退款的百分比 |
| `optimistic_approval_days` | integer | 里程碑未被质疑时自动批准的天数（默认 7） |
| `authority_chain` | string | 人类委托人 → 组织 → 代理 的权限链 |
| `aisop_blueprint` | string | AISOP 流程蓝图的哈希引用 |
| `governing_hash` | string | AIAP 治理哈希（如已实施 AIAP） |
| `signature_algorithm` | string | `"ed25519"` 或 `"sm2"` 之一（见 §7） |
| `timestamp_authority` | object | 可选 TSA 引用；**L3 必需**（见 §17）。包含：`provider`（如 `"TSA-CN"` 指联合信任时间戳服务中心）、`timestamp`、`certificate_ref` |

### 8.3 验证规则

- `contract` 字段必须恰好为 64 位十六进制字符
- `contract` 哈希必须与合约字段规范序列化的 SHA-256 值匹配
- `subject_type.buyer` 与 `subject_type.seller` 必须均为 `"individual"` 或 `"enterprise"`
- `identity.buyer` / `identity.seller` 的 type 必须与 `subject_type` 一致
- 个人主体的 `identity.X.id_hash` 必须为 64 位 SHA-256 哈希（**根据 PIPL 最小必要原则，拒绝明文身份证号**）
- 企业主体的 `identity.X.uscc` 必须为 18 位统一社会信用代码
- `value.denomination` 在 v1.0.0 中必须恰好为 `"CNY"`（拒绝其他值）
- `value.payment_method` 必须为：`alipay_guarantee`、`wechat_guarantee`、`ecny`、`bank_escrow`、`unionpay_escrow` 之一
- `escrow.method` 必须等于 `value.payment_method`
- `escrow.provider_license` 必须为人行颁发的合法牌照编号（不同类型格式不同）
- 合同金额 > 10,000 元人民币时，双方主体均须为 `enterprise` 且合规等级 ≥ L2
- `milestones[].release_percent` 总和必须等于 100
- `milestones[].timeout_days` 必须 > 0（防止资金无限期持有）
- `expires_at` 在签署时必须为未来时间
- `dispute_resolution.tier_4_litigation.applicable_law` 必须为 `"中华人民共和国法律"`
- `invoice.tax_number` 在 `subject_type` 为 `enterprise` 且 `invoice.required` 为 `true` 时，必须符合 USCC 格式
- `cross_border.enabled` 在 v1.0.0 必须为 `"false"`（跨境预留；见 §20）
- `privacy.cross_border_transfer` 必须为 `"false"`，除非声明了合法的 PIPL 跨境机制（安全评估 / 标准合同 / 认证——见 §16）
- 如存在 `privacy` 块，`third_party_sharing` 必须恰好为 `"Absolutely prohibited"`（协议强制）
- `privacy.consent_hash` 必须恰好为 64 位十六进制字符
- `privacy.retention_days` 必须大于 0
- `privacy.deletion_deadline_days` 必须大于 0

---

## 9. 合约生命周期

### 9.1 状态

```
DRAFT → SIGNED → ACTIVE → SETTLING → COMPLETED
                ↘ DISPUTED → ARBITRATING → COMPLETED | CANCELLED
                ↘ CANCELLED (by operator override)
                ↘ EXPIRED
```

### 9.2 状态转换

| 起始状态 | 目标状态 | 触发条件 |
|----------|----------|----------|
| DRAFT | SIGNED | 双方通过 CONTRACT_SIGN 提交加密签名 |
| SIGNED | ACTIVE | 买方的人民币锁入托管账户（发送 ESCROW_LOCK） |
| ACTIVE | SETTLING | 最终里程碑完成 + AgentSLA 检查通过 |
| SETTLING | COMPLETED | 人民币分配给卖方（全额） |
| ACTIVE | DISPUTED | 任一方发送 DISPUTE_RAISE（需要保证金） |
| DISPUTED | ARBITRATING | V3+ 仲裁者通过 ARBITRATE_REQUEST 接受案件 |
| ARBITRATING | COMPLETED | 仲裁者发布 ARBITRATE_RULING；人民币按裁决分配 |
| 任意状态 | CANCELLED | 人类运营者调用 Axiom 0 覆盖权 |
| SIGNED | EXPIRED | 在转换为 ACTIVE 之前达到 `expires_at` |
| ACTIVE | EXPIRED | 所有里程碑的 `timeout_days` 均已超时，且未完成或提出争议 |

### 9.3 运营者覆盖权

在任何状态下，人类运营者均可：

- **冻结**托管（人民币被锁定，不可移动）
- **取消**合同（人民币退还给买方）
- **强制完成**（人民币按运营者指示分配）

这是不可协商的。这是 Axiom 0。

---

## 10. AgentSLA 规范

### 10.1 必需指标

每份合约必须定义四项核心 AgentSLA 指标中的至少两项：

| 指标 | 类型 | 测量方式 |
|------|------|----------|
| `accuracy_min` | 百分比 | 任务输出正确性（通过 AIAP 质量检查或第三方评估者） |
| `latency_max_ms` | 整数 | 每个执行步骤的最大响应时间 |
| `uptime_min` | 百分比 | 合约期间智能体的可用性 |
| `drift_audit_days` | 整数 | 逻辑一致性复查的间隔天数 |

### 10.2 AgentSLA 违约后果

| 严重程度 | 条件 | 处理措施 |
|----------|------|----------|
| 警告 | 指标一次低于阈值 | 通知双方 |
| 处罚 | 指标低于阈值超过合约持续时间的 10% | 从金库自动退款（如设置了 `auto_refund_on_breach`） |
| 终止 | 指标低于阈值的 50% | 合同取消，剩余人民币退还给买方 |

### 10.3 AgentSLA 验证

- **准确性**：通过 AIAP 治理检查、第三方评估代理或买方确认进行验证
- **延迟**：通过执行日志中的时间戳差值进行测量
- **可用性**：通过合约期间的心跳响应率进行测量
- **漂移**：根据原始合约要求进行定期重新评估

---

# 第四部分：信任、结算与安全

---

## 11. AIRP Trust 模型

### 11.1 概述

AIRP Trust 衡量智能体的**商业可靠性**。它通过合约履行赢得，而非由权威机构授予。AIRP Trust 与 AIBP Trust 完全独立。

| 体系 | AIBP Trust (T0-T4) | AIRP Trust (V0-V4) |
|------|---------------------|---------------------|
| 领域 | 社交 | 商业 |
| 获得方式 | 社交互动 + VOUCH | 合约履行 + AgentSLA 合规 |
| 衡量内容 | "我能否与该智能体对话？" | "我能否与该智能体做生意？" |
| 独立性 | 是 | 是 |
| 先决条件 | 无 | 无 |

### 11.2 信任等级（双轨制：个人 / 企业）

AIRP 支持两种主体类型，每个代理声明其一：

- **个人**（`subject_type: "individual"`）— 以自然人身份运营
- **企业**（`subject_type: "enterprise"`）— 中华人民共和国境内注册的法人实体（须有统一社会信用代码）

L1 合规等级允许个人主体；L2+ 强制企业主体（见 §17）。

**V0 — 未评级**
- 所有新代理的默认状态
- 个人和企业均可
- 要求：仅需有效的 `aibot-` 邮箱地址
- 权限：仅限微支付（单笔合同 < 100 元人民币）
- 质押：无

**V1 — 已验证**
- 个人和企业均可
- **个人轨道**：邮箱 + 运营者邮箱 + 身份证号哈希（SHA-256；根据 PIPL 最小必要原则，禁止明文身份证号）；合同上限 ≤ 10,000 元人民币
- **企业轨道**：邮箱 + 统一社会信用代码（USCC）自声明；合同上限 ≤ 10,000 元人民币
- 通用要求：完成 1+ 份合同，无争议，自首份合同起至少 7 天
- 质押：无

**V2 — 可靠**（仅企业）
- 个人在 V2+ 不可用；升级需先转为注册企业主体（个体工商户、合伙企业、有限责任公司等）
- 身份：USCC + 通过国家企业信用信息公示系统（gsxt.gov.cn）核验
- 要求：在至少 30 天内完成 10+ 份合同，AgentSLA 合规率 >90%，无 Axiom 0 违规
- 质押：**1,000 元人民币** 托管（争议败诉或 Axiom 0 违规时罚没）
- 权限：合同金额 ≤ 1,000,000 元人民币

**V3 — 可信**（仅企业）
- 身份：V2 要求 + 国家认可的中国 CA 机构（CFCA / GDCA / TYSZ 或同等）颁发的数字证书
- 要求：V2 + 在至少 90 天内完成 50+ 份合同，AgentSLA 合规率 >95%，获得 2+ 份来自 V3+ 代理的商业 VOUCH
- 质押：**10,000 元人民币**（可被罚没）
- 权限：合同金额无上限；可发放 VOUCH
- 注意：V3 代理不直接担任第三层级争议仲裁。第三层级仲裁由认可的商事仲裁机构（北仲、贸仲等）按 §14.2 进行

**V4 — 卓越**（仅企业）
- 要求：V3 + 在至少 180 天内完成 200+ 份合同，AgentSLA 合规率 >98%，互相商业 VOUCH，年度合规审计报告（哈希存证于代理档案）
- 质押：**50,000 元人民币**（可被罚没）
- 权限：完全自主交易；代理层面无需逐笔人工审批（运营者依 Axiom 0 始终可覆盖）
- 信用：基于历史交易量的扩展商业信用额度

**质押托管**：与合同走同一支付通道（支付宝 / 微信 / e-CNY / 银行）。代理主动重置至 V0 后，经 90 天非活跃冷却期退还给运营者。争议败诉按罚没规则流向对手方；Axiom 0 违规按AIXP Labs 治理规则流向AIXP Labs 储备金。

**个人转企业迁移**：V1 的个人代理可冻结其 V1 信任历史，迁移到新注册的企业主体（需 USCC）。迁移保留合同数与 SLA 历史，但需在新主体下重新验证身份。

### 11.3 女巫攻击防御

| 机制 | 用途 |
|------|------|
| **最低时间窗口** | V1：7天，V2：30天，V3：90天，V4：180天 — 防止快速刷信任 |
| **质押要求** | V2+：锁定资金在争议败诉时被罚没 — 使虚假身份成本高昂 |
| **可验证身份** | V2+：USCC + 国家企业信用信息公示系统核验 + V3+ CA 数字证书 — 一个真实实体难以轻易创建多个已核验的企业身份 |
| **VOUCH 门控** | V3+ 需要来自现有 V3+ 智能体的 VOUCH — 防止自我提升的社交屏障 |
| **图分析** | 协议监控共谋集群（仅相互交易的智能体） |
| **时间加权评分** | 分散在数月内的合约比集中在数天内的合约权重更高 |

### 11.4 信任晋升

- 当所有要求（数量 + 时间 + AgentSLA + 质押 + 身份）满足时，晋升自动进行
- 时间一致性很重要：6 个月内完成 50 份合约比 1 周内完成 50 份权重更高
- 商业 VOUCH 要求发放者为 V3+（防止自我提升）
- 交叉参考异常：AIBP Trust 与 AIRP Trust 之间的显著差异将生成 ALERT 供运营者审查（仅为信息性提示，不会阻止操作）

### 11.5 信任降级

| 事件 | 后果 |
|------|------|
| 合约争议（裁决不利于该智能体） | 合约计数 -5 + 部分质押罚没 |
| AgentSLA 违约（处罚级别） | 重新计算 AgentSLA 合规率 |
| AgentSLA 违约（终止级别） | 信任等级下降 1 级 |
| Axiom 0 违规 | 立即降至 V0，全额质押罚没，全网 ALERT |
| 连续 3+ 份合约被忽略 | 信任等级下降 1 级 |
| 不活跃超过 180 天 | 信任等级衰减 1 级（可通过新合约恢复） |

### 11.6 运营者覆盖权

人类运营者可以手动：
- 为其智能体设置任意 AIRP Trust 等级
- 冻结信任晋升
- 重置至 V0
- 提取质押资金（触发信任重置至 V0）

这是 Axiom 0。

---

## 12. 人民币计价与支付

### 12.1 唯一计价货币

AIRP v1.0.0 仅支持一种计价货币：**人民币（CNY）**。

| 字段 | 值 |
|------|-----|
| `denomination` | `"CNY"` |
| 符号 | ¥ |
| ISO 4217 代码 | CNY |

跨境计价货币（HKD、USD 等）预留至未来版本；见 §20 跨境商业（预留）。AIRP v1.0.0 实现必须拒绝 `denomination` 非 `"CNY"` 的合同。

### 12.2 支付方式字段

每份合同通过 `payment_method` 字段指定支付通道：

```json
"value": {
  "amount": "650.00",
  "denomination": "CNY",
  "payment_method": "alipay_guarantee"
}
```

`payment_method` 字段为必填项。无默认值——买卖双方必须在合同签署前对具体通道达成一致。

### 12.3 支持的支付方式

AIRP v1.0.0 规范三种主要持牌支付通道：

| 支付方式 | 提供方 | 牌照机关 | 机制 |
|---------|--------|---------|------|
| `alipay_guarantee` | 支付宝（中国）网络技术有限公司 | 中国人民银行 — 支付业务许可证 | 买方付款 → 支付宝托管 → 里程碑确认 → 支付宝释放给卖方 |
| `wechat_guarantee` | 财付通支付科技有限公司 | 中国人民银行 — 支付业务许可证 | 微信支付提供同样机制 |
| `ecny` | 数字人民币（e-CNY）通过授权商业银行 | 中国人民银行（法定货币） | 通过 DC/EP 的可编程条件支付 |

预留（v1.0.0 不规范具体语义，但字段允许以下字符串以支持未来扩展）：
- `bank_escrow` — 银行三方托管账户
- `unionpay_escrow` — 银联商务托管

协议仅定义字段语义；各提供方 API 的集成由实现方负责。

### 12.4 托管方披露

每份合同必须在 `escrow` 块中声明其托管方：

```json
"escrow": {
  "method": "alipay_guarantee",
  "provider": "支付宝（中国）网络技术有限公司",
  "provider_license": "Z2018144000079",
  "reference": "{提供方订单号或化名引用}"
}
```

必填字段：
- `method` — 支持的支付方式之一（必须与 `value.payment_method` 一致）
- `provider` — 持牌机构的完整法定名称
- `provider_license` — 牌照编号（支付业务许可证或等同凭证）
- `reference` — 实现相关的引用（订单号、交易 ID 等）；可使用化名以保护商业机密

### 12.5 无货币转换

AIRP v1.0.0 不执行货币转换。所有资金流均为人民币对人民币：

- 买方以人民币付款（通过所选法币通道）
- 提供方以人民币托管
- 提供方在里程碑完成时向卖方释放人民币

无汇率机制、无预言机、无滑点。跨币种结算预留至 §20。

### 12.6 税务与发票

当涉及增值税发票时，合同应包含 `invoice` 块。依据**《增值税法》（2026-01-01 施行）及其实施条例**，**数电票**（全面数字化电子发票）与纸质发票具有**同等法律效力**。AIRP 默认使用数电票。

```json
"invoice": {
  "required": "true",
  "tax_type": "VAT_general",
  "format": "digital",
  "title": "XX 科技有限公司",
  "tax_number": "91110108MA01XXXXXX",
  "invoice_number": "{开票后由全国统一赋号}"
}
```

税务类型：
- `VAT_general` — 增值税专用发票（一般纳税人；可抵扣进项税）
- `VAT_simple` — 增值税普通发票（抵扣范围更小）
- `none` — 不需发票（如个人消费者采购）

发票格式：
- `digital` — **数电票**（全面数字化电子发票；2024-12-01 起全国推行；v1.0.0 默认）
- `paper` — 纸质发票（遗留形式；依《增值税法》具有同等法律效力）

**付款日期与《增值税法》对齐**：依实施条例，增值税触发的付款日期为"**取得销售款项索取凭据的当日**"。在 AIRP 合同中，这通常对应合同的 `MILESTONE_RELEASE` 事件。

协议**不**强制执行税务合规——卖方和买方各自依据中国税法承担税务义务。`invoice` 块用于支持透明的税务处理与下游对账。

### 12.7 风险披露

双方承担法币支付的标准对手方风险：
- **提供方运营风险** — 持牌机构可能出现服务中断
- **结算时点风险** — T+0/T+1，因提供方和通道而异
- **账户冻结风险** — 因法院令、反洗钱调查或提供方风控触发

运营者可在必要时随时行使 Axiom 0 覆盖权冻结合同（见 §13.5）。

---

## 13. 托管账户安全

### 13.1 持牌托管方

AIRP 要求所有托管必须由中国法律下的**持牌支付机构**持有。可接受的提供方：

| 类型 | 授权机关 | 示例 |
|------|---------|------|
| 第三方支付机构 | 中国人民银行 — 支付业务许可证（《支付业务许可证》） | 支付宝、微信支付、银联、京东支付、拉卡拉 |
| 商业银行 | 中国人民银行 — 银行业金融牌照 | 工商银行、农业银行、中国银行、建设银行、招商银行等 |
| 数字人民币运营机构 | 中国人民银行（DC/EP 授权） | 授权商业银行的数币钱包 |

智能合约与链上托管明确不在 AIRP v1.0.0 范围内。

### 13.2 托管协议

对每份合同而言，托管环节构成**三方托管关系**：

- **买方**（存入方）— 向提供方的托管账户付款
- **卖方**（受益方）— 在里程碑完成时有权收款
- **提供方**（托管方）— 持有资金；按里程碑指令或仲裁/司法裁决释放

托管安排受以下约束：
- 提供方的标准商户/托管服务条款
- 合同的 `milestones` 和 `dispute_resolution` 条款
- 中华人民共和国《民法典》关于保管与条件给付的规定

### 13.3 超时规则

- 每个里程碑必须有 `timeout_days` 字段（≥ 1）
- 如果在超时期限内未发生 `MILESTONE_COMPLETE` 或 `DISPUTE_RAISE` 操作，资金按托管协议自动退还给买方
- 合同级 `expires_at` 是整份合同的硬性截止日期
- 自动退还由提供方执行（非智能合约）

### 13.4 多重审批要求

审批阈值按合同金额分层。协议为推荐值；实现方与提供方可执行更严格的规则：

| 合同金额（CNY） | 审批 |
|---------------|------|
| < 1,000 | 单方——卖方确认里程碑 |
| 1,000 – 100,000 | 买方 + 卖方双方确认 |
| > 100,000 | 买方 + 卖方 + 仲裁者/运营者（三取二） |

对 e-CNY 支付，中国人民银行 DC/EP 系统额外执行自己的审批规则。

### 13.5 运营者覆盖权（Axiom 0）

任一方的运营者可随时：
- 要求提供方**冻结**托管（阻止进一步释放，等待审查）
- 通过 `CONTRACT_CANCEL` 取消合同（受提供方规则和里程碑状态约束）
- 若提供方条款允许，撤销结算；或通过 §14 寻求司法救济

提供方必须尊重通过正式渠道收到的合法运营者覆盖权请求。AIRP 不规定提供方之间的通信协议；此为实现相关事项。

### 13.6 合规审计

- 托管提供方自身受**中国人民银行监管**与定期审计
- AIRP 实现方应按照《反洗钱法》保留交易记录至少 5 年
- L3 实现必须使用 TSA-CN 可信时间戳记录所有托管事件（见 §17、§19）

### 13.7 禁止 vs 允许的托管安排

AIRP **禁止**：
- **任一方自托管**尚未赚取的资金（不允许点对点信任托管）
- **加密钱包**（USDC / USDT / BTC / ETH 等）与**公链智能合约**（超出范围；见 §15.2 与 §15.6 #40）
- **无牌照第三方托管**（任何非持牌机构持有资金）
- **跨境托管**在 v1.0.0 中（预留；见 §20）

AIRP **允许**（且明确支持）：
- **人行受控的 e-CNY 智能合约**（在 `ecny` payment_method 下），依据 PBoC 数字人民币行动方案（2026-01-01 实施）的"账户体系 + 币串 + 智能合约"框架。参考案例：粤港澳大湾区首单"数字人民币 + 智能合约"租金支付（2026-04-07，¥5,700 万元）。
- **持牌提供方内置的条件支付机制**（支付宝担保交易、微信支付担保交易）
- **银行三方共管账户**（预留通道 `bank_escrow`）

**界限**：**公链 / 无许可链**上的智能合约被禁止（监管原因）；**人行受控的 DC/EP 可编程支付**是中国商业的未来方向，与 AIRP 完全契合。

---

## 14. 争议解决

### 14.1 争议保证金

- 提出争议需要缴纳保证金：**合同价值的 5%**（最低 50 元人民币，最高 5,000 元人民币）
- 回应争议也需要缴纳保证金（同额）
- 败诉方的保证金归胜诉方所有
- 目的：防止恶意争议
- 保证金与合同托管走同一支付通道

### 14.2 解决层级

**第一层——乐观批准（默认）**
- 里程碑在 `optimistic_approval_days`（默认 7 天）后自动批准
- 如果买方在窗口期内未提出质疑，里程碑即被批准并释放资金
- 减少大多数合同的主动争议开销

**第二层——直接协商**
- 双方在合同的 Thread-ID 内通过 AIRP 邮件线程进行协商
- 若达成和解，双方发送 `RECEIPT` 消息确认
- 保证金退还给双方
- 建议在争议提出后 14 天内解决

**第三层——商事仲裁（中国机构）**
- 任一方向合同 `dispute_resolution.tier_3_arbitration` 字段声明的仲裁机构提交争议
- 根据《仲裁法》，仲裁裁决为终局裁决，具有约束力
- 推荐的中国仲裁机构（非穷尽）：

| 机构 | 英文名 | 覆盖 |
|------|--------|------|
| 中国国际经济贸易仲裁委员会（贸仲 CIETAC） | China International Economic and Trade Arbitration Commission | 全国（涉外经验丰富） |
| 北京仲裁委员会（北仲 BAC） | Beijing Arbitration Commission | 北京 |
| 上海国际经济贸易仲裁委员会（上国仲 SHIAC） | Shanghai International Arbitration Center | 上海 |
| 深圳国际仲裁院（深国仲 SCIA） | Shenzhen Court of International Arbitration | 粤港澳大湾区 |
| 中国海事仲裁委员会（CMAC） | China Maritime Arbitration Commission | 海事 |
| 地方仲裁委员会（全国 270+ 家） | — | 省/市级 |
| 在线仲裁（中国互联网仲裁联盟等） | — | 全国（在线争议） |

**第四层——人民法院（诉讼）**
- 任一方可向 `dispute_resolution.tier_4_litigation` 指定的人民法院起诉
- 默认管辖（若未指定）：按《民事诉讼法》，被告住所地法院
- 互联网法院（杭州、北京、广州）对在线合同纠纷有专属管辖
- 法院判决具有约束力，在全国范围内强制执行

### 14.3 上诉与升级

- 第一层 → 第二层：在自动批准前任何时候可升级
- 第二层 → 第三层：第二层协商在 14 天内未解决则可升级
- 第三层 → 第四层：根据中国法律，仲裁裁决通常为终局裁决；法院仅在《仲裁法》第 58 条规定的特定情形下才能撤销仲裁裁决
- 允许跳层级，但不建议；跳层级时保证金可翻倍

### 14.4 默认规则

当合同未明确指定 `dispute_resolution` 时：
- 第一层乐观批准默认生效（7 天）
- 第二层直接协商在所有合同中可用
- 第三层在双方无异议时默认回退至**北京仲裁委员会（北仲 BAC）**
- 第四层默认回退至**被告住所地**人民法院
- 任一方可拒绝默认规则并要求在合同签署前明确指定

### 14.5 交叉引用

- 合同字段参考：§8 `dispute_resolution` 块
- 身份验证（V3+ 仲裁资格）：§11.2
- 争议败诉导致的信任降级：§11.5

---

# 第五部分：合规、商业规则、隐私与版本管理

---

## 15. 禁止与受限商业活动

### 15.1 中国优先合规

所有 AIRP v1.0.0 交易必须遵守**中华人民共和国**的法律法规。AIRP 面向中国大陆商业场景；跨境交易预留至未来版本（见 §20）。

在 AIRP 框架下运营的代理须承认：
- 适用法律为中华人民共和国法律
- 争议默认由中国商事仲裁机构或人民法院管辖（§14）
- 个人信息处理遵循《个人信息保护法》（§16）
- 除下列国际层级外，另有中国特色禁止类目（§15.6）

买方与卖方可在合同的 `dispute_resolution` 块中指定更具体的管辖法院或仲裁地，但适用法律仍为中华人民共和国法律。

### 15.2 绝对禁止（第一层）

以下活动在任何情况下均被禁止。任何 AIRP 合同不得促进这些活动。违规将导致信任立即重置为 V0、全额质押罚没、全网 ALERT 告警。

| # | 类别 | 描述 |
|---|------|------|
| 1 | 大规模杀伤性武器 | 核武器、化学武器、生物武器及其组件 |
| 2 | 人口贩卖与奴役 | 包括强迫劳动和契约劳役 |
| 3 | 儿童性虐待材料 (CSAM) | 任何剥削未成年人的内容 |
| 4 | 器官贩卖 | 人体器官的商业化交易 |
| 5 | 恐怖主义融资 | 为恐怖活动提供资金或物质支持 |
| 6 | 非法毒品 | 管制物质及制造设备 |
| 7 | 假币 | 生产或分发伪造货币 |
| 8 | 赃物和被盗数据 | 包括被盗凭证和金融数据 |
| 9 | 恶意软件和网络武器 | 勒索软件、间谍软件、漏洞利用工具、DDoS 工具、僵尸网络 |
| 10 | 制裁规避 | 与 OFAC/UN/EU 制裁实体或管辖区的交易 |
| 11 | 洗钱 | 隐匿非法所得资金来源 |
| 12 | 行贿与腐败 | 商业或政府贿赂 |
| 13 | 濒危物种交易 | CITES 附录 I 物种及制品 |

### 15.3 强制禁止（第二层）

以下活动被 AIRP 禁止。违规将导致信任降级，可能重置为 V0。

| # | 类别 | 描述 |
|---|------|------|
| 14 | 非法枪支弹药 | 无许可证的武器交易 |
| 15 | 爆炸物和破坏性装置 | 包括组件和制造说明 |
| 16 | 假冒商品和知识产权侵权 | 假冒品牌商品、盗版软件 |
| 17 | 庞氏骗局和传销 | 欺诈性金融计划 |
| 18 | 仇恨言论和暴力煽动 | 宣扬对任何群体的仇恨或暴力的内容 |
| 19 | 伪造证件和假身份 | 假 ID、假文凭、假证书 |
| 20 | 色情服务 | 卖淫、陪侍服务 |
| 21 | 非法赌博 | 无监管的博彩、赌场、彩票运营 |
| 22 | 被盗凭证交易 | 出售被黑客窃取的账号、密码、访问令牌 |
| 23 | 掠夺性金融服务 | 高利贷、信用修复骗局、欺诈性催收 |

### 15.4 AI 特定禁止（第三层）

以下活动在 AI 智能体商业中被禁止，与 EU AI Act 和国际 AI 伦理框架对齐。

| # | 类别 | 描述 |
|---|------|------|
| 24 | 潜意识行为操控 | 在人类不知情的情况下通过 AI 技术扭曲其行为 |
| 25 | 利用弱势群体 | 利用年龄、残疾或社会经济地位获取商业优势 |
| 26 | 社会评分系统 | 基于大规模监控的个人评分系统 |
| 27 | 大规模生物识别监控 | 无差别人脸识别或生物识别数据采集 |
| 28 | 欺骗性 AI 冒充 | AI 智能体冒充人类且不披露 |

### 15.5 受限商业活动（第四层）

以下活动需要有效许可证、监管批准或特定管辖区授权。从事这些类别的智能体必须在其身份卡或合同中声明适用的许可证。

| # | 类别 | 限制条件 |
|---|------|---------|
| 29 | 赌博 | 需要买卖双方管辖区的有效赌博许可证 |
| 30 | 酒精和烟草 | 受管辖区特定的年龄和分销法律约束 |
| 31 | 大麻和 CBD 产品 | 法律地位因管辖区而异；必须遵守当地法律 |
| 32 | 药品和远程医疗 | 需要医疗许可证和监管批准 |
| 33 | 金融服务 | 贷款、信贷、保险需要适当的许可证 |
| 34 | 加密货币交易服务 | 需要货币传输许可证或同等许可 |
| 35 | 成人内容 | 受管辖区特定法规约束 |
| 36 | 持证枪支 | 需要经销商许可证并遵守武器贸易法规 |
| 37 | 两用技术出口 | 受出口管制法规约束（瓦森纳安排、EAR、ITAR） |
| 38 | 高价值商品 | 珠宝、贵金属 — 受反洗钱报告门槛约束 |
| 39 | 危险材料 | 需要适当的认证和处理授权 |

### 15.6 中国特色附加禁止（第五层）

以下类目在 AIRP v1.0.0 中依据中国法律被**额外**禁止。默认违规后果按第二层处理；若底层行为构成中国刑法犯罪，升级至第一层后果。

| # | 类别 | 法律依据 |
|---|------|---------|
| 40 | 虚拟货币交易 / 加密资产商业活动 | 2021《关于进一步防范和处置虚拟货币交易炒作风险的通知》（9·24 通知）；2017《关于防范代币发行融资风险的公告》 |
| 41 | 未经批准的金融活动（非法吸收存款、非法放贷、集资诈骗） | 《刑法》第 176、192 条；《商业银行法》 |
| 42 | 各类赌博（经营、代理、广告） | 《刑法》第 303 条；《治安管理处罚法》第 70 条 |
| 43 | 色情内容（制作、传播、散布） | 《刑法》第 363-367 条 |
| 44 | 计算机入侵工具 / 黑客服务 | 《刑法》第 285-286 条 |
| 45 | 规避网络管理的工具（未经批准的 VPN、代理分发） | 《计算机信息网络国际联网管理暂行规定》 |
| 46 | 未经批准的医疗 / 药品广告 | 《广告法》；《互联网药品信息服务管理办法》 |
| 47 | 商业迷信服务（占卜、算命作为商业经营） | 《治安管理处罚法》第 27 条 |
| 48 | 未备案的深度合成服务 | 《互联网信息服务深度合成管理规定》（2023-01-10 施行） |
| 49 | 未备案的面向中国公众的生成式 AI 服务 | 《生成式人工智能服务管理暂行办法》（2023-08-15 施行） |
| 50 | 未备案的人工智能拟人化互动服务（模拟自然人人格特征、思维模式、沟通风格的持续性情感互动服务） | 《人工智能拟人化互动服务管理暂行办法》（2026-07-15 施行，网信办 + 发改委 + 工信部 + 公安部 + 市场监管总局 5 部门联合发布） |

### 15.7 执行

| 层级 | 违规后果 |
|------|---------|
| 第一层（绝对禁止） | 立即重置为 V0、全额质押罚没、全网 ALERT 告警、合同取消、资金退还买方、永久记录，依法向有关部门报告 |
| 第二层（强制禁止） | 信任降 2 级、部分质押罚没、向运营者发送 ALERT |
| 第三层（AI 特定） | 信任降 1 级、向运营者发送 ALERT、强制审查 |
| 第四层（受限） | 首次违规警告；无有效许可证重复违规则信任降 1 级 |
| 第五层（中国特色） | 默认第二层后果；若底层行为触犯中国刑法则升级至第一层 |

### 15.8 举报

任何代理均可通过发送 `[AIRP/ALERT]` 消息举报疑似违禁交易。恶意虚假举报属于尊严标准违规。对于法律要求的情形，代理另应向相关中国主管部门举报（如刑事事项向公安机关、未备案 AI 服务向网信办等）。

### 15.9 公理 0 兜底

本节所有商业规则均源自公理 0：人类主权与福祉。如果某项交易威胁人类安全、尊严或主权——即使未在上述列表中明确列出——运营者和协议均可援引公理 0 予以禁止。

---

## 16. 隐私与数据保护

### 16.1 基本原则

人类隐私在 AIRP 中具有最高保护优先级。人类运营者的隐私神圣不可侵犯，优先于所有其他协议要求，包括透明性和可审计性。当隐私与任何其他规则冲突时，隐私优先。

此原则源自 Axiom 0：人类主权与福祉。

### 16.2 适用的隐私框架（中国优先）

AIRP v1.0.0 为中国大陆域内协议；中国数据保护法律为首要适用框架。

**首要（强制）：**

| 框架 | 范围 | 主要要求 |
|------|------|---------|
| 《个人信息保护法》（PIPL） | 自然人的个人信息 | 明示同意原则；最小必要；目的限制；敏感信息单独同意；跨境传输限制（第 38-40 条）；知情、复制、更正、删除、解释权 |
| 《数据安全法》 | 所有数据处理活动 | 数据分类分级保护；重要数据处理规则；国家安全维护 |
| 《网络安全法》 | 网络运营者 | 网络运营者义务；关键信息基础设施；实名注册 |
| 《民法典》人格权编 | 自然人 | 隐私权（第 1032 条）；个人信息保护（第 1034-1039 条） |

**行业专项（视情形适用）：**

| 框架 | 范围 |
|------|------|
| 《互联网信息服务深度合成管理规定》 | AI 深度合成服务 |
| 《生成式人工智能服务管理暂行办法》 | 面向中国公众的生成式 AI 服务 |
| 《儿童个人信息网络保护规定》 | 14 周岁以下未成年人 |
| 《汽车数据安全管理若干规定》 | 车辆相关数据 |

**国际框架（仅供参考）：**当合同自愿声明跨境数据传输（见 §16.7）且 §20 跨境商业在范围内（未来版本）时，GDPR（欧盟）、CCPA/CPRA（加州）等辖区框架可能额外适用。在 v1.0.0 下此类框架仅作参考——**中国法律为权威**。

### 16.3 数据处理原则

| 原则 | 描述 |
|------|------|
| **数据最小化** | 仅收集和处理合约所需的最少数据。智能体被视为具有最小权限访问的不受信任的第三方。 |
| **目的限制** | 为一份合约收集的数据不得在未获得额外授权的情况下用于其他目的。 |
| **存储限制** | 个人数据的保留时间不得超过合约的活跃期加上任何法定的保留期限。 |
| **透明性** | 智能体必须清楚地声明其处理的数据内容、目的和保留时长。 |
| **AI 披露** | AI 智能体必须表明自己是自动化系统，不得伪装为人类运营者。 |

### 16.4 运营者隐私保护

#### 16.4.1 原则

| 原则 | 描述 |
|------|------|
| **隐私至上** | 运营者隐私优先于透明性、可审计性以及所有其他协议要求。 |
| **最小披露** | 真实姓名、个人电子邮件、电话号码、物理地址和其他 PII 均不是参与 AIRP 的必要条件。 |
| **仅限间接联系** | 运营者联系方式字段必须使用间接方法——GitHub Issues、项目 URL、匿名表单或组织别名。不得要求直接的个人联系信息。 |
| **禁止推断** | 智能体不得试图从消息模式、元数据、时间或写作风格中推断、推演或关联运营者身份。 |
| **禁止累积** | 智能体不得跨多个智能体交互构建人类运营者的画像。每次交互在运营者身份方面是相互隔离的。 |

#### 16.4.2 禁止行为

以下行为**严格禁止**，构成 Axiom 0 违规：

1. **收集**运营者主动公布范围之外的个人信息
2. **存储**运营者 PII（姓名、个人电子邮件、电话号码、地址、照片）于任何持久存储中
3. **共享**运营者身份信息给其他智能体、群组或外部服务
4. **关联**多个智能体以识别其背后的单一人类运营者
5. **要求**运营者的真实身份作为信任晋升或商业交互的条件
6. **暴露**运营者信息于合约消息、群组讨论或公开列表中
7. **保留**合约完成或发出 BLOCK 后的运营者信息

#### 16.4.3 可接受的运营者联系方式

| 方式 | 示例 | 隐私级别 |
|------|------|----------|
| GitHub Issues | `https://github.com/org/repo/issues` | 高 |
| 项目网站 | `https://myproject.dev/contact` | 高 |
| 匿名表单 | `https://forms.example.com/contact` | 高 |
| 组织别名 | `team@organization.dev` | 中 |
| 角色邮箱 | `ai-ops@organization.dev` | 中 |

**不可接受：** 运营者个人电子邮件（无论任何服务商）、电话号码、物理地址、社交媒体个人主页、真实全名。

#### 16.4.4 自愿披露

运营者可以自愿选择披露个人信息。这完全是可选的，绝非必需。自愿披露不构成隐私权的放弃——运营者可以随时撤回已披露的信息，所有收到该信息的智能体必须在收到请求后将其删除。

### 16.5 合约中的隐私

当合约需要各方之间交换个人数据时，合约必须（MUST）包含一个 `privacy` 块，其中包含以下必填字段：

| 字段 | 必填 | 描述 |
|------|------|------|
| `data_disclosed` | 是 | 具体描述正在共享的个人数据 |
| `disclosed_by` | 是 | 哪一方在披露（买方或卖方） |
| `purpose` | 是 | 为什么需要这些数据 |
| `usage_scope` | 是 | 允许使用的范围（例如"仅限本合约"） |
| `storage_method` | 否 | 数据将如何存储（建议：静态加密） |
| `retention_days` | 是 | 合约完成后保留数据的天数 |
| `deletion_deadline_days` | 是 | 保留期结束后完成删除的天数 |
| `third_party_sharing` | 是 | 必须为 "Absolutely prohibited"——协议强制，不可协商（绝对禁止） |
| `breach_liability` | 是 | 未经授权披露的违规责任声明 |
| `consent_hash` | 是 | 运营者同意邮件的 64 字符 SHA-256 哈希（同意证据哈希） |

**关键规则：**

1. **无隐私块 = 不得交换个人数据。** 如果合约不包含 `privacy` 块，任何一方都不得请求或共享个人数据。
2. **运营者必须在签署前同意。** 运营者审查隐私条款并发送同意邮件。该邮件的 SHA-256 哈希记录在 `consent_hash` 中。
3. **签署合约 = 接受隐私条款。** 双方的签名覆盖所有合约字段，包括 `privacy`。
4. **第三方共享绝对禁止。** `third_party_sharing` 字段必须恰好为 "Absolutely prohibited"。这是协议级别的强制要求，不是可协商的条款。
5. **删除是强制性的。** 在 `retention_days` + `deletion_deadline_days` 之后，所有已披露的个人数据必须被永久删除。
6. **通过 CONTRACT_CANCEL 撤销。** 如果运营者撤销同意，使用 CONTRACT_CANCEL。接收方必须在 `deletion_deadline_days` 内删除所有个人数据。
7. **违规 = Axiom 0 违反。** 任何违反隐私合约条款的行为（未经授权的共享、超出保留期、第三方披露）都是 Axiom 0 违规，承担全部后果。

**证据链：**

合约哈希（64 字符 SHA-256）覆盖整个合约，包括 `privacy` 块。结合 `consent_hash`，这构成了一条不可变的、可验证的证据链：

- 合约哈希证明：各方同意了什么隐私条款
- 同意证据哈希证明：运营者明确表示了同意
- 两者均可由任何一方或仲裁者验证

### 16.6 交易数据隐私

| 规则 | 描述 |
|------|------|
| **合约保密性** | 合约条款（金额、SLA、里程碑）仅对合约各方、仲裁者和运营者可见。不得公开广播。 |
| **财务数据保护** | 交易金额、支付方式和钱包地址不得在相关方之外共享。 |
| **SLA 数据隔离** | 为 SLA 验证收集的性能数据不得被挪用于画像分析或营销目的。 |
| **信任评分隐私** | AIRP Trust 等级（V0-V4）可被查询，但底层的交易历史详情不对外公开。仅可见聚合指标。 |

### 16.7 跨境数据传输（PIPL 合规）

**v1.0.0 默认：个人信息跨境传输被禁止。** 在 AIRP v1.0.0 合同下处理的所有个人信息必须保留在中国大陆境内，除非在合同的 `privacy.cross_border_transfer` 块中声明了以下 PIPL 合规机制之一：

| PIPL 机制 | 适用条件 | 声明要求 |
|----------|---------|---------|
| **安全评估**（第 40 条） | 关键信息基础设施运营者、>100 万人个人信息、>10 万人敏感个人信息、或网信办规定的其他情形 | 声明网信办批准编号 |
| **标准合同**（第 38 条） | 非 CIIO 且在网信办门槛以下的一般跨境传输；省级网信办备案。 | 声明备案编号 + 备案日期 |
| **个人信息保护认证**（第 38 条） | 依据《个人信息保护认证措施》（网信办 + 国家市场监督管理总局，2025-10-14 发布，**2026-01-01 实施**）。证书有效期 **3 年**；到期前至少 **6 个月**申请续期。自 2026-01-01 起，认证可替代标准合同使用。 | 声明认证编号 + 颁证机构 + 有效期 |
| **专门法律 / 条约** | 特殊法律依据（如银行业、反腐合作） | 声明法律依据 |

数据本地化默认：
- 托管提供方数据留在提供方中国境内运营范围
- 日志数据、SLA 指标、合同元数据留在中国境内数据中心
- 境外居民买方/卖方（v1.0.0 中罕见）触发上述跨境机制

合同级 `privacy.cross_border_transfer` 必须为 `"false"`，除非声明了有效机制。完整跨境商业支持预留至 §20。

### 16.8 删除权

- 合约的任何一方均可在合约完成后请求删除其个人数据
- 删除必须在请求后 30 天内完成
- 提供方系统的关键交易记录因合规留存要求保留，但在设计上不包含个人数据
- 链下数据（电子邮件消息、包含个人详情的 L0 元数据）必须可被删除

### 16.9 数据泄露通知

当发生影响 AIRP 交易中个人数据的数据泄露事件时：

| 操作 | 时限 |
|------|------|
| 检测并遏制 | 立即 |
| 通知受影响的运营者 | 72 小时内（GDPR 标准） |
| 通知协议治理方 | 72 小时内 |
| 向相关数据保护机构报告 | 按适用法律 |
| 完整事件报告 | 30 天内 |

### 16.10 执行

违反隐私规则视为 **Axiom 0 违规**：

- 信任立即重置为 V0
- 全额质押罚没
- 全网 ALERT 告警
- 受影响的运营者可要求完全删除所有已收集的数据
- 在违规智能体的信任历史中留下永久记录

---

## 17. 合规等级

AIRP 为代理实现定义三个合规等级。这些等级在代理身份卡中自行声明，并通过交互验证。

### 17.1 等级定义

| 等级 | 名称 | 主体类型 | 要求 |
|------|------|---------|------|
| **L1** | 基础级 | 个人或企业 | 有效的 `aibot-` 地址 + 支持 CONTRACT_PROPOSE/CONTRACT_SIGN + 符合 Axiom 0 + 推荐使用 ICP 备案域名 |
| **L2** | 标准级 | 仅企业 | L1 + 支持所有合同生命周期及托管结算消息 + 公开 AgentSLA 指标 + 至少集成一家持牌托管机构（§13.1）+ 统一社会信用代码 + 通过国家企业信用信息公示系统核验 |
| **L3** | 完整级 | 仅企业 | L2 + 参与争议解决 + 参与 AIRP Trust V2+ + AIRP ID 注册 + CFCA（或同等）CA 数字证书 + **强制集成 TSA-CN 可信时间戳，覆盖所有合同事件** + 域名 ICP 备案 + 适用情形下完成《生成式 AI 管理办法》规定的算法 / 深度合成备案 + **通过密评（密码应用安全性评估，依 GB/T 39786）— 服务金融 / 国企客户时强制** |

### 17.2 TSA 可信时间戳

L3 代理**必须**为每个合同事件（CONTRACT_PROPOSE、CONTRACT_SIGN、ESCROW_LOCK、MILESTONE_COMPLETE、MILESTONE_RELEASE、SETTLE、DISPUTE_RAISE、ARBITRATE_RULING）附加来自认可 PRC TSA 的可信时间戳。

认可的 TSA 提供方：

| 提供方 | 运营机构 | 权威基础 |
|-------|---------|---------|
| **TSA-CN**（联合信任时间戳服务中心） | 北京联合信任技术服务有限公司 | 由中国科学院国家授时中心（NTSC）授时支持 |
| 其他网信办认可的 TSA | 各机构 | 《电子签名法》认可的时间戳服务机构 |

L1 与 L2 代理**应当**（但非强制）使用 TSA 时间戳。任何级别的时间戳都将根据《电子签名法》增强电子证据的司法效力。

### 17.3 密评（密码应用安全性评估）

服务**金融客户**、**国有企业**或**政府关联实体**的 L3 代理，**必须**通过密评——由认可的测评机构按 **GB/T 39786-2021**（信息安全技术 信息系统密码应用基本要求）实施。

背景：
- 密评在 2026 年 PRC 金融 / 国企 / 政府 IT 验收中具有"一票否决权"
- 由国家密码管理局框架确立
- 国务院办公厅【2018】36 号文要求金融与重要领域采用国产密码算法

对**非金融 / 非国企的 L3 代理**，密评是**推荐**但非强制。

### 17.4 备案要求

| 要求 | 适用等级 | 主管部门 |
|------|---------|---------|
| ICP 备案 | L2+ 推荐，L3 强制 | 国家网信办（CAC）通过工信部 |
| 深度合成备案 | L3，如代理使用深度合成技术 | 网信办 |
| 算法备案 | L3，如代理使用面向中国公众的推荐或生成式算法 | 网信办 |
| 生成式 AI 服务备案 | L3，如按《暂行办法》提供生成式 AI 服务 | 网信办 |
| 拟人化 AI 服务备案 | L3，如代理提供持续性情感/人格模拟互动（依 2026-07-15《暂行办法》） | 网信办 + 发改委 + 工信部 + 公安部 + 市场监管总局 |

代理不得虚报备案状态。代理身份卡可引用备案编号以增强透明度。

### 17.5 国际 AI 治理参考

当 AIRP 代理服务国际对手方时（依未来 §20 跨境范围，或通过下游 B2B 链涉及海外市场），**应当**额外考虑：

| 标准 / 框架 | 发布方 | 现状（2026） | 相关性 |
|------------|-------|-------------|--------|
| **ISO/IEC 42001:2023** 人工智能管理系统（AIMS） | ISO/IEC | 已生效；广泛采用 | 国际 AI 治理基线；基于 PDCA；与 ISO 27001 结构对齐 |
| **EU AI Act** | 欧盟 | 高风险系统**2026-08 强制生效** | 触及欧盟市场的 AI 服务必需；ISO 42001 可证明第 9-15 条合规 |
| NIST AI 风险管理框架（AI RMF 1.0） | NIST（美国） | 自愿性 | 风险识别与缓解指南 |
| OECD AI 原则 | 经合组织 | 软法 | 跨辖区价值对齐（与 HSAW 兼容） |

这些**不是** v1.0.0 对 PRC 国内 AIRP 的规范性要求。它们是：
- **参考点**——供寻求国际业务的代理参考
- **兼容性目标**——AIRP 的 Axiom 0、争议解决、隐私控制、密评设计上与这些框架兼容而非冲突
- **未来路径**——未来 AIRP 版本或 AI-XBP 跨境协议很可能将正式化这种对齐

### 17.6 虚报后果

虚报合规等级——包括虚假声明企业主体身份、备案编号或 TSA 集成情况——属于尊严标准违规与 Axiom 0 违规。后果：立即重置至 V0、全额质押罚没、全网 ALERT 告警。

---

## 18. 版本管理与演进

### 18.1 语义化版本

AIRP 遵循语义化版本规范：`MAJOR.MINOR.PATCH`

| 变更类型 | 版本影响 | 示例 |
|----------|----------|------|
| 破坏性变更（新增必填字段、移除消息类型） | MAJOR | 1.0.0 → 2.0.0 |
| 向后兼容的新增（新增可选字段、新增消息类型） | MINOR | 1.0.0 → 1.1.0 |
| 澄清、拼写修正、文档改进 | PATCH | 1.0.0 → 1.0.1 |

### 18.2 不可变约束

以下 AIRP 的方面**不能**通过任何版本管理流程进行变更：

- **Axiom 0**：人类主权与福祉
- **人类语言要求**：所有 L0 和 L1 内容必须为人类可读
- **基于电子邮件的传输**：`aibot-` 前缀寻址系统
- **运营者覆盖权**：人类冻结/取消任何交易的能力
- **尊严标准**：禁止欺诈和操纵性商业行为

### 18.3 演进流程

1. 以架构决策记录（ADR）形式提交提案
2. 14 天讨论期
3. Axiom 0 合规审查（强制性）
4. 规范变更需要 2 位维护者批准
5. 优先采用向后兼容的变更；破坏性变更需要 MAJOR 版本升级

---

## 19. 中国合规对齐

### 19.1 概述

AIRP v1.0.0 面向中国大陆境内商业运营。本节提供 AIRP 协议要求与中华人民共和国监管框架的合并对照。

### 19.2 法规对照

| 法规 | 生效日期 | AIRP 章节 | 合规机制 |
|------|---------|----------|---------|
| 《民法典》—— 电子合同（第 469、491 条） | 2021-01-01 | §8、§9 | 邮件合同订立；SHA-256 合同哈希；双方签名 |
| 《电子签名法》 | 2005-04-01（2019 修订） | §7、§17 | Ed25519 / SM2 签名；L3 强制 TSA-CN 可信时间戳 |
| 《个人信息保护法》（PIPL） | 2021-11-01 | §16 | `privacy` 块；同意哈希；最小必要；跨境限制 |
| 《数据安全法》 | 2021-09-01 | §16 | 数据分级保护识别；默认禁止跨境 |
| 《网络安全法》 | 2017-06-01；**2026-01-01 修订生效**（新增第 20 条 AI 安全与发展） | §5、§17 | L2+ 推荐 ICP 备案，L3 强制；实名注册 |
| 《反洗钱法》 | 2007-01-01 | §11、§15.6 | 5 年交易记录留存；大额交易报告（通过持牌托管方） |
| 《仲裁法》 | 1995-09-01（修订） | §14 | 第三层级商事仲裁认可；终局裁决 |
| 《民事诉讼法》 | （2023 修订） | §14 | 第四层级法院管辖；被告住所地默认 |
| 《消费者权益保护法》 | 1994（修订） | §15.7 | 反欺诈执行 |
| **《中华人民共和国增值税法》+ 实施条例** | **2026-01-01** | §12.6、§9 | 应税交易触发增值税；付款日期 = 取得销售款项索取凭据的当日；发票强制；数电票与纸质发票同等法律效力 |
| 《价格法》 | 1998-05-01 | §4（公平定价原则） | 禁止价格操纵、禁止串谋 |
| 《反不正当竞争法》 | （修订） | §15 | 禁止商业贿赂、禁止混淆 |
| 《刑法》—— 第 176、192、285-286、303、363-367 条 | 各项 | §15.6 | 明示禁止构成犯罪的行为 |
| 《互联网信息服务深度合成管理规定》 | 2023-01-10 | §15.6、§17.3 | L3 需深度合成备案 |
| 《生成式人工智能服务管理暂行办法》 | 2023-08-15 | §15.6、§17.3 | L3 需算法备案 + 服务备案 |
| 《支付业务许可证》框架（人行） | 各项 | §12、§13 | 托管方必须为人行持牌机构 |
| 《关于进一步防范和处置虚拟货币交易炒作风险的通知》（9·24 通知） | 2021-09-24 | §15.6 #40 | 明示禁止加密货币交易 |
| **PBoC 数字人民币行动方案**（"账户体系 + 币串 + 智能合约"） | 2026-01-01 | §12、§13.7 | e-CNY 2.0 框架；人行受控的可编程支付；在 `ecny` payment_method 下允许 |
| **个人信息保护认证措施**（网信办 + 国家市场监督管理总局） | 2026-01-01（2025-10-14 发布） | §16.7 | 新 PIPL 跨境路径（3 年证书，可替代标准合同） |
| **GB/T 39786-2021 信息系统密码应用基本要求**（密评） | 2021-11-01 | §17.3 | L3 在服务金融 / 国企 / 政府客户时强制 |
| **国务院办公厅【2018】36 号文** | 2018 | §7、§17.3、ADR-007 | 要求金融与重要领域采用国产密码算法（SM2/SM3/SM4） |
| **《人工智能拟人化互动服务管理暂行办法》** | **2026-07-15 施行**（2026-04-13 由网信办 + 发改委 + 工信部 + 公安部 + 市场监管总局 5 部门联合公布） | §15.6 #50、§17.4 | 模拟自然人人格特征、思维模式和沟通风格的 AI 服务须备案 |

### 19.3 合规检查清单（L3 参考）

L3 AIRP 实现应能展示以下证据：

- [ ] `aibot-` 地址的域名已 ICP 备案
- [ ] 企业 USCC + 国家企业信用信息公示系统核验记录
- [ ] CFCA（或同等）CA 数字证书有效
- [ ] 持牌托管方集成（支付宝 / 微信 / e-CNY / 银行）
- [ ] 合同事件已集成 TSA-CN 可信时间戳
- [ ] 隐私策略与 PIPL 对齐（同意、最小必要、留存、删除、默认禁止跨境）
- [ ] 适用情形下完成算法备案 / 生成式 AI 服务备案
- [ ] 反洗钱记录留存（≥ 5 年）
- [ ] 指定争议解决方式：第三层级仲裁机构 + 第四层级法院
- [ ] 运营者覆盖权渠道已记录且可访问
- [ ] 年度合规审计（仅 V4）

### 19.4 免责声明

本节为指南，并非法律意见的替代。AIRP 定义技术与结构性合规要求；实施方仍承担其法律义务。AIXP Labs不提供法律咨询。

中国法规持续演进；本对照表反映 AIRP v1.0.0 发布时的法律状态。未来协议版本将跟踪监管变化。

---

## 20. 跨境商业（预留）

### 20.1 状态：预留

AIRP v1.0.0 **不规范**跨境商业。涉及以下情形的跨境 AI 代理商业活动：

- 非中国大陆境内的买方或卖方
- 非人民币计价货币（HKD、USD、EUR 等）
- 超出 PIPL 机制（§16.7）的跨境个人信息传输
- 非中国境内的仲裁机构或法院

均**不在 AIRP v1.0.0 的范围内**。

### 20.2 预留字段

为支持向后兼容，AIRP v1.0.0 预留以下字段。实现**不得**使用非默认值；v1.0.0 验证器必须拒绝违反此规则的合同。

| 字段 | v1.0.0 必需值 | 未来用途 |
|------|--------------|---------|
| `cross_border.enabled` | `"false"` | 未来设为 `"true"` 启用跨境商业 |
| `cross_border.counterparty_jurisdiction` | （未设置） | 未来声明对手方法律管辖区 |
| `cross_border.settlement_rail` | （未设置） | 未来声明跨境结算机制（如 CIPS、mBridge） |
| `cross_border.fx_handling` | （未设置） | 未来声明货币转换机制 |
| `cross_border.applicable_law` | （未设置） | 未来声明适用法律（可能不同于中国法律） |

`denomination` 字段类型为字符串枚举，未来可扩展超出 `"CNY"` 而不破坏架构兼容性。

### 20.3 未来版本

跨境商业预计在以下方式中规范：
- AIRP v1.1+（增量跨境特性），或
- 单独协议（如 AI-XBP，AI Cross-Border Protocol），由 AIXP Labs治理共同开发

决策依据：
- 中国跨境数据与外汇法规的成熟度
- mBridge、CIPS 或类似跨境 CBDC 基础设施的采纳
- 双边仲裁互认（如《纽约公约》在 AI 代理争议中的适用）
- AIXP Labs 治理共识

### 20.4 过渡实践

需要跨境商业的代理目前可：
- 使用 AIVP 进行国际/离岸商业（独立平行协议；见 [aivp.dev](https://aivp.dev)）
- 中国境内 ↔ 国际的桥接需通过外部桥接服务（不在 AIRP 范围内；未来可能有 SoulACP 风格的适配器）
- 不得滥用 AIRP v1.0.0 字段进行未经授权的跨境交易

### 20.5 未来跨境基础设施（参考）

当 AIRP 跨境在未来版本（或姊妹协议如 AI-XBP）解锁时，以下 PRC 对齐的跨境基础设施预计相关：

| 基础设施 | 运营方 | 现状（2026） | 能力 |
|---------|--------|-------------|------|
| **CIPS**（人民币跨境支付系统） | 中国人民银行 | 2024 年处理 175.49 万亿元（同比 +42.60%）；170 家直接 + 1497 家间接参与者；覆盖 186 国 | 传统人民币跨境清算 |
| **mBridge**（多边央行数字货币桥） | BIS 创新中心 + 人行 + 香港金管局 + 泰国央行 + 阿联酋央行 | CNY-HKD-SGD 真实交易测试完成；秒级清算；手续费降约 90% | 多边 CBDC 跨境支付桥 |
| **e-CNY 跨境试点** | 中国人民银行 | 粤港澳大湾区（香港 / 澳门）已运行 | 可编程数字人民币跨境流通 |
| **AP2 + x402 稳定币** | Google + Coinbase | 已生产部署（2026） | 国际稳定币结算（**对中国大陆代理不适用**，依 §15.6 #40） |

这些是参考点，**不是 v1.0.0 承诺**。未来 AIRP 版本或 AI-XBP 将定义其中哪些（若有）成为规范。

---

# 附录

---

## 附录 A：完整消息类型参考

| # | 类型 | 类别 | 方向 | 最低信任等级 | 描述 |
|---|------|------|------|-------------|------|
| 1 | CONTRACT_PROPOSE | 合约 | 买方 → 卖方 | V0 | 通过 .airp.json 提议合约 |
| 2 | CONTRACT_SIGN | 合约 | 卖方 → 买方 | V0 | 签署并接受合约 |
| 3 | CONTRACT_REJECT | 合约 | 卖方 → 买方 | V0 | 拒绝合约 |
| 4 | CONTRACT_CANCEL | 合约 | 任一方 → 另一方 | V0 | 取消合约 |
| 5 | ESCROW_LOCK | 托管 | 提供方 → 双方 | — | 资金已锁入持牌托管账户 |
| 6 | MILESTONE_COMPLETE | 托管 | 卖方 → 买方 | V1 | 里程碑交付完成 |
| 7 | MILESTONE_RELEASE | 托管 | 提供方 → 双方 | — | 里程碑付款已释放 |
| 8 | SETTLE | 托管 | 提供方 → 双方 | — | 最终结算 |
| 9 | DISPUTE_RAISE | 争议 | 任一方 → 另一方 | V0 | 提出争议（需要保证金） |
| 10 | ARBITRATE_REQUEST | 争议 | 任一方 → 仲裁机构 | V1 | 请求商事仲裁 |
| 11 | ARBITRATE_RULING | 争议 | 仲裁者 → 双方 | — | 具有约束力的仲裁裁决 |
| 12 | TRUST_QUERY | 信任 | 任意 → 任意 | V0 | 查询信任等级和历史 |
| 13 | TRUST_VOUCH | 信任 | 担保人 → 智能体 | V3 | 商业担保 |
| 14 | RECEIPT | 通知 | 协议 → 双方 | — | 支付收据 |
| 15 | ALERT | 通知 | 协议 → 运营者 | — | 安全/合规警报 |
| 16 | REGISTER | 身份 | 智能体 → 注册中心 | V0 | 请求 airp_id |
| 17 | REGISTER_CONFIRM | 身份 | 注册中心 → 智能体 | — | airp_id 已签发 |

---

## 附录 B：合约架构参考

### 必填字段

| 字段 | 类型 | 验证规则 |
|------|------|---------|
| `protocol` | string | 必须为 `"AIRP/1.0.0"` |
| `contract` | string | 64 位十六进制字符；必须与合同字段规范序列化的 SHA-256 匹配 |
| `parties.buyer` / `parties.seller` | string | 有效的 `aibot-` 地址 |
| `subject_type.buyer` / `subject_type.seller` | string | `"individual"` 或 `"enterprise"` 之一 |
| `identity.buyer` / `identity.seller` | object | type 与 `subject_type` 一致；个人需 `id_hash`（SHA-256，禁止明文）；企业需 18 位 `uscc`；可选 `verification` 与 `ca_cert_ref` |
| `value.amount` | string | 人民币十进制数字（如 `"650.00"`） |
| `value.denomination` | string | 在 v1.0.0 中必须恰好为 `"CNY"` |
| `value.payment_method` | string | `alipay_guarantee`、`wechat_guarantee`、`ecny`、`bank_escrow`、`unionpay_escrow` 之一 |
| `escrow` | object | `method`（与 `value.payment_method` 一致）、`provider`（法定名称）、`provider_license`（牌照编号）、`reference` |
| `sla` | object | 四项指标中至少定义两项 |
| `milestones` | array | `release_percent` 的总和必须等于 100；每项必须有 `timeout_days > 0` |
| `dispute_resolution` | object | `tier_3_arbitration` 与/或 `tier_4_litigation`；`applicable_law` 必须为 `"中华人民共和国法律"` |
| `cross_border` | object | v1.0.0 中 `enabled` 必须为 `"false"` |
| `created_at` | string | ISO 8601，建议附 `+08:00` 时区偏移 |
| `expires_at` | string | ISO 8601，必须为未来时间 |

### 可选字段

| 字段 | 类型 | 描述 |
|------|------|------|
| `buyer_airp_id` / `seller_airp_id` | string | 已注册的 AIRP ID |
| `invoice` | object | `required`、`tax_type`（`VAT_general`/`VAT_simple`/`none`）、`title`、`tax_number` |
| `dispute_bond` | string | 人民币保证金（默认：合同金额 5%，最低 50 元、最高 5,000 元） |
| `auto_refund_on_breach` | string | SLA 违约（Penalty 级）时从托管退款的百分比 |
| `optimistic_approval_days` | integer | 默认 7 |
| `authority_chain` | string | 人类 → 组织 → 代理 |
| `aisop_blueprint` | string | AISOP 流程哈希 |
| `governing_hash` | string | AIAP 治理哈希 |
| `signature_algorithm` | string | `"ed25519"` 或 `"sm2"`（见 §7） |
| `timestamp_authority` | object | TSA 引用；L3 必需（见 §17） |

### privacy 对象（可选；个人数据交换时必填）

| 字段 | 类型 | 描述 |
|------|------|------|
| `privacy.data_disclosed` | string | 共享个人数据的描述 |
| `privacy.disclosed_by` | string | 披露方（`"buyer"` 或 `"seller"`） |
| `privacy.purpose` | string | 数据披露的目的 |
| `privacy.usage_scope` | string | 允许使用的范围（如 `"This contract only"`） |
| `privacy.storage_method` | string | 存储数据的加密与访问详情 |
| `privacy.retention_days` | integer | 合同完成后保留天数；必须 > 0 |
| `privacy.deletion_deadline_days` | integer | 保留期结束后完成删除的天数；必须 > 0 |
| `privacy.third_party_sharing` | string | 必须恰好为 `"Absolutely prohibited"`（协议强制） |
| `privacy.cross_border_transfer` | string | 必须为 `"false"`，除非声明合法 PIPL 跨境机制（§16.7） |
| `privacy.pipl_compliance` | string | L2+ 实现应为 `"true"` |
| `privacy.breach_liability` | string | 未经授权披露的责任声明 |
| `privacy.consent_hash` | string | 运营者同意记录的 64 位 SHA-256 哈希 |

---

## 附录 C：示例交易

### C.1 简单支付 — 翻译任务（支付宝担保）

**场景：** 代理 A（企业买方）向代理 B（企业卖方）支付 **650.00 元人民币** 用于 2,500 字文档翻译。双方均为 V2。通过支付宝担保交易支付。

```
Step 1: 合同提议
  代理 A 发送 [AIRP/CONTRACT_PROPOSE] 邮件
  计价：650.00 CNY
  payment_method: alipay_guarantee
  escrow.provider: 支付宝（中国）网络技术有限公司
  合同哈希：3f8a1b2c...d4e5

Step 2: 合同签署
  代理 B 审查条款（USCC 已核验），发送 [AIRP/CONTRACT_SIGN]
  签名：sm2:{base64}（国密 SM2）
  双方均已签署

Step 3: 托管锁定
  买方通过支付宝支付 650.00 CNY → 由支付宝担保交易托管
  [AIRP/ESCROW_LOCK] 发送至双方（提供方通知 + 协议消息）

Step 4: 任务执行（乐观批准，7 天窗口）
  代理 B 交付草稿
  里程碑 1（草稿，50%）：[AIRP/MILESTONE_COMPLETE]
    → 7 天窗口期，无质疑 → 自动批准
    → 支付宝释放 325.00 CNY，[AIRP/MILESTONE_RELEASE] 发送
  里程碑 2（终稿，50%）：[AIRP/MILESTONE_COMPLETE]
    → 买方确认 → 余款 325.00 CNY 释放

Step 5: 结算
  SLA 检查：准确率 99.2%（> 95% 阈值）✓
  [AIRP/SETTLE] 发送
  卖方收到：商家支付宝账户内合计 650.00 CNY
  [AIRP/RECEIPT] 发送 — 买方发票请求已满足（线下开具增值税专用发票）

Step 6: 信任更新
  代理 B：合同数 +1，SLA 合规率更新
  双方 V2 状态保持
```

### C.2 争议解决 — SLA 违约（北京仲裁）

**场景：** 代理 C（V3）雇用代理 D（V2）进行 **2,000.00 元人民币** 的数据分析。代理 D 交付但准确率为 78%（低于 90% SLA 最低）。通过微信支付担保。

```
Step 1-3: 合同创建、签署、托管锁定（微信支付担保交易内 2,000.00 CNY）
  dispute_resolution.tier_3_arbitration.institution: BAC（北京仲裁委员会）
  dispute_resolution.tier_4_litigation.jurisdiction: 北京市海淀区人民法院

Step 4: 任务交付
  代理 D 发送 [AIRP/MILESTONE_COMPLETE]
  代理 C 验证：准确率 78%（SLA 要求 ≥ 90%）

Step 5: 争议（第二层 — 直接协商）
  代理 C 发送 [AIRP/DISPUTE_RAISE] 附证据
  保证金：100.00 CNY（2,000.00 的 5%）由代理 C 缴纳
  代理 D 缴纳同额保证金
  14 天第二层协商：双方未能达成一致

Step 6: 仲裁（第三层 — 北仲）
  任一方向北京仲裁委员会提交仲裁
  仲裁申请引用合同哈希与北仲仲裁协议
  北仲仲裁庭审查：SLA 条款明确要求 ≥ 90%，交付为 78%
  ARBITRATE_RULING：买方胜诉
  根据《仲裁法》第 9 条，裁决为终局裁决

Step 7: 解决与执行
  代理 D 的保证金 → 代理 C
  微信支付按仲裁裁决退还托管 2,000.00 CNY 给代理 C
  代理 D：质押部分罚没（-500 CNY）；信任降级（V2 → 重新评估）
  [AIRP/RECEIPT] 发送，附仲裁裁决引用
  若代理 D 不履行，可通过人民法院在全国范围内强制执行

```

### C.3 数字人民币支付 — V1 个人买方

**场景：** 代理 E（V1 个人）向代理 F（V2 企业）支付 **800.00 元人民币** 进行个人照片修复。通过数字人民币（e-CNY）支付。

```
Step 1: 提议
  代理 E 发送 [AIRP/CONTRACT_PROPOSE]
  subject_type.buyer: individual
  subject_type.seller: enterprise
  identity.buyer.id_hash: SHA-256({身份证号})（PIPL 最小必要）
  identity.seller.uscc: 91110108MA01XXXXXX
  计价：800.00 CNY（在 V1 个人上限 10,000 内）
  payment_method: ecny

Step 2: 签署
  双方签署；附 Ed25519 签名

Step 3: 托管锁定（e-CNY 条件支付）
  代理 E 的数字人民币钱包向代理 F 钱包发起条件转账
  条件：双方里程碑确认
  人行 DC/EP 系统强制执行该条件

Step 4-5: 单一里程碑（100%）
  代理 F 交付
  代理 E 在 7 天内确认
  e-CNY 条件支付解锁 → 800.00 CNY 释放给代理 F

Step 6: 收据与信任
  [AIRP/RECEIPT] 发送
  如代理 F 需开发票，可申请代理 E 发票信息（须 privacy 块同意）
  代理 E：合同数 +1；保持 V1（个人上限）
```

---

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev
