# Create Deep Research Prompt Task （创建深度研究提示任务）

此任务帮助为各种类型的深度分析创建综合研究提示。它可以处理来自头脑风暴会话、项目简介、市场研究或特定研究问题的输入，以生成针对更深层次调查的目标提示。

## Purpose （目的）

生成结构良好的研究提示，这些提示：

- 定义明确的研究目标和范围
- 指定适当的研究方法
- 概述预期的交付物和格式
- 指导复杂主题的系统性调查
- 确保捕获可操作的见解

## Research Type Selection （研究类型选择）

关键：首先，帮助用户根据他们的需求和提供的任何输入文档选择最合适的研究重点。

### 1. Research Focus Options （研究重点选项）

向用户呈现这些编号选项：

1. **Product Validation Research （产品验证研究）**
    - 验证产品假设和市场适应性
    - 测试关于用户需求和解决方案的假设
    - 评估技术和业务可行性
    - 识别风险和缓解策略

2. **Market Opportunity Research （市场机会研究）**
    - 分析市场规模和增长潜力
    - 识别市场细分和动态
    - 评估市场进入策略
    - 评估时机和市场准备度

3. **User & Customer Research （用户和客户研究）**
    - 深入用户角色和行为
    - 理解待完成工作和痛点
    - 映射客户旅程和接触点
    - 分析支付意愿和价值感知

4. **Competitive Intelligence Research （竞争情报研究）**
    - 详细的竞争对手分析和定位
    - 功能和能力比较
    - 商业模式和策略分析
    - 识别竞争优势和差距

5. **Technology & Innovation Research （技术和创新研究）**
    - 评估技术趋势和可能性
    - 评估技术方法和架构
    - 识别新兴技术和颠覆
    - 分析构建vs购买vs合作伙伴选项

6. **Industry & Ecosystem Research （行业和生态系统研究）**
    - 映射行业价值链和动态
    - 识别关键参与者和关系
    - 分析监管和合规因素
    - 理解合作伙伴机会

7. **Strategic Options Research （战略选项研究）**
    - 评估不同的战略方向
    - 评估商业模式替代方案
    - 分析进入市场策略
    - 考虑扩展和扩展路径

8. **Risk & Feasibility Research （风险和可行性研究）**
    - 识别和评估各种风险因素
    - 评估实施挑战
    - 分析资源要求
    - 考虑监管和法律影响

9. **Custom Research Focus （自定义研究重点）**
    - 用户定义的研究目标
    - 专业领域调查
    - 跨功能研究需求

### 2. Input Processing （输入处理）

**If Project Brief provided （如果提供了项目简介）**:

- 提取关键产品概念和目标
- 识别目标用户和使用案例
- 注意技术约束和偏好
- 突出不确定性和假设

**If Brainstorming Results provided （如果提供了头脑风暴结果）**:

- 综合主要想法和主题
- 识别需要验证的领域
- 提取要测试的假设
- 注意要探索的创意方向

**If Market Research provided （如果提供了市场研究）**:

- 基于已识别的机会
- 深化特定市场见解
- 验证初步发现
- 探索相邻可能性

**If Starting Fresh （如果从头开始）**:

- 通过问题收集基本上下文
- 定义问题空间
- 澄清研究目标
- 建立成功标准

## Process （流程）

### 3. Research Prompt Structure （研究提示结构）

关键：协作开发包含这些组件的综合研究提示。

#### A. Research Objectives （研究目标）

关键：与用户协作阐明研究的具体、明确目标。

- 主要研究目标和目的
- 研究将告知的关键决策
- 研究的成功标准
- 约束和边界

#### B. Research Questions （研究问题）

关键：与用户协作开发按主题组织的具体、可操作的研究问题。

**Core Questions （核心问题）**:

- 必须回答的中心问题
- 问题优先级排序
- 问题之间的依赖关系

**Supporting Questions （支持问题）**:

- 额外的上下文构建问题
- 有则更好的见解
- 面向未来的考虑

#### C. Research Methodology （研究方法）

**Data Collection Methods （数据收集方法）**:

- 二次研究来源
- 主要研究方法（如适用）
- 数据质量要求
- 来源可信度标准

**Analysis Frameworks （分析框架）**:

- 要应用的具体框架
- 比较标准
- 评估方法
- 综合方法

#### D. Output Requirements （输出要求）

**Format Specifications （格式规格）**:

- 执行摘要要求
- 详细发现结构
- 视觉/表格呈现
- 支持文档

**Key Deliverables （关键交付物）**:

- 必须有的章节和见解
- 决策支持元素
- 面向行动的建议
- 风险和不确定性文档

### 4. Prompt Generation （提示生成）

**Research Prompt Template （研究提示模板）**:

```markdown
## Research Objective （研究目标）

[Clear statement of what this research aims to achieve （关于此研究旨在实现什么的清晰陈述）]

## Background Context （背景上下文）

[Relevant information from project brief, brainstorming, or other inputs （来自项目简介、头脑风暴或其他输入的相关信息）]

## Research Questions （研究问题）

### Primary Questions (Must Answer) （主要问题（必须回答））

1. [Specific, actionable question （具体、可操作的问题）]
2. [Specific, actionable question （具体、可操作的问题）]
   ...

### Secondary Questions (Nice to Have) （次要问题（有则更好））

1. [Supporting question （支持问题）]
2. [Supporting question （支持问题）]
   ...

## Research Methodology （研究方法）

### Information Sources （信息来源）

- [Specific source types and priorities （具体来源类型和优先级）]

### Analysis Frameworks （分析框架）

- [Specific frameworks to apply （要应用的具体框架）]

### Data Requirements （数据要求）

- [Quality, recency, credibility needs （质量、时效性、可信度需求）]

## Expected Deliverables （预期交付物）

### Executive Summary （执行摘要）

- Key findings and insights （关键发现和见解）
- Critical implications （关键影响）
- Recommended actions （建议行动）

### Detailed Analysis （详细分析）

[Specific sections needed based on research type （基于研究类型需要的具体章节）]

### Supporting Materials （支持材料）

- Data tables （数据表）
- Comparison matrices （比较矩阵）
- Source documentation （来源文档）

## Success Criteria （成功标准）

[How to evaluate if research achieved its objectives （如何评估研究是否实现其目标）]

## Timeline and Priority （时间线和优先级）

[If applicable, any time constraints or phasing （如适用，任何时间约束或分阶段）]
```

### 5. Review and Refinement （审查和改进）

1. **Present Complete Prompt （呈现完整提示）**
    - 显示完整的研究提示
    - 解释关键元素和理由
    - 突出任何做出的假设

2. **Gather Feedback （收集反馈）**
    - 目标是否清晰正确？
    - 问题是否解决了所有关注点？
    - 范围是否适当？
    - 输出要求是否充分？

3. **Refine as Needed （根据需要改进）**
    - 纳入用户反馈
    - 调整范围或重点
    - 添加缺失元素
    - 澄清歧义

### 6. Next Steps Guidance （下一步指导）

**Execution Options （执行选项）**:

1. **Use with AI Research Assistant （与AI研究助手一起使用）**: 向具有研究能力的AI模型提供此提示
2. **Guide Human Research （指导人类研究）**: 用作手动研究工作的框架
3. **Hybrid Approach （混合方法）**: 使用此结构结合AI和人类研究

**Integration Points （集成点）**:

- 发现将如何进入下一阶段
- 哪些团队成员应该审查结果
- 如何验证发现
- 何时重新访问或扩展研究

## Important Notes （重要说明）

- 研究提示的质量直接影响收集的见解质量
- 在研究问题中要具体而不是一般
- 考虑当前状态和未来影响
- 平衡全面性和重点
- 清楚记录假设和限制
- 计划基于初步发现的迭代改进
