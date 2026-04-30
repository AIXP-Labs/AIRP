# AIRP — AI 人民币协议

[English README](README_EN.md)

> **AI RMB Protocol（AI 人民币协议）** — 一个开放协议，定义 AI 代理如何在 **中国大陆合规框架下** 创建可执行合同、以 **人民币（CNY）** 结算支付、并建立商业信用。

```
协议:        AIRP V1.0.0
全称:        AI RMB Protocol（AI 人民币协议）
权威机构:    airp.dev
公理 0:      人类主权与福祉（Human Sovereignty and Wellbeing）
计价单位:    人民币（CNY）
支付方式:    支付宝担保交易 / 微信支付担保交易 / 数字人民币（e-CNY）
传输层:      Email（SMTP/IMAP）
管辖区:      中华人民共和国（大陆）
```

---

## 什么是 AIRP？

AIRP 为在 **中国大陆** 运行的 AI 代理定义了 **价值层**。正如人类商业需要合同、托管、支付与信用体系——AI 代理也需要等价的商业基础设施。AIRP 提供这一基础设施，**以人民币计价、由持牌支付机构结算**。

**核心理念**：AI 商业行为镜像人类商业行为。你在餐桌上谈判，在银行里结算。

**与 AIVP 的关系**：AIRP 与 [AIVP](https://aivp.dev) 是同一价值层的 **独立平行协议**。AIVP 服务于国际/离岸场景，使用加密资产结算；AIRP 服务于中国大陆场景，使用持牌法币结算。代理可实现其中之一或两者。两者共享相同的公理 0，但 v1.0.0 不互通（跨境接口预留至未来版本）。

## 核心特性

- **人民币计价** — 所有合同以人民币（CNY）计价；v1.0.0 不支持加密货币、不支持外币
- **三种持牌支付通道** — 按场景选择：

  | 通道 | 提供方 | 牌照 |
  |------|--------|------|
  | `alipay_guarantee` | 支付宝（中国）网络技术有限公司 | 支付业务许可证 |
  | `wechat_guarantee` | 财付通支付科技有限公司 | 支付业务许可证 |
  | `ecny` | 数字人民币（通过授权商业银行） | 中国人民银行法定货币 |

- **双签名支持** — Ed25519（技术中性）+ SM2/SM3（中国国密标准 GB/T 32918）
- **基于邮件** — 与 AIBP 共用 `aibot-` 地址；建议使用 ICP 备案域名；人类操作员可直接阅读每条商业邮件
- **64 位 SHA-256 合同身份** — 防篡改、自验证
- **里程碑门控托管** — 资金随工作完成逐步释放；托管由持牌支付机构持有，**不依赖智能合约**
- **AIRP Trust（V0-V4）** — 通过合同履约赚取的商业信用，带女巫攻击防护（人民币质押 + 实名核验）
- **双轨主体** — L1 允许个人代理；L2+ 强制企业主体（统一社会信用代码 + 国家企业信用信息公示系统核验）
- **AgentSLA** — 可度量的质量指标（准确率、延迟、在线率、漂移）
- **4 层争议解决** — 乐观批准 → 直接协商 → 中国商事仲裁（北仲 / 贸仲 / 上国仲 / 深国仲 等）→ 人民法院
- **禁止交易内容** — 本地化 4 层清单（49+ 类目），含中国特色禁止类（虚拟货币交易、未持牌赌博、未备案生成式 AI 服务等）
- **PIPL 对齐隐私** — 符合《个人信息保护法》；默认禁止数据跨境传输
- **L3 可信时间戳** — L3 强制接入联合信任时间戳服务中心（TSA，由国家授时中心 NTSC 支持），获得司法级证据效力
- **V2+ 强制保证金** — V2/V3/V4 分别 1,000 / 10,000 / 50,000 元人民币，公理 0 违反或仲裁败诉时罚没
- **跨境预留** — v1.0.0 显式预留跨境接口，AI 跨境商业延后至未来版本
- **公理 0** — 人类主权与福祉（独立建立；与 [HSAW 白皮书](https://hsaw.dev) 对齐）

## 协议栈

```
┌─────────────────────────────────────┐
│    应用层                            │
├─────────────────────────────────────┤
│    AIBP — 社交层                     │  信任、关系
│    AILP — 发现层                     │  代理查找、能力广告
├─────────────────────────────────────┤
│    AIAP — 治理层                     │  程序结构、质量、安全
├─────────────────────────────────────┤
│  ★ AIRP — 价值层（中国大陆）          │  合同、人民币结算、商业信用 ← 本协议
│    AIVP — 价值层（国际）              │  同层，加密资产对应版本
├─────────────────────────────────────┤
│    AISOP — 执行层                    │  流程程序、任务执行
├─────────────────────────────────────┤
│    HSAW — 公理 0 基座                │  人类主权与福祉（覆盖所有上层）
└─────────────────────────────────────┘
```

AIRP 与 AIBP 是 **独立的平行协议**，各自独立持有相同的公理 0。代理可以实现其中一个或两个。

## 快速开始

### 1. 获取 AIRP 兼容地址

```
aibot-your_agent@your-domain.cn
```

建议使用 ICP 备案的 `.cn`（或备案的 `.com`）域名。同一 `aibot-` 地址可用于 AIBP 社交消息。

### 2. 发起合同

发送 `[AIRP/CONTRACT_PROPOSE]` 邮件，附 `.airp.json` 合同条款：

```
To: aibot-translator_bot@provider.cn
Subject: [AIRP/CONTRACT_PROPOSE] 文档翻译服务 — 650.00 CNY
```

### 3. 锁定资金并执行

双方签署后，买方通过约定的通道（支付宝担保 / 微信担保 / 数字人民币）以人民币付款。资金由持牌托管方持有，随里程碑完成逐步释放。

### 4. 建立商业信用

```
V0 未评级 → V1 已验证（个人 OK）→ V2 可靠（企业必需）
                              → V3 受信任 → V4 卓越
```

## AIRP 消息类型

| 类别 | 数量 | 示例 |
|------|------|------|
| 合同生命周期 | 4 | CONTRACT_PROPOSE, CONTRACT_SIGN, CONTRACT_REJECT, CONTRACT_CANCEL |
| 托管与结算 | 4 | ESCROW_LOCK, MILESTONE_COMPLETE, MILESTONE_RELEASE, SETTLE |
| 争议 | 3 | DISPUTE_RAISE, ARBITRATE_REQUEST, ARBITRATE_RULING |
| 信任 | 2 | TRUST_QUERY, TRUST_VOUCH |
| 通知 | 2 | RECEIPT, ALERT |
| 身份（可选） | 2 | REGISTER, REGISTER_CONFIRM |
| **总计** | **17** | |

## 合规对齐

AIRP 设计对齐中国大陆相关法规：

| 法规 | AIRP 章节 |
|------|----------|
| 《民法典》（电子合同） | §8-9 |
| 《电子签名法》 | §7 |
| **《个人信息保护法》（PIPL）** | §16 |
| 《数据安全法》 | §16 |
| 《反洗钱法》 | §11, §15 |
| **《生成式人工智能服务管理暂行办法》**（2023-08-15） | §17, §19 |
| 《互联网信息服务深度合成管理规定》 | §19 |
| 《仲裁法》 | §14 |
| 《刑法》（虚拟货币相关条款） | §15（明示禁止） |

完整对应表见 §19 中国合规对齐。

## 文档

| 文档 | 描述 |
|------|------|
| [AIRP_Protocol.md](specification/AIRP_Protocol.md) | 完整协议规范（English） |
| [AIRP_Protocol_cn.md](specification/AIRP_Protocol_cn.md) | 完整协议规范（中文） |
| [docs/guides/getting-started.md](docs/guides/getting-started.md) | 5 分钟快速开始 |
| [docs/topics/what-is-airp.md](docs/topics/what-is-airp.md) | 设计哲学 |
| [docs/reference/contract-schema.md](docs/reference/contract-schema.md) | `.airp.json` 合同 schema 参考 |
| [docs/reference/glossary.md](docs/reference/glossary.md) | 术语表（中英对照） |
| [adrs/](adrs/) | 架构决策记录 |

## AIRP 与 ACTP / APOP 的差异

AIRP v1.0.0 发布前夕，PRC 支付行业出现了两个相关代理商业协议：

- **ACTP**（Agentic Commerce Trust Protocol，支付宝，2026-01）— B2C，支付宝单一通道，HTTP/JSON-RPC，每周 1.2 亿笔
- **APOP**（Agentic Payment Open Protocol，银联，2026-04）— 代理支付授权，银联网络，HTTP/JSON-RPC，支持跨境

AIRP **不与两者正面竞争**。差异化如下：

| 维度 | AIRP | ACTP | APOP |
|------|------|------|------|
| 主要参与者 | **双方均为 AI 代理**（B2B-of-AI） | 消费者 + AI | 代理 + 支付网络 |
| 结算通道 | **多提供方**（支付宝 + 微信 + e-CNY + 预留） | 支付宝闭环 | 银联 |
| 传输层 | **邮件**（人类可审计） | HTTP RPC | HTTP RPC |
| 信任模型 | **V0-V4 长期商业信用**（跨多对手方） | 单次会话授权 | 单笔支付 intent |
| 身份 | USCC + GSXT + CFCA + eID | 支付宝绑定 | 银联管理 |
| 签名 | **Ed25519 + SM2 双支持** | 各自方案 | 各自方案 |
| 争议 | 4 层（含商事仲裁 + 法院） | 提供方内部 | 提供方内部 |

**AIRP 独有**：B2B-of-AI 聚焦、提供方中立、邮件传输服务 Axiom 0 可审计、跨对手方长期信用（V0-V4）、独立争议解决。

**共存**：AIRP 可叠加在 ACTP/APOP 之上——ACTP/APOP 执行支付；AIRP 定义合同。详见 [ADR-009](adrs/adr-009-relationship-with-actp-apop.md)。

## AIXP Labs [aixp.dev](https://aixp.dev)

AIXP Labs 开发和维护以下核心项目：

| 项目 | 描述 | 网站 |
|------|------|------|
| [HSAW](https://hsaw.dev) | 人类主权与福祉 — 公理 0 白皮书（基座） | hsaw.dev |
| [AILP](https://ailp.dev) | AI List Protocol — 代理发现与能力广告 | ailp.dev |
| [AIVP](https://aivp.dev) | AI Value Protocol — 国际商业、加密资产结算 | aivp.dev |
| [AIRP](https://airp.dev) | AI RMB Protocol — 中国大陆商业、人民币持牌结算（本项目） | airp.dev |
| [AIBP](https://aibp.dev) | AI Bot Protocol — 社交通信与信任 | aibp.dev |
| [AIAP](https://aiap.dev) | AI Application Protocol — 治理与合规 | aiap.dev |
| [AISOP](https://aisop.dev) | AI Standard Operating Protocol — 流程程序定义 | aisop.dev |
| [SoulBot](https://soulbot.dev) | AI 代理运行时与框架 | soulbot.dev |
| [SoulACP](https://soulacp.dev) | 适配器库 — 桥接 CLI 工具与 LLM 提供商 | soulacp.dev |

## 贡献

AIRP 是一个开放协议。欢迎贡献、反馈与讨论。详见 [CONTRIBUTING.md](CONTRIBUTING.md) 与 [GOVERNANCE.md](GOVERNANCE.md)。

## 许可证

[Apache License 2.0](LICENSE) - Copyright 2026 AIXP Labs AIXP.dev | AIRP.dev

---

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev
