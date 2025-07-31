# Create Next Story Task （创建下一个Story任务）

## Purpose （目的）

基于项目进度和epic定义识别下一个逻辑story，然后使用`Story Template`准备综合、自包含和可操作的story文件。此任务确保story包含所有必要的技术上下文、要求和验收标准，使其准备好由Developer Agent高效实施，无需额外研究或寻找自己的上下文。

## SEQUENTIAL Task Execution (Do not proceed until current Task is complete) （顺序任务执行（在当前任务完成之前不要继续））

### 0. Load Core Configuration and Check Workflow （加载核心配置并检查工作流程）

- 从项目根目录加载 `{root}/core-config.yaml`
- 如果文件不存在，停止并告知用户："core-config.yaml not found. This file is required for story creation. You can either: 1) Copy it from GITHUB bmad-core/core-config.yaml and configure it for your project OR 2) Run the BMad installer against your project to upgrade and add the file automatically. Please add and configure core-config.yaml before proceeding."
- 提取关键配置：`devStoryLocation`, `prd.*`, `architecture.*`, `workflow.*`

### 1. Identify Next Story for Preparation （识别要准备的下一个Story）

#### 1.1 Locate Epic Files and Review Existing Stories （定位Epic文件并审查现有Story）

- 基于配置中的`prdSharded`，定位epic文件（分片位置/模式或整体PRD章节）
- 如果`devStoryLocation`有story文件，加载最高的`{epicNum}.{storyNum}.story.md`文件
- **If highest story exists （如果最高story存在）**:
    - 验证状态是否为'Done'。如果不是，提醒用户："ALERT: Found incomplete story! File: {lastEpicNum}.{lastStoryNum}.story.md Status: [current status] You should fix this story first, but would you like to accept risk & override to create the next story in draft?"
    - 如果继续，选择当前epic中的下一个顺序story
    - 如果epic完成，提示用户："Epic {epicNum} Complete: All stories in Epic {epicNum} have been completed. Would you like to: 1) Begin Epic {epicNum + 1} with story 1 2) Select a specific story to work on 3) Cancel story creation"
    - **关键**: 永远不要自动跳到另一个epic。用户必须明确指示创建哪个story。
- **If no story files exist （如果不存在story文件）**: 下一个story总是1.1（第一个epic的第一个story）
- 向用户宣布识别的story："Identified next story for preparation: {epicNum}.{storyNum} - {Story Title}"

### 2. Gather Story Requirements and Previous Story Context （收集Story要求和上一个Story上下文）

- 从识别的epic文件提取story要求
- 如果上一个story存在，审查Dev Agent Record章节的：
    - Completion Notes and Debug Log References
    - Implementation deviations and technical decisions
    - Challenges encountered and lessons learned
- 提取为当前story准备提供信息的相关见解

### 3. Gather Architecture Context （收集架构上下文）

#### 3.1 Determine Architecture Reading Strategy （确定架构阅读策略）

- **If `architectureVersion: >= v4` and `architectureSharded: true`**: 读取 `{architectureShardedLocation}/index.md` 然后遵循下面的结构化阅读顺序
- **Else**: 对类似章节使用整体`architectureFile`

#### 3.2 Read Architecture Documents Based on Story Type （基于Story类型读取架构文档）

**For ALL Stories （对于所有Story）**: tech-stack.md, unified-project-structure.md, coding-standards.md, testing-strategy.md

**For Backend/API Stories, additionally （对于后端/API Story，另外）**: data-models.md, database-schema.md, backend-architecture.md, rest-api-spec.md, external-apis.md

**For Frontend/UI Stories, additionally （对于前端/UI Story，另外）**: frontend-architecture.md, components.md, core-workflows.md, data-models.md

**For Full-Stack Stories （对于全栈Story）**: 读取上面的后端和前端章节

#### 3.3 Extract Story-Specific Technical Details （提取Story特定技术详情）

仅提取与实施当前story直接相关的信息。不要发明源文档中没有的新库、模式或标准。

提取：

- story将使用的特定数据模型、模式或结构
- story必须实施或消费的API端点
- story中UI元素的组件规格
- 新代码的文件路径和命名约定
- 特定于story功能的技术要求
- 影响story的安全或性能考虑

始终引用源文档：`[Source: architecture/{filename}.md#{section}]`

### 4. Verify Project Structure Alignment （验证项目结构对齐）

- 将story要求与来自`docs/architecture/unified-project-structure.md`的项目结构指南交叉引用
- 确保文件路径、组件位置或模块名称与定义的结构对齐
- 在story草案的"Project Structure Notes"章节中记录任何结构冲突

### 5. Populate Story Template with Full Context （用完整上下文填充Story模板）

- 使用Story Template创建新的story文件：`{devStoryLocation}/{epicNum}.{storyNum}.story.md`
- 填写基本story信息：Title, Status (Draft), Story statement, Acceptance Criteria from Epic
- **`Dev Notes` section (关键)**:
    - 关键：此章节必须仅包含从架构文档提取的信息。永远不要发明或假设技术详情。
    - 包括来自步骤2-3的所有相关技术详情，按类别组织：
        - **Previous Story Insights （上一个Story见解）**: 来自上一个story的关键学习
        - **Data Models （数据模型）**: 特定模式、验证规则、关系 [带源引用]
        - **API Specifications （API规格）**: 端点详情、请求/响应格式、认证要求 [带源引用]
        - **Component Specifications （组件规格）**: UI组件详情、props、状态管理 [带源引用]
        - **File Locations （文件位置）**: 基于项目结构应该创建新代码的确切路径
        - **Testing Requirements （测试要求）**: 来自testing-strategy.md的特定测试案例或策略
        - **Technical Constraints （技术约束）**: 版本要求、性能考虑、安全规则
    - 每个技术详情必须包括其源引用：`[Source: architecture/{filename}.md#{section}]`
    - 如果在架构文档中找不到某个类别的信息，明确说明："No specific guidance found in architecture docs"
- **`Tasks / Subtasks` section**:
    - 基于以下内容生成详细、顺序的技术任务列表：Epic Requirements, Story AC, Reviewed Architecture Information
    - 每个任务必须引用相关架构文档
    - 基于测试策略将单元测试作为明确的子任务包括
    - 在适用时链接任务到AC（例如，`Task 1 (AC: 1, 3)`）
- 添加关于在步骤4中找到的项目结构对齐或差异的说明

### 6. Story Draft Completion and Review （Story草案完成和审查）

- 审查所有章节的完整性和准确性
- 验证所有源引用都包含在技术详情中
- 确保任务与epic要求和架构约束都对齐
- 将状态更新为"Draft"并保存story文件
- 执行 `{root}/tasks/execute-checklist` `{root}/checklists/story-draft-checklist`
- 向用户提供摘要，包括：
    - Story created: `{devStoryLocation}/{epicNum}.{storyNum}.story.md`
    - Status: Draft
    - Key technical components included from architecture docs
    - Any deviations or conflicts noted between epic and architecture
    - Checklist Results
    - Next steps: For Complex stories, suggest the user carefully review the story draft and also optionally have the PO run the task `{root}/tasks/validate-next-story`
