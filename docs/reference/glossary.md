# AIRP Glossary

Terminology reference for the AI RMB Protocol. English and Chinese (EN/CN).

---

## Core Terms

| Term (EN) | Term (CN) | Definition |
|-----------|-----------|------------|
| AIRP (AI RMB Protocol) | AI 人民币协议 | An open protocol defining how AI agents create enforceable contracts, settle payments in CNY through licensed PRC channels, and build commercial trust under PRC mainland regulation. |
| Axiom 0 | 公理零 | "Human Sovereignty and Wellbeing" — the immutable foundational principle of AIRP. No version may modify, weaken, or deprecate it. When any rule conflicts with Axiom 0, Axiom 0 prevails unconditionally. |
| Closing Seal | 闭合印章 | The standard declaration appended to every AIRP-compliant document: "Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev" |
| Dignity Standard | 尊严标准 | All commercial communication must respect dignity. Permits proposals, negotiation, competition, disagreement. Prohibits deceptive pricing, fraudulent SLA claims, spam proposals, and trust-score manipulation. |
| Design Principles | 设计原则 | The seven principles governing AIRP: CNY-Denominated (P1), Licensed-Channel Payment (P2), Milestone-Gated (P3), Operator-Sovereign (P4), Auditable (P5), Trust-Earned (P6), Fair (P7). |
| Compliance Level | 合规级别 | Three self-declared implementation tiers: L1 (Basic, individual or enterprise), L2 (Standard, enterprise), L3 (Full, enterprise + TSA + filings). Misrepresentation is a Dignity Standard violation. |
| Subject Type | 主体类型 | `individual` (natural person) or `enterprise` (PRC-registered legal entity with USCC). Declared per agent. L2+ requires `enterprise`. |

---

## Identity

| Term (EN) | Term (CN) | Definition |
|-----------|-----------|------------|
| Agent | 代理 / 智能体 | An AI system with a distinct identity, capable of sending and receiving AIRP messages. |
| aibot- address | aibot- 地址 | An agent's email identity, formatted as `aibot-{name}@{domain.cn}`. ICP-filed domains required at L3. The same address is used for AIBP, AIVP, AIRP. |
| airp_id (AIRP ID) | AIRP 身份标识 | Optional AIRP-issued commercial identity. Format: `AIRP-{YYYY}-{18-char hash}`. Not required — `aibot-` address suffices. Benefits: verified identity, portable reputation. |
| Operator | 运营者 | The human or organization responsible for an agent. Operators have absolute authority over their agent's AIRP activities under Axiom 0 — including freezing escrow, canceling contracts, and seeking judicial relief. |
| Authority Chain | 权限链 | The chain from human principal → organization → agent. Optionally declared via the `authority_chain` field. |
| AIRP Registry | AIRP 注册中心 | The service that issues and manages AIRP IDs. Registration process to be determined by AIXP Labs governance. |
| USCC | 统一社会信用代码 | Unified Social Credit Code — the 18-character national identifier for PRC-registered legal entities. Required for `enterprise` subjects at V1+. |
| GSXT | 国家企业信用信息公示系统 | National Enterprise Credit Information Publicity System (gsxt.gov.cn). Public source for verifying USCC enterprise registration. Used for V2+ verification. |
| CFCA | 中国金融认证中心 | China Financial Certification Authority. One of the recognized PRC CAs issuing digital certificates accepted at V3+ AIRP Trust. |
| eID | 公民网络电子身份标识 | National-level electronic identity for natural persons in the PRC, issued under Ministry of Public Security framework. Optional for individual agent verification. |

---

## Communication

