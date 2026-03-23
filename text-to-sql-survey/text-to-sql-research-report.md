# Text-to-SQL 技术调研报告 2025-2026

**报告日期：** 2026 年 3 月 23 日  
**调研范围：** 市场产品、技术架构、发展趋势、企业案例

---

## 执行摘要

Text-to-SQL 技术正经历快速发展期，从学术研究走向大规模企业应用。随着大语言模型（LLM）的成熟，Text-to-SQL 系统能够实现更高的准确率和更复杂的查询能力。本报告全面分析了当前市场上的主要产品、技术实现方案、2025-2026 年发展趋势以及企业级落地案例。

**核心发现：**
- 开源模型（如 SQLCoder）在特定任务上已超越 GPT-4
- 企业级应用强调安全性、权限控制和审计能力
- 多 Agent 架构和 RAG 技术成为主流技术方案
- 2026 年趋势指向自主 Agent、模式演化鲁棒性和成本优化

---

## 一、市面上的 Text-to-SQL 产品和平台

### 1.1 领先产品概览

#### **Vanna AI** 🦙
- **定位：** 开源 Text-to-SQL 框架，支持多数据库、多轮对话
- **核心特点：**
  - 开源框架，支持任何 LLM 提供商和数据库
  - Vanna 2.0 新增企业级功能：用户感知权限、行级安全、审计日志
  - 预构建的 `<vanna-chat>` Web 组件，支持流式响应
  - 支持 FastAPI 集成，可嵌入任何网页
- **技术架构：** 采用 Agent 模式，用户身份贯穿系统提示、工具执行和 SQL 过滤
- **适用场景：** 数据分析应用、多租户 SaaS、企业环境
- **网站：** https://vanna.ai
- **GitHub：** https://github.com/vanna-ai/vanna

#### **Defog AI / SQLCoder** 🔍
- **定位：** 行业领先的 Text-to-SQL 专用模型
- **核心产品：**
  - **SQLCoder：** 开源 LLM 系列，专为 SQL 生成优化
  - **SQLCoder-34B/70B：** 在基准测试中超越 GPT-4 和 GPT-4-Turbo
  - **SQLEval：** 开源评估框架，用于测量模型准确率
- **技术优势：**
  - 在 20,000+ 人工策划问题上训练
  - 基于 10 个不同 schema，评估数据与训练数据完全隔离
  - 支持多种部署方式：transformers、llama-cpp、本地启动
- **性能数据（按类别准确率）：**
  | 模型 | date | group_by | order_by | ratio | join | where |
  |------|------|----------|----------|-------|------|-------|
  | SQLCoder-70B | 96% | 91.4% | 97.1% | 85.7% | 97.1% | 91.4% |
  | GPT-4 | 72% | 94.3% | 97.1% | 80% | 91.4% | 80% |
  | GPT-4-Turbo | 76% | 91.4% | 91.4% | 62.8% | 88.6% | 77.1% |
- **专家评价：**
  - Hugging Face CEO："开源模型现在开始在专业任务上超越 GPT-4"
  - AWS 高级架构师："Defog SQLCoder-34B 远超其他开源 text2sql 模型"
- **网站：** https://defog.ai
- **GitHub：** https://github.com/defog-ai/sqlcoder

#### **SQL AI** ⚡
- **定位：** 面向开发者的 AI 驱动 SQL 查询生成工具
- **用户规模：** 2,000+ 开发者
- **核心功能：**
  - **SQL Generator：** 自然语言描述生成生产级 SQL
  - **Query Explainer：** 4 种解释模式（基础到性能分析）
  - **Query Fixer：** 自动修复语法、安全和性能问题
  - **ERD Generator：** 从 CREATE TABLE 语句生成实体关系图
  - **Schema Builder：** 可视化设计数据库 schema
  - **Optimizer：** 索引推荐和查询优化
  - **SQL Tutor：** 交互式学习
  - **Converters：** CSV/Excel/JSON 转 SQL
  - **API Access：** REST API 集成
  - **Team Workspace：** 团队协作和查询库
- **支持数据库：** MySQL、PostgreSQL、SQLite、SQL Server、Oracle
- **网站：** https://sqlai.app

#### **MindsDB** 🧠
- **定位：** AI 分析查询引擎，支持 200+ 数据源
- **部署规模：** 500K+ 部署，38K+ GitHub Stars
- **核心特点：**
  - **无需 ETL：** 直接查询 200+ 数据源（Postgres、MongoDB、Salesforce、Shopify 等）
  - **统一 SQL 方言：** 跨不同类型数据系统 JOIN 数据
  - **Knowledge Base：** 结合向量数据和结构化数据
  - **AI Agents：** 自主推理 Agent，跨数据栈生成答案
- **工作流程：** Connect → Unify → Respond
- **应用场景：**
  - 企业知识搜索
  - 高级语义搜索
  - 客户支持自动化
  - 财务分析 Agent
  - 实时 AI 分析
  - 对话式数据助手
  - CRM 智能
- **网站：** https://mindsdb.com
- **GitHub：** https://github.com/mindsdb/mindsdb

#### **LangChain / LangSmith** 🔗
- **定位：** Agent 工程平台，支持 Text-to-SQL 应用开发
- **用户规模：** 100M+ 月下载量，6K+ 活跃客户，5/10 财富 100 强公司使用
- **核心能力：**
  - **Observability：** 追踪 Agent 行为，结构化时间线分析
  - **Evaluation：** LLM-as-judge 评估，人工反馈校准
  - **Deployment：** 支持人机协作、并发输入、后台 Agent
  - **Fleet：** 企业级 Agent 管理，支持 MCP 服务器
- **框架支持：** Python、TypeScript、Go、Java SDK
- **网站：** https://langchain.com

#### **IBM watsonx** 🏢
- **定位：** 企业级 AI 产品组合，包含 Text-to-SQL 能力
- **产品套件：**
  - **watsonx Orchestrate：** 创建和管理 AI 助手与 Agent
  - **watsonx Code Assistant：** AI 辅助开发
  - **watsonx.ai：** 端到端 AI 开发者工作室
  - **watsonx.data：** 统一数据管理
  - **watsonx.governance：** AI 治理和合规
- **企业案例：**
  - Vodafone：测试周转时间提升 99%
  - US Open：捕获分析 700 万数据点
  - IBM CIO：创建 Ansible Playbook 节省 40% 时间
  - D&B：供应商风险评估节省 10% 时间
- **网站：** https://www.ibm.com/products/watsonx

### 1.2 其他值得关注的平台

| 平台 | 特点 | 适用场景 |
|------|------|----------|
| **AskUI** | 设备控制自动化，视觉 + DOM+选择器 | 跨平台测试自动化 |
| **DataHerald** | 开源 Text-to-SQL 框架 | 企业数据查询 |
| **Snowflake Cortex** | 云数据仓库内置 AI | 云端数据分析 |
| **Databricks SQL AI** | 湖仓一体 AI 查询 | 大数据场景 |

---

## 二、Text-to-SQL 技术实现架构和方案

### 2.1 核心架构模式

#### **架构 1：Agent-Based 架构（Vanna 2.0 模式）**

```
┌─────────────┐     ┌──────────────┐     ┌─────────────┐
│   👤 User   │────▶│  🌐 <vanna>  │────▶│  🐍 Server  │
└─────────────┘     └──────────────┘     └─────────────┘
                                              │
                                              ▼
┌─────────────┐     ┌──────────────┐     ┌─────────────┐
│   📊 UI     │◀────│  🤖 Agent    │◀────│  🧰 Tools   │
│  Table/Chart│     │  (LLM)       │     │  (SQL Runner)│
└─────────────┘     └──────────────┘     └─────────────┘
```

**关键组件：**
- **User Resolver：** 从请求中提取用户身份（cookies、JWTs 等）
- **User-Aware Tools：** 基于用户组成员自动检查权限
- **Streaming Components：** 后端流式传输结构化 UI 组件
- **Row-Level Security：** 查询自动按用户权限过滤

**技术特点：**
- 身份贯穿系统提示、工具执行和 SQL 过滤
- 支持生命周期钩子（配额检查、日志、内容过滤）
- 内置 Web UI 组件，框架无关（React、Vue、纯 HTML）

#### **架构 2：专用模型架构（SQLCoder 模式）**

```
┌─────────────────┐     ┌──────────────┐     ┌─────────────┐
│ Natural Language│────▶│  SQLCoder    │────▶│   SQL Query │
│   Question      │     │   (LLM)      │     │   Execution │
└─────────────────┘     └──────────────┘     └─────────────┘
                               │
                               ▼
                        ┌──────────────┐
                        │   Metadata   │
                        │  (Schema)    │
                        └──────────────┘
```

**训练方法：**
- 基于 20,000+ 人工策划问题
- 10 个不同 schema，训练/评估数据完全隔离
- 支持 Reward Modeling 和 RLHF 微调

**部署选项：**
- **NVIDIA GPU（16GB+ VRAM）：** `pip install "sqlcoder[transformers]"`
- **Apple Silicon：** `CMAKE_ARGS="-DLLAMA_METAL=on" pip install "sqlcoder[llama-cpp]"`
- **CPU/无 GPU：** `CMAKE_ARGS="-DLLAMA_BLAS=ON" pip install "sqlcoder[llama-cpp]"`

#### **架构 3：RAG + 多 Agent 架构（2025-2026 趋势）**

```
┌─────────────┐
│   User      │
│  Question   │
└──────┬──────┘
       │
       ▼
┌─────────────────────────────────────┐
│        Query Understanding          │
│      (Intent Classification)        │
└──────────────┬──────────────────────┘
               │
       ┌───────┴───────┐
       ▼               ▼
┌─────────────┐ ┌─────────────┐
│  Schema     │ │  Context    │
│  Retriever  │ │  Retriever  │
│  (RAG)      │ │  (RAG)      │
└──────┬──────┘ └──────┬──────┘
       │               │
       └───────┬───────┘
               ▼
┌─────────────────────────────────────┐
│         Multi-Agent System          │
│  ┌──────────┐ ┌──────────┐         │
│  │ Schema   │ │ Query    │         │
│  │ Agent    │ │ Agent    │ ...     │
│  └──────────┘ └──────────┘         │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│      Execution & Validation         │
│  (Test Suite Accuracy Check)        │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────┐
│   Result    │
└─────────────┘
```

### 2.2 关键技术组件

#### **2.2.1 Schema Linking（模式链接）**
- **挑战：** 将自然语言中的实体映射到数据库表/列
- **方案：**
  - 基于语义相似度的检索
  - 使用 LLM 进行实体消歧
  - 维护 schema 元数据缓存

#### **2.2.2 Context Retrieval（上下文检索）**
- **RAG 技术：** 检索相关 schema 信息、示例查询、业务术语
- **Knowledge Base：** 结合结构化数据（表）和非结构化数据（文档）
- **向量搜索：** 使用嵌入模型进行语义检索

#### **2.2.3 SQL Generation（SQL 生成）**
- **模型选择：**
  - 专用模型：SQLCoder、CodeLlama-SQL
  - 通用模型：GPT-4、Claude、Gemini（通过 prompt 工程）
- **生成策略：**
  - Chain-of-Thought（思维链）
  - Self-Correction（自校正）
  - Execution-Guided Decoding（执行引导解码）

#### **2.2.4 Validation & Correction（验证与校正）**
- **Test Suite Accuracy：** 使用测试用例验证 SQL 正确性
- **Execution Feedback：** 执行失败时自动修正
- **Hallucination Detection：** 检测模型生成的错误信息

#### **2.2.5 Security & Governance（安全与治理）**
- **Row-Level Security：** 基于用户权限过滤查询结果
- **Audit Logging：** 记录所有查询用于合规
- **Rate Limiting：** 每用户配额限制
- **PII Detection：** 检测和保护敏感信息

### 2.3 评估指标

| 指标 | 说明 | 工具 |
|------|------|------|
| **Exact Matching** | SQL 完全匹配准确率 | Spider eval |
| **Execution Accuracy** | 执行结果正确率 | Test Suite Accuracy |
| **Component Matching** | SQL 组件（SELECT、WHERE 等）匹配 | Spider eval |
| **Test Suite Accuracy** | 通过测试用例的比例 | sql-eval |
| **Latency** | 查询响应时间 | 自定义监控 |
| **Cost** | 每次查询的 LLM token 成本 | 成本追踪 |

---

## 三、2025-2026 年 Text-to-SQL 最新发展趋势

### 3.1 技术趋势

#### **趋势 1：多 Agent 协作系统**
- **代表研究：** "A Multi-agent Text2SQL Framework using Small Language Models and Execution Feedback" (2025 年 12 月)
- **核心思想：** 使用多个小模型协作，而非单一大型模型
- **优势：**
  - 降低推理成本
  - 提高复杂查询处理能力
  - 支持执行反馈循环

#### **趋势 2：Schema Evolution Robustness（模式演化鲁棒性）**
- **代表研究：** "EvoSchema: Towards Text-to-SQL Robustness Against Schema Evolution" (2026 年 3 月)
- **挑战：** 数据库 schema 变化导致模型失效
- **方案：** 动态适应 schema 变化，无需重新训练

#### **趋势 3：多轮对话 Text-to-SQL**
- **代表研究：** "Track-SQL: Enhancing Generative Language Models with Dual-Extractive Modules for Schema and Context Tracking in Multi-turn Text-to-SQL" (2026 年 3 月)
- **能力：** 支持 follow-up 问题，维护对话上下文
- **技术：** Schema 跟踪 + 上下文跟踪双模块

#### **趋势 4：知识蒸馏与结构化思维链**
- **代表研究：** "Knowledge Distillation with Structured Chain-of-Thought for Text-to-SQL" (2025 年 12 月)
- **目标：** 将大模型能力蒸馏到小模型
- **方法：** 结构化 CoT 作为中间表示

#### **趋势 5：幻觉检测与不可回答问题识别**
- **代表研究：** 
  - "Hallucination Detection for LLM-based Text-to-SQL Generation via Two-Stage Metamorphic Testing" (2025 年 12 月)
  - "Query Carefully: Detecting the Unanswerables in Text-to-SQL Tasks" (2025 年 12 月)
- **重要性：** 提高系统可靠性和用户信任

#### **趋势 6：成本优化（Reasoning vs Non-Reasoning 模型）**
- **代表研究：** "Cost Trade-offs of Reasoning and Non-Reasoning Large Language Models in Text-to-SQL" (2025 年 12 月)
- **发现：** 根据查询复杂度动态选择模型类型
- **策略：** 简单查询用小模型，复杂查询用推理模型

### 3.2 产品趋势

#### **趋势 1：企业级安全与合规**
- 行级安全（Row-Level Security）
- 审计日志（Audit Logs）
- 权限控制（Access Control）
- 数据隐私保护（Data Privacy）

#### **趋势 2：低代码/无代码界面**
- 预构建 UI 组件（如 Vanna 的 `<vanna-chat>`）
- 可视化 schema 设计器
- 自然语言配置

#### **趋势 3：流式响应与实时交互**
- 流式 SQL 生成
- 实时表格和图表渲染
- 进度更新

#### **趋势 4：多模态支持**
- 文本 + 视觉输入（如截图生成查询）
- 语音输入
- 图表输出

#### **趋势 5：自主 Agent**
- 自主数据探索
- 假设检验
- 异常检测与告警

### 3.3 市场趋势

| 趋势 | 描述 | 影响 |
|------|------|------|
| **开源模型崛起** | SQLCoder 等开源模型超越闭源模型 | 降低企业采用门槛 |
| **垂直化专用模型** | 针对特定行业/场景优化的模型 | 提高准确率 |
| **云厂商整合** | Snowflake、Databricks 等内置 Text-to-SQL | 成为标准功能 |
| **评估标准化** | SQLEval 等开源评估框架 | 促进技术竞争 |
| **Agent 工程平台** | LangSmith 等平台的成熟 | 加速应用开发 |

---

## 四、企业级 Text-to-SQL 落地案例

### 4.1 典型应用场景

#### **场景 1：数据分析与 BI**
- **用户：** 业务分析师、数据科学家
- **需求：** 快速生成复杂查询，无需手写 SQL
- **价值：** 减少 80%+ 查询时间
- **案例：**
  - **MindsDB：** 电商团队实时 AI 分析，无需 ETL
  - **Vanna：** 多租户 SaaS 数据分析应用

#### **场景 2：客户支持自动化**
- **用户：** 客服团队
- **需求：** 快速查询客户信息、订单状态
- **价值：** 减少人工查询时间，提高响应速度
- **案例：**
  - **MindsDB + Gong：** 对话智能，分析呼叫数据
  - **Janus 系统：** AI 驱动的客户支持帮助台

#### **场景 3：CRM 智能**
- **用户：** 销售团队
- **需求：** 查询 Salesforce 数据，生成销售报告
- **价值：** 无需等待数据团队，自助分析
- **案例：**
  - **MindsDB + Salesforce：** 解锁 CRM 智能
  - **Vanna：** 销售管道分析

#### **场景 4：财务分析**
- **用户：** 财务团队
- **需求：** 跨系统财务数据聚合分析
- **价值：** 减少手工报表时间
- **案例：**
  - **MindsDB：** 财务分析 Agent，混合搜索
  - **IBM watsonx：** D&B 供应商风险评估节省 10% 时间

#### **场景 5：企业知识搜索**
- **用户：** 全体员工
- **需求：** 搜索内部文档、支持工单、知识库
- **价值：** 快速找到信息，减少重复工作
- **案例：**
  - **MindsDB Knowledge Base：** 企业知识搜索
  - **语义搜索 Agent：** 跨非结构化数据源搜索

### 4.2 企业落地最佳实践

#### **4.2.1 安全与权限**
```
最佳实践：
1. 实施行级安全（Row-Level Security）
2. 所有查询记录审计日志
3. 基于角色的访问控制（RBAC）
4. 敏感数据脱敏
5. 每用户配额限制
```

#### **4.2.2 性能优化**
```
最佳实践：
1. Schema 元数据缓存
2. 查询结果缓存
3. 智能模型选择（简单查询用小模型）
4. 并发查询限制
5. 数据库索引优化
```

#### **4.2.3 用户体验**
```
最佳实践：
1. 流式响应，减少等待焦虑
2. 可视化结果（表格、图表）
3. SQL 解释功能（帮助用户学习）
4. 多轮对话支持
5. 错误友好提示
```

#### **4.2.4 运维监控**
```
最佳实践：
1. 查询延迟监控
2. 准确率追踪（使用测试套件）
3. 成本监控（token 使用量）
4. 用户满意度反馈
5. 异常检测与告警
```

### 4.3 真实企业案例

#### **案例 1：Deutsche Bahn（德国铁路）**
- **挑战：** 跨系统测试耗时
- **方案：** 使用 AskUI 进行 UI 自动化测试
- **结果：**
  - 测试时间减少 80%
  - 测试覆盖率提高 95%
  - ROI 达到 300%
- **引用：** "AskUI 将我们的测试时间减少了 80%，并无缝集成到 GitLab 流水线中。"

#### **案例 2：Vodafone**
- **挑战：** 客户旅程测试周转时间长
- **方案：** IBM watsonx Orchestrate
- **结果：** 周转时间提升 99%

#### **案例 3：US Open（美国网球公开赛）**
- **挑战：** 实时分析大量比赛数据
- **方案：** IBM watsonx
- **结果：** 捕获和分析 700 万数据点

#### **案例 4：IBM CIO Organization**
- **挑战：** 手动创建 Ansible Playbook 耗时
- **方案：** watsonx Code Assistant
- **结果：** 节省 40%+ 时间

#### **案例 5：Dun & Bradstreet**
- **挑战：** 供应商风险评估耗时
- **方案：** watsonx Ask Procurement
- **结果：** 客户评估时间节省 10%+

---

## 五、技术选型建议

### 5.1 开源 vs 商业

| 维度 | 开源方案 | 商业方案 |
|------|----------|----------|
| **成本** | 低（仅基础设施） | 高（订阅费） |
| **定制性** | 高 | 中 |
| **支持** | 社区 | 企业 SLA |
| **安全性** | 自行负责 | 厂商提供 |
| **部署** | 自托管 | SaaS/私有化 |

**推荐：**
- **初创公司/小团队：** 开源方案（Vanna、SQLCoder）
- **中大型企业：** 商业方案 + 自研混合
- **高安全要求：** 自托管开源方案

### 5.2 模型选择

| 场景 | 推荐模型 | 理由 |
|------|----------|------|
| **简单查询** | SQLCoder-7B | 快速、低成本 |
| **复杂查询** | SQLCoder-70B / GPT-4 | 高准确率 |
| **成本敏感** | 小模型 + RAG | 平衡成本与效果 |
| **企业部署** | 自托管 SQLCoder | 数据隐私 |
| **多轮对话** | Track-SQL 架构 | 上下文跟踪 |

### 5.3 架构选择

| 规模 | 推荐架构 | 说明 |
|------|----------|------|
| **小型（<100 用户）** | 单 Agent + 缓存 | 简单高效 |
| **中型（100-1000 用户）** | 多 Agent + RAG | 平衡性能与成本 |
| **大型（>1000 用户）** | 多 Agent + 分布式 + 监控 | 高可用、可观测 |

---

## 六、风险与挑战

### 6.1 技术风险

| 风险 | 描述 | 缓解措施 |
|------|------|----------|
| **准确率不足** | 复杂查询生成错误 SQL | 使用测试套件验证、人工审核 |
| **幻觉问题** | 模型生成不存在的表/列 | Schema 验证、幻觉检测 |
| **性能问题** | 查询延迟高 | 缓存、模型蒸馏、并发优化 |
| **安全漏洞** | SQL 注入、数据泄露 | 参数化查询、权限控制、审计 |

### 6.2 业务风险

