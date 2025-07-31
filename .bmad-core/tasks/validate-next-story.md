# Validate Next Story Task （验证下一个Story任务）

## Purpose （目的）

在实施开始前全面验证story草稿，确保其完整、准确，并为成功开发提供足够的上下文。此任务识别需要解决的问题和差距，防止幻觉并确保实施就绪。

## SEQUENTIAL Task Execution (Do not proceed until current Task is complete) （顺序任务执行（在当前任务完成之前不要继续））

### 0. Load Core Configuration and Inputs （加载核心配置和输入）

- 加载 `.bmad-core/core-config.yaml`
- 如果文件不存在，停止并通知用户："core-config.yaml not found. This file is required for story validation."
- 提取关键配置：`devStoryLocation`, `prd.*`, `architecture.*`
- 识别并加载以下输入：
    - **Story文件**: 要验证的草稿story（由用户提供或在 `devStoryLocation` 中发现）
    - **父epic**: 包含此story要求的epic
    - **架构文档**: 基于配置（分片或整体）
    - **Story模板**: `bmad-core/templates/story-tmpl.md` 用于完整性验证

### 1. Template Completeness Validation （模板完整性验证）

- 加载 `bmad-core/templates/story-tmpl.md` 并从模板中提取所有章节标题
- **缺失章节检查**: 将story章节与模板章节进行比较，验证所有必需章节都存在
- **占位符验证**: 确保没有模板占位符仍未填写（例如，`{{EpicNum}}`, `{{role}}`, `_TBD_`）
- **代理章节验证**: 确认模板中的所有章节都存在供未来代理使用
- **结构合规**: 验证story遵循模板结构和格式

### 2. File Structure and Source Tree Validation （文件结构和源树验证）

- **文件路径清晰度**: 要创建/修改的新/现有文件是否明确指定？
- **源树相关性**: 相关项目结构是否包含在开发说明中？
- **目录结构**: 新目录/组件是否根据项目结构正确定位？
- **文件创建顺序**: 任务是否指定文件应该按逻辑顺序创建的位置？
- **路径准确性**: 文件路径是否与架构文档中的项目结构一致？

### 3. UI/Frontend Completeness Validation (if applicable) （UI/前端完整性验证（如果适用））

- **组件规格**: UI组件是否足够详细以供实施？
- **样式/设计指导**: 视觉实施指导是否清晰？
- **用户交互流程**: 是否指定了UX模式和行为？
- **响应式/可访问性**: 如果需要，是否解决了这些考虑？
- **集成点**: 前端-后端集成点是否清晰？

### 4. Acceptance Criteria Satisfaction Assessment （验收标准满足评估）

- **AC覆盖**: 列出的任务是否满足所有验收标准？
- **AC可测试性**: 验收标准是否可测量和可验证？
- **缺失场景**: 是否涵盖边缘情况或错误条件？
- **成功定义**: 每个AC的"完成"是否明确定义？
- **任务-AC映射**: 任务是否正确链接到特定验收标准？

### 5. Validation and Testing Instructions Review （验证和测试指令审查）

- **测试方法清晰度**: 测试方法是否明确指定？
- **测试场景**: 是否识别了关键测试用例？
- **验证步骤**: 验收标准验证步骤是否清晰？
- **测试工具/框架**: 是否指定了所需的测试工具？
- **测试数据要求**: 是否识别了测试数据需求？

### 6. Security Considerations Assessment (if applicable) （安全考虑评估（如果适用））

- **安全要求**: 是否识别并解决了安全需求？
- **认证/授权**: 是否指定了访问控制？
- **数据保护**: 敏感数据处理要求是否清晰？
- **漏洞预防**: 是否解决了常见安全问题？
- **合规要求**: 是否解决了监管/合规需求？

### 7. Tasks/Subtasks Sequence Validation （任务/子任务序列验证）

- **逻辑顺序**: 任务是否遵循正确的实施顺序？
- **依赖关系**: 任务依赖关系是否清晰正确？
- **粒度**: 任务是否适当大小且可操作？
- **完整性**: 任务是否涵盖所有要求和验收标准？
- **阻塞问题**: 是否有任何任务会阻塞其他任务？

### 8. Anti-Hallucination Verification （反幻觉验证）

- **源验证**: 每个技术声明必须可追溯到源文档
- **架构对齐**: 开发说明内容与架构规格匹配
- **无发明细节**: 标记任何不受源文档支持的技术决策
- **引用准确性**: 验证所有源引用是否正确且可访问
- **事实检查**: 根据epic和架构文档交叉引用声明

### 9. Dev Agent Implementation Readiness （开发代理实施就绪）

- **自包含上下文**: 是否可以在不阅读外部文档的情况下实施story？
- **清晰指令**: 实施步骤是否明确？
- **完整技术上下文**: 开发说明中是否包含所有必需的技术细节？
- **缺失信息**: 识别任何关键信息差距
- **可操作性**: 所有任务是否可由开发代理操作？

### 10. Generate Validation Report （生成验证报告）

提供结构化验证报告，包括：

#### Template Compliance Issues （模板合规问题）

- 来自story模板的缺失章节
- 未填写的占位符或模板变量
- 结构格式问题

#### Critical Issues (Must Fix - Story Blocked) （关键问题（必须修复 - Story被阻塞））

- 实施缺少基本信息
- 不准确或不可验证的技术声明
- 验收标准覆盖不完整
- 缺少必需章节

#### Should-Fix Issues (Important Quality Improvements) （应该修复的问题（重要质量改进））

- 不清晰的实施指导
- 缺少安全考虑
- 任务排序问题
- 不完整的测试指令

#### Nice-to-Have Improvements (Optional Enhancements) （锦上添花的改进（可选增强））

- 有助于实施的额外上下文
- 提高效率的澄清
- 文档改进

#### Anti-Hallucination Findings （反幻觉发现）

- 不可验证的技术声明
- 缺少源引用
- 与架构文档不一致
- 发明的库、模式或标准

#### Final Assessment （最终评估）

- **GO**: Story已准备好实施
- **NO-GO**: Story在实施前需要修复
- **Implementation Readiness Score （实施就绪评分）**: 1-10分制
- **Confidence Level （置信度）**: 成功实施的高/中/低
