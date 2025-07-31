# Create Brownfield Story Task （创建Brownfield Story任务）

## Purpose （目的）

为具有非标准文档的brownfield项目创建详细、可实施的story。此任务弥合了各种文档格式（document-project输出、brownfield PRD、epic或用户文档）与Dev agent可执行story之间的差距。

## When to Use This Task （何时使用此任务）

**Use this task when （在以下情况使用此任务）**:

- 处理具有非标准文档的brownfield项目
- 需要从document-project输出创建story
- 从没有完整PRD/架构的brownfield epic工作
- 现有项目文档不遵循BMad v4+结构
- 在story创建过程中需要从用户收集额外上下文

**Use create-next-story when （在以下情况使用create-next-story）**:

- 使用正确分片的PRD和v4架构文档
- 遵循标准greenfield或文档完善的brownfield工作流程
- 所有技术上下文都以结构化格式提供

## Task Execution Instructions （任务执行指令）

### 0. Documentation Context （文档上下文）

按此顺序检查可用文档：

1. **Sharded PRD/Architecture （分片PRD/架构）** (docs/prd/, docs/architecture/)
    - 如果找到，建议使用create-next-story任务

2. **Brownfield Architecture Document （Brownfield架构文档）** (docs/brownfield-architecture.md或类似)
    - 由document-project任务创建
    - 包含实际系统状态、技术债务、变通方法

3. **Brownfield PRD （Brownfield PRD）** (docs/prd.md)
    - 可能包含嵌入的技术详情

4. **Epic Files （Epic文件）** (docs/epics/或类似)
    - 由brownfield-create-epic任务创建

5. **User-Provided Documentation （用户提供的文档）**
    - 要求用户指定位置和格式

### 1. Story Identification and Context Gathering （Story识别和上下文收集）

#### 1.1 Identify Story Source （识别Story来源）

基于可用文档：

- **From Brownfield PRD （来自Brownfield PRD）**: 从epic章节提取story
- **From Epic Files （来自Epic文件）**: 读取epic定义和story列表
- **From User Direction （来自用户指导）**: 询问用户要实施哪个具体增强
- **No Clear Source （无明确来源）**: 与用户合作定义story范围

#### 1.2 Gather Essential Context （收集基本上下文）

关键：对于brownfield story，您必须收集足够的上下文以安全实施。准备在信息缺失时询问用户。

**Required Information Checklist （必需信息检查清单）**:

- [ ] 哪些现有功能可能受到影响？
- [ ] 与当前代码的集成点是什么？
- [ ] 应该遵循哪些模式（带示例）？
- [ ] 存在哪些技术约束？
- [ ] 有哪些需要知道的"陷阱"或变通方法？

如果任何必需信息缺失，列出缺失信息并要求用户提供。

### 2. Extract Technical Context from Available Sources （从可用来源提取技术上下文）

#### 2.1 From Document-Project Output （来自Document-Project输出）

如果使用来自document-project的brownfield-architecture.md：

- **Technical Debt Section （技术债务章节）**: 注意影响此story的任何变通方法
- **Key Files Section （关键文件章节）**: 识别需要修改的文件
- **Integration Points （集成点）**: 查找现有集成模式
- **Known Issues （已知问题）**: 检查story是否触及问题区域
- **Actual Tech Stack （实际技术栈）**: 验证版本和约束

#### 2.2 From Brownfield PRD （来自Brownfield PRD）

如果使用brownfield PRD：

- **Technical Constraints Section （技术约束章节）**: 提取所有相关约束
- **Integration Requirements （集成要求）**: 注意兼容性要求
- **Code Organization （代码组织）**: 遵循指定模式
- **Risk Assessment （风险评估）**: 理解潜在影响

#### 2.3 From User Documentation （来自用户文档）

要求用户帮助识别：

- 相关技术规格
- 要遵循的现有代码示例
- 集成要求
- 项目中使用的测试方法

### 3. Story Creation with Progressive Detail Gathering （通过渐进式详情收集创建Story）

#### 3.1 Create Initial Story Structure （创建初始Story结构）

使用story模板开始，填入已知内容：

```markdown
# Story {{Enhancement Title}}

## Status: Draft

## Story

As a {{user_type}},
I want {{enhancement_capability}},
so that {{value_delivered}}.

## Context Source

- Source Document （源文档）: {{document name/type}}
- Enhancement Type （增强类型）: {{single feature/bug fix/integration/etc}}
- Existing System Impact （现有系统影响）: {{brief assessment}}
```

#### 3.2 Develop Acceptance Criteria （制定验收标准）

关键：对于brownfield，始终包括关于维护现有功能的标准

标准结构：

1. 新功能按指定工作
2. 现有{{affected feature}}继续无变化工作
3. 与{{existing system}}的集成保持当前行为
4. {{related area}}无回归
5. 性能保持在可接受范围内

#### 3.3 Gather Technical Guidance （收集技术指导）