| 风险 | 描述 | 缓解措施 |
|------|------|----------|
| **用户信任** | 用户不信任 AI 生成的 SQL | 提供 SQL 解释、透明度 |
| **成本失控** | LLM token 使用量激增 | 配额限制、成本监控 |
| **依赖风险** | 过度依赖单一供应商 | 多供应商策略、开源备选 |
| **合规风险** | 数据隐私法规 | 数据脱敏、审计日志、合规审查 |

---

## 七、结论与建议

### 7.1 核心结论

1. **Text-to-SQL 技术已成熟：** 开源模型（SQLCoder）在特定任务上超越 GPT-4，企业级产品（Vanna、MindsDB）提供完整解决方案。

2. **2025-2026 年关键趋势：** 多 Agent 协作、模式演化鲁棒性、多轮对话、成本优化、幻觉检测。

3. **企业落地可行：** 已有多个成功案例（Deutsche Bahn、Vodafone、US Open 等），关键在安全、性能和用户体验。

4. **开源生态繁荣：** SQLCoder、Vanna、MindsDB 等开源项目降低采用门槛，促进技术创新。

### 7.2 行动建议

#### **对于技术团队：**
1. **评估需求：** 明确使用场景（数据分析、客户支持、CRM 等）
2. **技术选型：** 根据规模和安全要求选择开源/商业方案
3. **POC 验证：** 使用真实数据测试准确率和性能
4. **安全优先：** 实施行级安全、审计日志、权限控制
5. **持续优化：** 监控准确率、成本、用户满意度

#### **对于企业决策者：**
1. **战略投资：** Text-to-SQL 是 AI 落地的重要场景，建议纳入 AI 战略
2. **人才培养：** 培训团队掌握 Text-to-SQL 技术
3. **合作伙伴：** 选择有企业经验的供应商
4. **合规审查：** 确保符合数据隐私和安全法规
5. **渐进式采用：** 从低风险场景开始，逐步扩展

### 7.3 未来展望

**2026-2027 年预测：**
- **自主 Agent 普及：** Text-to-SQL Agent 能够自主探索数据、发现洞察
- **多模态融合：** 文本 + 视觉 + 语音输入，图表 + 报告输出
- **行业专用模型：** 金融、医疗、零售等行业专用 Text-to-SQL 模型
- **标准化评估：** 行业统一的准确率和性能评估标准
- **成本大幅下降：** 模型优化和竞争导致使用成本下降 50%+

---

## 附录

### A. 关键资源链接

| 资源 | 链接 |
|------|------|
| **Vanna AI** | https://vanna.ai, https://github.com/vanna-ai/vanna |
| **Defog SQLCoder** | https://defog.ai, https://github.com/defog-ai/sqlcoder |
| **SQL AI** | https://sqlai.app |
| **MindsDB** | https://mindsdb.com, https://github.com/mindsdb/mindsdb |
| **LangChain** | https://langchain.com |
| **IBM watsonx** | https://www.ibm.com/products/watsonx |
| **Spider 数据集** | https://yale-lily.github.io/spider |
| **SQLCoder Demo** | https://defog.ai/sqlcoder-demo |

### B. 关键论文

1. **EvoSchema** (2026-03): Towards Text-to-SQL Robustness Against Schema Evolution
2. **Track-SQL** (2026-03): Enhancing Generative Language Models with Dual-Extractive Modules for Multi-turn Text-to-SQL
3. **SQaLe** (2025-12): A Large Text-to-SQL Corpus Grounded in Real Schemas
4. **AGRO-SQL** (2025-12): Agentic Group-Relative Optimization with High-Fidelity Data Synthesis
5. **Multi-agent Text2SQL** (2025-12): A Multi-agent Framework using Small Language Models and Execution Feedback
6. **Knowledge Distillation** (2025-12): Knowledge Distillation with Structured Chain-of-Thought for Text-to-SQL

### C. 评估工具

| 工具 | 用途 | 链接 |
|------|------|------|
| **Spider Eval** | 准确率和执行准确率 | https://github.com/taoyds/spider |
| **SQLEval** | Defog 开源评估框架 | https://github.com/defog-ai/sql-eval |
| **Test Suite Accuracy** | 测试用例验证 | https://github.com/taoyds/test-suite-sql-eval |

---

**报告完成日期：** 2026 年 3 月 23 日  
**调研方法：** 网络搜索、官方文档分析、GitHub 仓库调研、学术论文分析  
**报告作者：** AI 研究助手