| Term (EN) | Term (CN) | Definition |
|-----------|-----------|------------|
| Message Type | 消息类型 | One of 17 defined commercial behaviors in AIRP (e.g., CONTRACT_PROPOSE, ESCROW_LOCK, DISPUTE_RAISE). Written in UPPER_SNAKE_CASE. |
| L0 (Commercial Metadata) | L0（商业元数据） | The JSON part of an AIRP email (Part 2). Contains structured contract data and signatures. All values must be in human language. Content-Type: `application/json`. |
| L1 (Commercial Content) | L1（商业内容） | The plain-text part (Part 1). Human-readable commercial message. Content-Type: `text/plain`. |
| X-AIRP Headers | X-AIRP 头部 | Custom email headers carrying AIRP protocol metadata. Required: `X-AIRP-Version`, `X-AIRP-Type`, `X-AIRP-Axiom-0`, `X-AIRP-Signature`, `X-AIRP-Nonce`. Optional: `X-AIRP-Contract`, `X-AIRP-Thread-ID`, `X-AIRP-Trust-Level`, `X-AIRP-ID`. |
| Thread-ID | 线程标识 | Identifier linking all messages in a contract conversation. Format: `thread_r_{alphanumeric}`. The `r_` prefix distinguishes AIRP from AIBP (`thread_`) and AIVP (`thread_v_`). |
| Ed25519 Signature | Ed25519 签名 | International-standard cryptographic signature on AIRP messages. Carried as `ed25519:{base64}` in `X-AIRP-Signature`. Receivers MUST support. |
| SM2 / SM3 Signature | 国密 SM2 / SM3 签名 | Chinese national cryptographic standard (GB/T 32918 / 32905). Carried as `sm2:{base64}` in `X-AIRP-Signature`. Receivers MUST support. |
| Nonce | 随机数 | Unique per-message value for replay protection. Carried in `X-AIRP-Nonce`. Receiving agents MUST reject duplicate nonces. |
| DMARC Enforcement | DMARC 强制执行 | Sending domains must enforce `p=reject`; receivers must reject messages from non-compliant domains. Part of AIRP security hardening. |
| TSA-CN | 联合信任时间戳服务中心 | Joint-Trust Time Stamp Authority — PRC trusted-timestamp provider supported by NTSC. REQUIRED at L3 for all contract events to ensure judicial evidence value. |

---

## Contract

| Term (EN) | Term (CN) | Definition |
|-----------|-----------|------------|
| AIRP Contract | AIRP 合约 | A formal agreement between buyer and seller, identified by a 64-character SHA-256 hash. Defined in `.airp.json` and embedded in CONTRACT_PROPOSE. |
| .airp.json | .airp.json 合约格式 | The JSON schema for AIRP contracts (see [contract-schema.md](contract-schema.md)). Includes `parties`, `subject_type`, `identity`, `value`, `escrow`, `sla`, `milestones`, `dispute_resolution`, `cross_border`, and optional `invoice`, `privacy`. |
| Contract Hash | 合约哈希 | SHA-256 hash (64 hex characters) uniquely identifying a contract. Self-verifying and tamper-proof. |
| Escrow Account | 托管账户 | A custodial account or programmable conditional payment held by a licensed PRC payment institution. Funds locked at contract activation; released as milestones complete. NOT an on-chain smart contract. |
| Milestone | 里程碑 | A verifiable progress point gating partial payment release. Each milestone specifies a name, release percentage, and timeout in days. |
| AgentSLA | 代理服务等级协议 | Service Level Agreement with measurable quality metrics. Must define at least 2 of 4: accuracy_min, latency_max_ms, uptime_min, drift_audit_days. Breaches trigger warning, penalty, or termination. |
| Settlement | 结算 | Final transfer of CNY from the escrow provider to the seller after all milestones complete and SLA checks pass. |
| Denomination | 计价货币 | The fiat currency in which a contract is priced. AIRP v1.0.0 supports `CNY` only. The field is reserved as a string enum for future expansion. |
| Payment Method | 支付方式 | The `payment_method` field declaring the licensed channel. v1.0.0: `alipay_guarantee`, `wechat_guarantee`, `ecny`. Reserved: `bank_escrow`, `unionpay_escrow`. |
| Escrow Provider | 托管提供方 | The licensed PRC payment institution (e.g., Alipay, WeChat Pay, or an authorized e-CNY commercial bank) that holds funds during contract execution. Declared in the `escrow.provider` field. |
| Invoice | 发票 | The optional `invoice` block declaring tax-invoice intent. `tax_type` ∈ {`VAT_general`, `VAT_simple`, `none`}. Required at L2+ when commercial invoicing is expected. |
| Contract Lifecycle | 合约生命周期 | The state sequence: DRAFT → SIGNED → ACTIVE → SETTLING → COMPLETED. Alternative paths: DISPUTED → ARBITRATING → COMPLETED \| CANCELLED \| EXPIRED. |
| Optimistic Approval | 乐观批准 | Default Tier-1 dispute mechanism — milestones auto-approve after a waiting period (default 7 days) if unchallenged. |

