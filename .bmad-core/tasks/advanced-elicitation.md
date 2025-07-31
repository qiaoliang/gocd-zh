# Advanced Elicitation Task （高级启发任务）

## Purpose （目的）

- 提供可选的反思和头脑风暴行动以增强内容质量
- 通过结构化启发技术实现更深层次的想法探索
- 通过多种分析视角支持迭代改进
- 可在模板驱动的文档创建或任何聊天对话中使用

## Usage Scenarios （使用场景）

### Scenario 1: Template Document Creation （场景1：模板文档创建）

在文档创建过程中输出章节后：

1. **Section Review （章节审查）**: 要求用户审查已起草的章节
2. **Offer Elicitation （提供启发）**: 呈现9个精心选择的启发方法
3. **Simple Selection （简单选择）**: 用户输入数字(0-8)来使用方法，或输入9继续
4. **Execute & Loop （执行和循环）**: 应用选定的方法，然后重新提供选择直到用户继续

### Scenario 2: General Chat Elicitation （场景2：通用聊天启发）

用户可以对任何agent输出请求高级启发：

- 用户说"do advanced elicitation"或类似的话
- Agent为上下文选择9个相关方法
- 相同的简单0-9选择过程

## Task Instructions （任务指令）

### 1. Intelligent Method Selection （智能方法选择）

**Context Analysis （上下文分析）**: 在呈现选项之前，分析：

- **Content Type （内容类型）**: 技术规格、用户故事、架构、需求等
- **Complexity Level （复杂度级别）**: 简单、中等或复杂内容
- **Stakeholder Needs （利益相关者需求）**: 谁将使用这些信息
- **Risk Level （风险级别）**: 高影响决策与常规项目
- **Creative Potential （创意潜力）**: 创新或替代方案的机会

**Method Selection Strategy （方法选择策略）**:

1. **Always Include Core Methods （始终包含核心方法）** (选择3-4个):
    - Expand or Contract for Audience （为受众扩展或收缩）
    - Critique and Refine （批评和改进）
    - Identify Potential Risks （识别潜在风险）
    - Assess Alignment with Goals （评估与目标的一致性）

2. **Context-Specific Methods （上下文特定方法）** (选择4-5个):
    - **Technical Content （技术内容）**: Tree of Thoughts, ReWOO, Meta-Prompting
    - **User-Facing Content （面向用户的内容）**: Agile Team Perspective, Stakeholder Roundtable
    - **Creative Content （创意内容）**: Innovation Tournament, Escape Room Challenge
    - **Strategic Content （战略内容）**: Red Team vs Blue Team, Hindsight Reflection

3. **Always Include （始终包含）**: "Proceed / No Further Actions" 作为选项9

### 2. Section Context and Review （章节上下文和审查）

在输出章节后调用时：

1. **Provide Context Summary （提供上下文摘要）**: 对用户应该在该章节中寻找的内容提供简短的1-2句话摘要

2. **Explain Visual Elements （解释视觉元素）**: 如果章节包含图表，在提供启发选项之前简要解释它们

3. **Clarify Scope Options （澄清范围选项）**: 如果章节包含多个不同项目，告知用户他们可以将启发行动应用于：
    - 整个章节作为一个整体
    - 章节内的个别项目（选择行动时指定哪个项目）

### 3. Present Elicitation Options （呈现启发选项）

**Review Request Process （审查请求过程）**:

- 要求用户审查已起草的章节
- 在同一消息中，告知他们可以建议直接更改或选择启发方法
- 呈现9个智能选择的方法(0-8)加上"Proceed"（继续）(9)
- 保持描述简短 - 只是方法名称
- 等待简单的数字选择

**Action List Presentation Format （行动列表呈现格式）**:

```text
**Advanced Elicitation Options （高级启发选项）**
Choose a number (0-8) or 9 to proceed （选择一个数字(0-8)或9继续）:

0. [Method Name （方法名称）]
1. [Method Name （方法名称）]
2. [Method Name （方法名称）]
3. [Method Name （方法名称）]
4. [Method Name （方法名称）]
5. [Method Name （方法名称）]
6. [Method Name （方法名称）]
7. [Method Name （方法名称）]
8. [Method Name （方法名称）]
9. Proceed / No Further Actions （继续/无需进一步行动）
```

**Response Handling （响应处理）**:

- **Numbers 0-8 （数字0-8）**: 执行选定的方法，然后重新提供选择
- **Number 9 （数字9）**: 继续下一章节或继续对话
- **Direct Feedback （直接反馈）**: 应用用户建议的更改并继续

### 4. Method Execution Framework （方法执行框架）

**Execution Process （执行过程）**:

1. **Retrieve Method （检索方法）**: 从启发方法数据文件访问特定的启发方法
2. **Apply Context （应用上下文）**: 从您当前角色的角度执行方法
3. **Provide Results （提供结果）**: 提供与内容相关的见解、批评或替代方案
4. **Re-offer Choice （重新提供选择）**: 再次呈现相同的9个选项，直到用户选择9或给出直接反馈

**Execution Guidelines （执行指南）**:

- **Be Concise （简洁）**: 专注于可操作的见解，而不是冗长的解释
- **Stay Relevant （保持相关性）**: 将所有启发与分析的具体内容联系起来
- **Identify Personas （识别角色）**: 对于多角色方法，清楚识别哪个观点在发言
- **Maintain Flow （保持流程）**: 保持过程高效进行
