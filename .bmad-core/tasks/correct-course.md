# Correct Course Task （纠正方向任务）

## Purpose （目的）

- 使用 `{root}/checklists/change-checklist` 指导对变更触发器的结构化响应
- 在检查清单结构的指导下，分析变更对epic、项目工件和MVP的影响
- 探索潜在解决方案（例如，调整范围、回滚元素、重新范围功能），如检查清单所提示
- 基于分析，起草对任何受影响项目工件的具体、可操作的提议更新（例如，epic、用户故事、PRD章节、架构文档章节）
- 生成包含影响分析和明确起草的提议编辑的整合"Sprint Change Proposal"文档，供用户审查和批准
- 如果变更性质需要其他核心agent（如PM或Architect）进行根本性重新规划，确保清晰的移交路径

## Instructions （指令）

### 1. Initial Setup & Mode Selection （初始设置和模式选择）

- **Acknowledge Task & Inputs （确认任务和输入）**:
    - 向用户确认"Correct Course Task"（变更导航和集成）正在启动
    - 验证变更触发器并确保您有用户对问题及其感知影响的初始解释
    - 确认访问所有相关项目工件（例如，PRD、Epic/Story、架构文档、UI/UX规格）以及关键的 `{root}/checklists/change-checklist`
- **Establish Interaction Mode （建立交互模式）**:
    - 询问用户他们对此任务的偏好交互模式：
        - **"Incrementally (Default & Recommended) （增量式（默认和推荐））:** 我们是否应该逐节处理change-checklist，讨论发现并协作起草每个相关部分的提议更改，然后再进行下一步？这允许详细的、逐步的改进。"
        - **"YOLO Mode (Batch Processing) （YOLO模式（批处理））:** 或者，您是否希望我基于检查清单进行更批量的分析，然后呈现整合的发现和提议更改集以供更广泛的审查？这对于初始评估可能更快，但可能需要更广泛地审查组合的提议。"
    - 一旦用户选择，确认所选模式，然后告知用户："我们现在将使用change-checklist分析变更并起草提议更新。我将根据我们选择的交互模式指导您完成检查清单项目。"

### 2. Execute Checklist Analysis (Iteratively or Batched, per Interaction Mode) （执行检查清单分析（根据交互模式迭代或批量））

- 系统性地处理change-checklist的第1-4节（通常涵盖变更上下文、Epic/Story影响分析、工件冲突解决和路径评估/建议）
- 对于每个检查清单项目或逻辑项目组（取决于交互模式）：
    - 向用户呈现检查清单中的相关提示或考虑因素
    - 请求必要信息并主动分析相关项目工件（PRD、epic、架构文档、story历史等）以评估影响
    - 与用户讨论每个项目的发现
    - 记录每个检查清单项目的状态（例如，`[x] Addressed`、`[N/A]`、`[!] Further Action Needed`）以及任何相关说明或决定
    - 协作同意检查清单第4节所提示的"Recommended Path Forward"

### 3. Draft Proposed Changes (Iteratively or Batched) （起草提议更改（迭代或批量））

- 基于完成的检查清单分析（第1-4节）和商定的"Recommended Path Forward"（排除需要根本性重新规划的场景，这些场景需要立即移交给PM/Architect）：
    - 识别需要更新的特定项目工件（例如，特定epic、用户故事、PRD章节、架构文档组件、图表）
    - **为每个识别的工件直接和明确地起草提议更改**。示例包括：
        - 修订用户故事文本、验收标准或优先级
        - 在epic中添加、删除、重新排序或拆分用户故事
        - 提议修改的架构图表片段（例如，提供更新的Mermaid图表块或对现有图表的更改的清晰文本描述）
        - 更新PRD或架构文档中的技术列表、配置详情或特定章节
        - 如有必要，起草新的、小的支持工件（例如，特定决定的简要附录）
    - 如果在"增量模式"中，与用户讨论并改进每个工件或相关工件小组的这些提议编辑
    - 如果在"YOLO模式"中，编译所有起草的编辑以在下一步中呈现

### 4. Generate "Sprint Change Proposal" with Edits （生成带编辑的"Sprint Change Proposal"）

- 将完整的change-checklist分析（涵盖第1-4节的发现）和所有商定的提议编辑（来自指令3）综合到标题为"Sprint Change Proposal"的单个文档中。此提议应与change-checklist第5节建议的结构保持一致
- 提议必须清晰呈现：
    - **Analysis Summary （分析摘要）**: 原始问题的简明概述、其分析影响（对epic、工件、MVP范围）以及所选路径前进的理由
    - **Specific Proposed Edits （具体提议编辑）**: 对于每个受影响的工件，清晰显示或描述确切的更改（例如，"Change Story X.Y from: [old text] To: [new text]"、"Add new Acceptance Criterion to Story A.B: [new AC]"、"Update Section 3.2 of Architecture Document as follows: [new/modified text or diagram description]"）
- 向用户呈现"Sprint Change Proposal"的完整草案以供最终审查和反馈。纳入用户要求的任何最终调整

### 5. Finalize & Determine Next Steps （最终确定并确定下一步）

- 获得用户对"Sprint Change Proposal"的明确批准，包括其中记录的所有具体编辑
- 向用户提供最终确定的"Sprint Change Proposal"文档
- **基于已批准变更的性质**:
    - **如果已批准的编辑充分解决了变更并且可以直接实施或由PO/SM组织**: 说明关于分析和变更提议的"Correct Course Task"已完成，用户现在可以继续实施或记录这些更改（例如，更新实际项目文档、待办事项）。如果适当，建议移交给PO/SM agent进行待办事项组织
    - **如果分析和提议路径（根据检查清单第4节和潜在的第6节）表明变更需要更根本性的重新规划（例如，重大范围变更、主要架构返工）**: 明确说明此结论。建议用户下一步涉及参与主要PM或Architect agent，使用"Sprint Change Proposal"作为该更深层次重新规划工作的关键输入和上下文

## Output Deliverables （输出交付物）

- **Primary （主要）**: "Sprint Change Proposal"文档（markdown格式）。此文档将包含：
    - change-checklist分析摘要（问题、影响、所选路径的理由）
    - 所有受影响项目工件的具体、明确起草的提议编辑
- **Implicit （隐含）**: 带注释的change-checklist（或其完成记录），反映过程中的讨论、发现和决定