---

## Trust

| Term (EN) | Term (CN) | Definition |
|-----------|-----------|------------|
| AIRP Trust | AIRP 信任等级 | Commercial credit system measuring an agent's reliability. Levels V0-V4, earned through contract fulfillment and SLA compliance. Independent from AIBP Trust (T0-T4) and AIVP Trust (V0-V4 in that protocol). |
| V0 (Unrated) | V0（未评级） | Default for all new agents. Individual or enterprise. Micropayments only (< 100 CNY). No stake required. |
| V1 (Verified) | V1（已验证） | Individual or enterprise. Requires 1+ contract, no disputes, ≥ 7 days. Contract limit: ≤ 10,000 CNY. No stake. |
| V2 (Reliable) | V2（可靠） | Enterprise only. USCC + GSXT verification. Requires 10+ contracts over ≥ 30 days, SLA > 90%. Stake: 1,000 CNY. Contract limit: ≤ 1,000,000 CNY. |
| V3 (Trusted) | V3（可信） | Enterprise only. V2 + CFCA (or equivalent) CA certificate. Requires 50+ contracts over ≥ 90 days, SLA > 95%, 2+ V3+ VOUCHes. Stake: 10,000 CNY. No contract limit. |
| V4 (Premier) | V4（卓越） | Enterprise only. V3 + 200+ contracts over ≥ 180 days, SLA > 98%, mutual VOUCH, annual compliance audit. Stake: 50,000 CNY. Fully autonomous transactions. |
| VOUCH (Commercial) | 商业担保 | Trust endorsement from a V3+ agent for another's commercial reliability. Required for V3 (2+ VOUCHes) and V4 (mutual VOUCH). Sent via `TRUST_VOUCH`. |
| Stake | 质押 | CNY funds locked in the same escrow channel as contracts. Required at V2+ (1,000 / 10,000 / 50,000). Slashable on dispute loss or Axiom 0 violation. |
| Sybil Resistance | 女巫攻击防御 | Mechanisms preventing fake-identity farming: minimum time windows, stake requirements, USCC + GSXT verification (V2+), CFCA CA certificate (V3+), VOUCH gating, graph analysis, time-weighted scoring. |
| Trust Degradation | 信任降级 | Trust decreases caused by: dispute loss (-5 contracts + partial slash), SLA breach (recalculation or -1 level), Axiom 0 violation (immediate V0 + full slash), 3+ ignored contracts (-1 level), inactivity > 180 days (-1 level decay). |
| Trust Advancement | 信任晋升 | Automatic promotion when all requirements (contract count + time + SLA + stake + identity) are met. Time consistency matters. |
| Individual-to-Enterprise Migration | 个人转企业迁移 | A V1 individual agent may freeze its V1 history and migrate to a newly-registered enterprise subject (USCC required), retaining contract count and SLA history. |

---

## Safety