关键：如果信息缺失，这里需要与用户交互

使用可用信息创建Dev Technical Guidance章节：

```markdown
## Dev Technical Guidance

### Existing System Context （现有系统上下文）

[从可用文档提取]

### Integration Approach （集成方法）

[基于找到的模式或询问用户]

### Technical Constraints （技术约束）

[来自文档或用户输入]

### Missing Information （缺失信息）

关键：列出dev需要的任何找不到的内容，并要求缺失信息
```

### 4. Task Generation with Safety Checks （带安全检查的任务生成）

#### 4.1 Generate Implementation Tasks （生成实施任务）

基于收集的上下文，创建任务：

- 如果系统理解不完整，包括探索任务
- 为现有功能添加验证任务
- 包括回滚考虑
- 当已知时引用特定文件/模式

brownfield的示例任务结构：

```markdown
## Tasks / Subtasks

- [ ] Task 1: Analyze existing {{component/feature}} implementation
    - [ ] Review {{specific files}} for current patterns
    - [ ] Document integration points
    - [ ] Identify potential impacts

- [ ] Task 2: Implement {{new functionality}}
    - [ ] Follow pattern from {{example file}}
    - [ ] Integrate with {{existing component}}
    - [ ] Maintain compatibility with {{constraint}}

- [ ] Task 3: Verify existing functionality
    - [ ] Test {{existing feature 1}} still works
    - [ ] Verify {{integration point}} behavior unchanged
    - [ ] Check performance impact

- [ ] Task 4: Add tests
    - [ ] Unit tests following {{project test pattern}}
    - [ ] Integration test for {{integration point}}
    - [ ] Update existing tests if needed
```

### 5. Risk Assessment and Mitigation （风险评估和缓解）

关键：对于brownfield - 始终包括风险评估

为brownfield特定风险添加章节：

```markdown
## Risk Assessment

### Implementation Risks （实施风险）

- **Primary Risk （主要风险）**: {{main risk to existing system}}
- **Mitigation （缓解）**: {{how to address}}
- **Verification （验证）**: {{how to confirm safety}}

### Rollback Plan （回滚计划）

- {{Simple steps to undo changes if needed}}

### Safety Checks （安全检查）

- [ ] Existing {{feature}} tested before changes
- [ ] Changes can be feature-flagged or isolated
- [ ] Rollback procedure documented
```

### 6. Final Story Validation （最终Story验证）

在最终确定之前：

1. **Completeness Check （完整性检查）**:
    - [ ] Story有明确范围和验收标准
    - [ ] 技术上下文足以实施
    - [ ] 集成方法已定义
    - [ ] 风险已识别并缓解

2. **Safety Check （安全检查）**:
    - [ ] 包括现有功能保护
    - [ ] 回滚计划可行
    - [ ] 测试涵盖新功能和现有功能

3. **Information Gaps （信息差距）**:
    - [ ] 所有关键缺失信息已从用户收集
    - [ ] 剩余未知数已为dev agent记录
    - [ ] 在需要时添加探索任务

### 7. Story Output Format （Story输出格式）

使用适当命名保存story：

- 如果来自epic: `docs/stories/epic-{n}-story-{m}.md`
- 如果独立: `docs/stories/brownfield-{feature-name}.md`
- 如果顺序: 遵循现有story编号

包括说明文档上下文的标题：

```markdown
# Story: {{Title}}

<!-- Source: {{documentation type used}} -->
<!-- Context: Brownfield enhancement to {{existing system}} -->

## Status: Draft

[Rest of story content...]
```

### 8. Handoff Communication （移交沟通）

向用户提供清晰的移交：

```text
Brownfield story created: {{story title}}

Source Documentation （源文档）: {{what was used}}
Story Location （Story位置）: {{file path}}

Key Integration Points Identified （识别的关键集成点）:
- {{integration point 1}}
- {{integration point 2}}

Risks Noted （注意的风险）:
- {{primary risk}}

{{If missing info}}:
Note: Some technical details were unclear. The story includes exploration tasks to gather needed information during implementation.

Next Steps （下一步）:
1. Review story for accuracy
2. Verify integration approach aligns with your system
3. Approve story or request adjustments
4. Dev agent can then implement with safety checks
```

## Success Criteria （成功标准）

brownfield story创建成功时：

1. Story可以在不要求dev搜索多个文档的情况下实施
2. 集成方法清晰且对现有系统安全
3. 所有可用技术上下文已提取并组织
4. 缺失信息已识别并解决
5. 风险已记录并制定缓解策略
6. Story包括现有功能验证
7. 回滚方法已定义

## Important Notes （重要说明）

- 此任务专门用于具有非标准文档的brownfield项目
- 始终优先考虑现有系统稳定性而非新功能
- 当有疑问时，添加探索和验证任务
- 询问用户澄清比做出假设更好
- 每个story对dev agent应该是自包含的
- 在可用时包括对现有代码模式的引用
