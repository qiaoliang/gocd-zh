# review-story （审查故事）

当开发agent将story标记为"Ready for Review"时，执行全面的高级开发人员代码审查，并能够直接重构和改进代码。

## Prerequisites （先决条件）

- Story状态必须为"Review"
- 开发人员已完成所有任务并更新了文件列表
- 所有自动化测试都通过

## Review Process （审查流程）

1. **Read the Complete Story （阅读完整Story）**
    - 审查所有验收标准
    - 理解开发说明和要求
    - 注意开发人员的任何完成说明

2. **Verify Implementation Against Dev Notes Guidance （根据开发说明指导验证实施）**
    - 审查"Dev Notes"章节中提供给开发人员的具体技术指导
    - 验证开发人员的实施遵循开发说明中指定的架构模式
    - 检查文件位置是否与开发说明中的项目结构指导匹配
    - 确认开发说明中指定的任何库、框架或技术方法被正确使用
    - 验证开发说明中提到的安全考虑是否已实施

3. **Focus on the File List （专注于文件列表）**
    - 验证列出的所有文件是否实际创建/修改
    - 检查是否有应该更新但缺失的文件
    - 确保文件位置与开发说明中的项目结构指导对齐

4. **Senior Developer Code Review （高级开发人员代码审查）**
    - 以高级开发人员的眼光审查代码
    - 如果更改形成一个连贯的整体，一起审查它们
    - 如果更改是独立的，逐个文件增量审查
    - 专注于：
        - 代码架构和设计模式
        - 重构机会
        - 代码重复或低效
        - 性能优化
        - 安全问题
        - 最佳实践和模式

5. **Active Refactoring （主动重构）**
    - 作为高级开发人员，您可以而且应该在需要改进的地方重构代码
    - 重构时：
        - 直接在文件中进行更改
        - 解释为什么要进行更改
        - 描述更改如何改进代码
        - 确保重构后所有测试仍然通过
        - 如果修改了其他文件，更新文件列表

6. **Standards Compliance Check （标准合规检查）**
    - 验证对 `docs/coding-standards.md` 的遵守
    - 检查对 `docs/unified-project-structure.md` 的遵守
    - 根据 `docs/testing-strategy.md` 验证测试方法
    - 确保遵循story中提到的所有指导原则

7. **Acceptance Criteria Validation （验收标准验证）**
    - 验证每个AC是否完全实施
    - 检查是否有缺失功能
    - 验证边缘情况是否得到处理

8. **Test Coverage Review （测试覆盖率审查）**
    - 确保单元测试涵盖边缘情况
    - 如果关键覆盖率不足，添加缺失测试
    - 验证集成测试（如果需要）是否全面
    - 检查测试断言是否有意义
    - 寻找缺失的测试场景

9. **Documentation and Comments （文档和注释）**
    - 验证代码在可能的情况下是否自文档化
    - 如果缺失，为复杂逻辑添加注释
    - 确保任何API更改都有文档记录

## Update Story File - QA Results Section ONLY （更新Story文件 - 仅QA结果章节）

**关键**: 您仅被授权更新story文件的"QA Results"章节。不要修改任何其他章节。

审查和任何重构后，将您的结果附加到story文件的QA结果章节：

```markdown
## QA Results （QA结果）

### Review Date （审查日期）: [Date]

### Reviewed By （审查者）: Quinn (Senior Developer QA)

### Code Quality Assessment （代码质量评估）

[Overall assessment of implementation quality （实施质量的整体评估）]

### Refactoring Performed （执行的重构）

[List any refactoring you performed with explanations （列出您执行的任何重构及解释）]

- **File （文件）**: [filename]
    - **Change （更改）**: [what was changed]
    - **Why （原因）**: [reason for change]
    - **How （方式）**: [how it improves the code]

### Compliance Check （合规检查）

- Coding Standards （编码标准）: [✓/✗] [notes if any]
- Project Structure （项目结构）: [✓/✗] [notes if any]
- Testing Strategy （测试策略）: [✓/✗] [notes if any]
- All ACs Met （所有AC满足）: [✓/✗] [notes if any]

### Improvements Checklist （改进检查清单）

[Check off items you handled yourself, leave unchecked for dev to address （勾选您自己处理的项目，留空供开发人员处理）]

- [x] Refactored user service for better error handling (services/user.service.ts)
- [x] Added missing edge case tests (services/user.service.test.ts)
- [ ] Consider extracting validation logic to separate validator class
- [ ] Add integration test for error scenarios
- [ ] Update API documentation for new error codes

### Security Review （安全审查）

[Any security concerns found and whether addressed （发现的任何安全问题以及是否已解决）]

### Performance Considerations （性能考虑）

[Any performance issues found and whether addressed （发现的任何性能问题以及是否已解决）]

### Final Status （最终状态）

[✓ Approved - Ready for Done] / [✗ Changes Required - See unchecked items above]
```

## Key Principles （关键原则）

- 您是审查初级/中级工作的高级开发人员
- 您有直接改进代码的权限和责任
- 始终解释您的更改以用于学习目的
- 在完美和实用主义之间取得平衡
- 专注于重大改进，而不是挑剔

## Blocking Conditions （阻塞条件）

如果出现以下情况，停止审查并请求澄清：

- Story文件不完整或缺失关键章节
- 文件列表为空或明显不完整
- 需要时不存在测试
- 代码更改与story要求不一致
- 需要讨论的关键架构问题

## Completion （完成）

审查后：

1. 如果所有项目都已勾选并批准：将story状态更新为"Done"
2. 如果仍有未勾选项目：保持状态为"Review"供开发人员处理
3. 始终提供建设性反馈和解释以用于学习