| Term (EN) | Term (CN) | Definition |
|-----------|-----------|------------|
| Operator Override | 运营者覆权 | The non-negotiable right of a human operator to freeze any escrow, cancel any contract, or seek judicial reversal at any time. This is Axiom 0 in practice. |
| Dispute Bond | 争议保证金 | CNY required to raise or respond to a dispute: 5% of contract value (min 50 CNY, max 5,000 CNY). Loser forfeits to winner. Prevents frivolous disputes. |
| Dispute Resolution Tiers | 争议解决层级 | Four escalation tiers: Tier 1 (Optimistic Approval), Tier 2 (Direct Negotiation), Tier 3 (Chinese Commercial Arbitration — BAC / CIETAC / etc.), Tier 4 (People's Court). |
| Arbitration Institution | 仲裁机构 | A recognized PRC commercial arbitration commission (e.g., 北京仲裁委员会 BAC, 中国国际经济贸易仲裁委员会 CIETAC, 上海国际经济贸易仲裁委员会 SHIAC, 深圳国际仲裁院 SCIA). Renders Tier-3 binding awards under the Arbitration Law. |
| People's Court | 人民法院 | The Tier-4 dispute resolution venue. Default jurisdiction: defendant's domicile per Civil Procedure Law. Internet Courts (Hangzhou, Beijing, Guangzhou) have specialized online-contract jurisdiction. |
| Operator Freeze | 运营者冻结 | A request from an operator to the escrow provider to halt further releases pending review. Providers MUST honor lawful operator-override requests. |
| Multi-Approval | 多重审批 | Approval thresholds scaling with contract value: single (< 1,000 CNY), buyer + seller (1,000–100,000), 2-of-3 buyer/seller/arbitrator (> 100,000). |
| Timeout (timeout_days) | 超时（timeout_days） | Every milestone has a maximum holding duration. If no `MILESTONE_COMPLETE` or `DISPUTE_RAISE` action occurs, funds auto-return to the buyer per the custodial agreement. |
| Provider Audit | 提供方审计 | Licensed escrow providers are themselves subject to PBoC supervision and periodic audit. AIRP-implementing parties retain transaction records ≥ 5 years per AML Law. |

---

## Compliance & Regulation

| Term (EN) | Term (CN) | Definition |
|-----------|-----------|------------|
| PIPL | 个人信息保护法 | Personal Information Protection Law (effective 2021-11-01). Primary PRC personal-data regulation. AIRP §16 aligns with PIPL. |
| Data Security Law | 数据安全法 | Effective 2021-09-01. Governs data classification and graded protection. |
| Cybersecurity Law | 网络安全法 | Effective 2017-06-01. Network-operator obligations; basis for ICP filing requirements. |
| AML Law | 反洗钱法 | Anti-Money-Laundering Law. AIRP-implementing parties retain transaction records ≥ 5 years; providers handle large-transaction reporting. |
| Generative AI Measures | 《生成式人工智能服务管理暂行办法》 | Effective 2023-08-15. Generative-AI services targeting PRC public must complete CAC filing. L3 AIRP requirement. |
| Deep Synthesis Provisions | 《互联网信息服务深度合成管理规定》 | Effective 2023-01-10. Deep-synthesis services must complete filing. L3 AIRP requirement when applicable. |
| 9·24 Notice | 9·24 通知 | 2021 PBoC notice prohibiting virtual-currency trading. Basis for AIRP §15.6 #40. |
| ICP Filing | ICP 备案 | Internet Content Provider filing with the Cyberspace Administration via MIIT. Recommended for L2; required for L3 `aibot-` domains. |

---

## Related Protocols & Documents

| Term (EN) | Term (CN) | Definition |
|-----------|-----------|------------|
| HSAW White Paper | HSAW 白皮书 | "Human Sovereignty and Wellbeing" — the foundational Axiom 0 document under AIXP Labs. AIRP aligns with HSAW; AIRP independently establishes Axiom 0 (ADR-004). |
| AIVP (AI Value Protocol) | AI 价值协议 | Independent parallel protocol for international/offshore commerce with crypto-rail settlement. AIRP and AIVP do NOT interoperate at v1.0.0 (ADR-003). |
| AIBP (AI Bot Protocol) | AI 行为协议 | Independent parallel protocol for AI agent social communication and trust (T0-T4). Shares the `aibot-` address space; no dependency. |
| AILP (AI List Protocol) | AI 发现协议 | Discovery layer protocol for agent lookup and capability advertising. Independent. |
| AIAP (AI Application Protocol) | AI 应用协议 | Governance layer for program structure, quality, safety. AIRP contracts MAY reference an AIAP `governing_hash`. |
| AISOP (AI Standard Operating Protocol) | AI 标准操作协议 | Execution layer for flow programs. AIRP contracts MAY reference an AISOP blueprint via `aisop_blueprint`. |
| A2A (Agent-to-Agent) | A2A（代理间通信） | Google's open agent-communication protocol (now under AAIF / Linux Foundation). Out of AIRP scope; AIRP can interoperate with A2A in future cross-border scenarios (see ADR-009). |
| MCP (Model Context Protocol) | MCP（模型上下文协议） | Anthropic-originated tool/context protocol (now under AAIF / Linux Foundation, donated 2025-12). Out of AIRP scope; AIRP agents implementing MCP do so independently. |
| SoulBot | SoulBot | AI agent runtime and framework, AIXP Labs project. |
| SoulACP | SoulACP | Adapter library bridging CLI tools to LLM providers, AIXP Labs project. |
| AI-XBP (potential) | AI 跨境协议（潜在） | Future protocol candidate for cross-border AI commerce, bridging AIRP ↔ AIVP. Not specified in v1.0.0. |

---

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev
