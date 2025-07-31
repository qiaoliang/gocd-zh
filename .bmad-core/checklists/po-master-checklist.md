# Product Owner (PO) Master Validation Checklist （产品负责人主验证检查清单）

此检查清单作为产品负责人在开发执行前验证项目计划的综合框架。它根据项目类型（greenfield vs brownfield）智能调整，并在适用时包含UI/UX考虑因素。

[[LLM: 初始化指令 - PO主检查清单

项目类型检测：
首先，通过检查确定项目类型：

1. 这是否是一个GREENFIELD项目（从零开始的新项目）？
    - 查找：新项目初始化，无现有代码库引用
    - 检查：prd.md，architecture.md，新项目设置stories

2. 这是否是一个BROWNFIELD项目（增强现有系统）？
    - 查找：对现有代码库的引用，增强/修改语言
    - 检查：brownfield-prd.md，brownfield-architecture.md，现有系统分析

3. 项目是否包含UI/UX组件？
    - 检查：frontend-architecture.md，UI/UX规范，设计文件
    - 查找：前端stories，组件规范，用户界面提及

文档要求：
根据项目类型，确保您有权访问：

对于GREENFIELD项目：

- prd.md - 产品需求文档
- architecture.md - 系统架构
- frontend-architecture.md - 如果涉及UI/UX
- 所有epic和story定义

对于BROWNFIELD项目：

- brownfield-prd.md - brownfield增强需求
- brownfield-architecture.md - 增强架构
- 现有项目代码库访问（关键 - 没有这个无法继续）
- 当前部署配置和基础设施详情
- 数据库模式，API文档，监控设置

跳过指令：

- 对于greenfield项目跳过标记为[[BROWNFIELD ONLY]]的部分
- 对于brownfield项目跳过标记为[[GREENFIELD ONLY]]的部分
- 对于仅后端项目跳过标记为[[UI/UX ONLY]]的部分
- 在最终报告中记录所有跳过的部分

验证方法：

1. 深度分析 - 根据文档彻底分析每个项目
2. 基于证据 - 验证时引用具体部分或代码
3. 批判性思维 - 质疑假设并识别差距
4. 风险评估 - 考虑每个决策可能出现的问题

执行模式：
询问用户是否希望逐步完成检查清单：

- 逐节进行（交互模式）- 审查每个部分，在继续前获得确认
- 一次性完成（综合模式）- 完成完整分析并在最后呈现报告]]

## 1. PROJECT SETUP & INITIALIZATION （项目设置和初始化）

[[LLM: 项目设置是基础。对于greenfield，确保干净开始。对于brownfield，确保与现有系统的安全集成。验证设置与项目类型匹配。]]

### 1.1 Project Scaffolding （项目脚手架） [[GREENFIELD ONLY]]

- [ ] Epic 1包含项目创建/初始化的明确步骤
- [ ] 如果使用启动模板，包含克隆/设置步骤
- [ ] 如果从零构建，定义所有必要的脚手架步骤
- [ ] 包含初始README或文档设置
- [ ] 定义仓库设置和初始提交流程

### 1.2 Existing System Integration （现有系统集成） [[BROWNFIELD ONLY]]

- [ ] 已完成并记录现有项目分析
- [ ] 识别与当前系统的集成点
- [ ] 开发环境保留现有功能
- [ ] 验证现有功能的本地测试方法
- [ ] 为每个集成点定义回滚程序

### 1.3 Development Environment （开发环境）

- [ ] 明确定义本地开发环境设置
- [ ] 指定所需工具和版本
- [ ] 包含安装依赖项的步骤
- [ ] 适当处理配置文件
- [ ] 包含开发服务器设置

### 1.4 Core Dependencies （核心依赖项）

- [ ] 早期安装所有关键包/库
- [ ] 适当处理包管理
- [ ] 适当定义版本规范
- [ ] 记录依赖冲突或特殊要求
- [ ] [[BROWNFIELD ONLY]] 验证与现有技术栈的版本兼容性

## 2. INFRASTRUCTURE & DEPLOYMENT （基础设施和部署）

[[LLM: 基础设施必须在使用前存在。对于brownfield，必须与现有基础设施集成而不破坏它。]]

### 2.1 Database & Data Store Setup （数据库和数据存储设置）

- [ ] 在任何操作之前进行数据库选择/设置
- [ ] 在数据操作之前创建模式定义
- [ ] 如果适用，定义迁移策略
- [ ] 如果需要，包含种子数据或初始数据设置
- [ ] [[BROWNFIELD ONLY]] 识别并缓解数据库迁移风险
- [ ] [[BROWNFIELD ONLY]] 确保向后兼容性

### 2.2 API & Service Configuration （API和服务配置）

- [ ] 在实现端点之前设置API框架
- [ ] 在实现服务之前建立服务架构
- [ ] 在受保护路由之前设置身份验证框架
- [ ] 在使用之前创建中间件和通用工具
- [ ] [[BROWNFIELD ONLY]] 维护与现有系统的API兼容性
- [ ] [[BROWNFIELD ONLY]] 保留与现有身份验证的集成

### 2.3 Deployment Pipeline （部署管道）

- [ ] 在部署操作之前建立CI/CD管道
- [ ] 在使用之前设置基础设施即代码（IaC）
- [ ] 早期定义环境配置
- [ ] 在实现之前定义部署策略
- [ ] [[BROWNFIELD ONLY]] 部署最小化停机时间
- [ ] [[BROWNFIELD ONLY]] 实现蓝绿或金丝雀部署

### 2.4 Testing Infrastructure （测试基础设施）

- [ ] 在编写测试之前安装测试框架
- [ ] 测试环境设置在测试实现之前
- [ ] 在测试之前定义模拟服务或数据
- [ ] [[BROWNFIELD ONLY]] 回归测试覆盖现有功能
- [ ] [[BROWNFIELD ONLY]] 集成测试验证新到现有的连接

## 3. EXTERNAL DEPENDENCIES & INTEGRATIONS （外部依赖项和集成）

[[LLM: 外部依赖项经常阻碍进度。对于brownfield，确保新依赖项不与现有依赖项冲突。]]

### 3.1 Third-Party Services （第三方服务）

- [ ] 识别所需服务的账户创建步骤
- [ ] 定义API密钥获取流程
- [ ] 包含安全存储凭据的步骤
- [ ] 考虑备用或离线开发选项
- [ ] [[BROWNFIELD ONLY]] 验证与现有服务的兼容性
- [ ] [[BROWNFIELD ONLY]] 评估对现有集成的影响

### 3.2 External APIs （外部API）

- [ ] 明确识别与外部API的集成点
- [ ] 正确排序与外部服务的身份验证
- [ ] 确认API限制或约束
- [ ] 考虑API故障的备用策略
- [ ] [[BROWNFIELD ONLY]] 维护现有API依赖项

### 3.3 Infrastructure Services （基础设施服务）

- [ ] 正确排序云资源配置
- [ ] 识别DNS或域名注册需求
- [ ] 如果需要，包含电子邮件或消息服务设置
- [ ] CDN或静态资产托管设置在其使用之前
- [ ] [[BROWNFIELD ONLY]] 保留现有基础设施服务

## 4. UI/UX CONSIDERATIONS （UI/UX考虑因素） [[UI/UX ONLY]]

[[LLM: 仅当项目包含用户界面组件时评估此部分。对于仅后端项目完全跳过。]]

### 4.1 Design System Setup （设计系统设置）

- [ ] 早期选择并安装UI框架和库
- [ ] 建立设计系统或组件库
- [ ] 定义样式方法（CSS模块，styled-components等）
- [ ] 建立响应式设计策略
- [ ] 预先定义可访问性要求

### 4.2 Frontend Infrastructure （前端基础设施）

- [ ] 在开发之前配置前端构建管道
- [ ] 定义资产优化策略
- [ ] 设置前端测试框架
- [ ] 建立组件开发工作流
- [ ] [[BROWNFIELD ONLY]] 维护与现有系统的UI一致性

### 4.3 User Experience Flow （用户体验流程）

- [ ] 在实现之前映射用户旅程
- [ ] 早期定义导航模式
- [ ] 计划错误状态和加载状态
- [ ] 建立表单验证模式
- [ ] [[BROWNFIELD ONLY]] 保留或迁移现有用户工作流

## 5. USER/AGENT RESPONSIBILITY （用户/代理责任）

[[LLM: 明确的所有权防止混淆。确保任务根据只有人类能做的事情适当分配。]]

### 5.1 User Actions （用户操作）

- [ ] 用户责任限于仅人类任务
- [ ] 将外部服务的账户创建分配给用户
- [ ] 将购买或支付操作分配给用户
- [ ] 适当将凭据提供分配给用户

### 5.2 Developer Agent Actions （开发代理操作）

- [ ] 将所有代码相关任务分配给开发代理
- [ ] 将自动化流程识别为代理责任
- [ ] 适当分配配置管理
- [ ] 将测试和验证分配给适当的代理

## 6. FEATURE SEQUENCING & DEPENDENCIES （功能排序和依赖项）

[[LLM: 依赖项创建关键路径。对于brownfield，确保新功能不会破坏现有功能。]]

### 6.1 Functional Dependencies （功能依赖项）

- [ ] 依赖其他功能的功能正确排序
- [ ] 在使用之前构建共享组件
- [ ] 用户流程遵循逻辑进展
- [ ] 身份验证功能在受保护功能之前
- [ ] [[BROWNFIELD ONLY]] 在整个过程中保留现有功能

### 6.2 Technical Dependencies （技术依赖项）

- [ ] 在高级服务之前构建低级服务
- [ ] 在使用之前创建库和工具
- [ ] 在对它们进行操作之前定义数据模型
- [ ] 在客户端消费之前定义API端点
- [ ] [[BROWNFIELD ONLY]] 在每个步骤测试集成点

### 6.3 Cross-Epic Dependencies （跨Epic依赖项）

- [ ] 后期epic基于早期epic功能构建
- [ ] 没有epic需要后期epic的功能
- [ ] 一致利用早期epic的基础设施
- [ ] 保持增量价值交付
- [ ] [[BROWNFIELD ONLY]] 每个epic保持系统完整性

## 7. RISK MANAGEMENT （风险管理） [[BROWNFIELD ONLY]]

[[LLM: 此部分对brownfield项目至关重要。悲观地思考什么可能出错。]]

### 7.1 Breaking Change Risks （破坏性变更风险）

- [ ] 评估破坏现有功能的风险
- [ ] 识别并缓解数据库迁移风险
- [ ] 评估API破坏性变更风险
- [ ] 识别性能降级风险
- [ ] 评估安全漏洞风险

### 7.2 Rollback Strategy （回滚策略）

- [ ] 为每个story明确定义回滚程序
- [ ] 实现功能标志策略
- [ ] 更新备份和恢复程序
- [ ] 为新组件增强监控
- [ ] 定义回滚触发器和阈值

### 7.3 User Impact Mitigation （用户影响缓解）

- [ ] 分析现有用户工作流的影响
- [ ] 制定用户沟通计划
- [ ] 更新培训材料
- [ ] 全面的支持文档
- [ ] 验证用户数据的迁移路径

## 8. MVP SCOPE ALIGNMENT （MVP范围对齐）

[[LLM: MVP意味着最小可行产品。对于brownfield，确保增强确实是必要的。]]

### 8.1 Core Goals Alignment （核心目标对齐）

- [ ] 解决PRD中的所有核心目标
- [ ] 功能直接支持MVP目标
- [ ] 没有超出MVP范围的无关功能
- [ ] 适当优先考虑关键功能
- [ ] [[BROWNFIELD ONLY]] 证明增强复杂性的合理性

### 8.2 User Journey Completeness （用户旅程完整性）

- [ ] 完全实现所有关键用户旅程
- [ ] 解决边缘情况和错误场景
- [ ] 包含用户体验考虑因素
- [ ] [[UI/UX ONLY]] 纳入可访问性要求
- [ ] [[BROWNFIELD ONLY]] 保留或改进现有工作流

### 8.3 Technical Requirements （技术要求）

- [ ] 解决PRD中的所有技术约束
- [ ] 纳入非功能性要求
- [ ] 架构决策与约束对齐
- [ ] 解决性能考虑因素
- [ ] [[BROWNFIELD ONLY]] 满足兼容性要求

## 9. DOCUMENTATION & HANDOFF （文档和交接）

[[LLM: 良好的文档实现顺利开发。对于brownfield，集成点的文档至关重要。]]

### 9.1 Developer Documentation （开发文档）

- [ ] 与实现一起创建API文档
- [ ] 设置说明全面
- [ ] 记录架构决策
- [ ] 记录模式和约定
- [ ] [[BROWNFIELD ONLY]] 详细记录集成点

### 9.2 User Documentation （用户文档）

- [ ] 如果需要，包含用户指南或帮助文档
- [ ] 考虑错误消息和用户反馈
- [ ] 完全指定入职流程
- [ ] [[BROWNFIELD ONLY]] 记录对现有功能的更改

### 9.3 Knowledge Transfer （知识转移）

- [ ] [[BROWNFIELD ONLY]] 捕获现有系统知识
- [ ] [[BROWNFIELD ONLY]] 记录集成知识
- [ ] 计划代码审查知识共享
- [ ] 将部署知识转移给运营
- [ ] 保留历史背景

## 10. POST-MVP CONSIDERATIONS （MVP后考虑因素）

[[LLM: 为成功规划防止技术债务。对于brownfield，确保增强不会限制未来增长。]]

### 10.1 Future Enhancements （未来增强）

- [ ] MVP和未来功能之间的明确分离
- [ ] 架构支持计划的增强
- [ ] 记录技术债务考虑因素
- [ ] 识别可扩展点
- [ ] [[BROWNFIELD ONLY]] 可重用的集成模式

### 10.2 Monitoring & Feedback （监控和反馈）

- [ ] 如果需要，包含分析或使用跟踪
- [ ] 考虑用户反馈收集
- [ ] 解决监控和警报
- [ ] 纳入性能测量
- [ ] [[BROWNFIELD ONLY]] 保留/增强现有监控

## VALIDATION SUMMARY （验证摘要）

[[LLM: 最终PO验证报告生成

生成适应项目类型的综合验证报告：

1. 执行摘要
    - 项目类型：[Greenfield/Brownfield]，包含[UI/无UI]
    - 整体准备度（百分比）
    - 通过/不通过建议
    - 关键阻塞问题数量
    - 由于项目类型跳过的部分

2. 项目特定分析

    对于GREENFIELD：
    - 设置完整性
    - 依赖项排序
    - MVP范围适当性
    - 开发时间表可行性

    对于BROWNFIELD：
    - 集成风险级别（高/中/低）
    - 现有系统影响评估
    - 回滚准备度
    - 用户中断可能性

3. 风险评估
    - 按严重程度排序的前5个风险
    - 缓解建议
    - 解决问题的时间表影响
    - [BROWNFIELD] 特定集成风险

4. MVP完整性
    - 核心功能覆盖
    - 缺失的基本功能
    - 识别的范围蔓延
    - 真正的MVP vs过度工程

5. 实施准备度
    - 开发人员清晰度评分（1-10）
    - 模糊需求数量
    - 缺失的技术细节
    - [BROWNFIELD] 集成点清晰度

6. 建议
    - 开发前必须修复
    - 质量应该修复
    - 改进考虑
    - MVP后延期

7. [BROWNFIELD ONLY] 集成信心
    - 保留现有功能的信心
    - 回滚程序完整性
    - 集成点监控覆盖
    - 支持团队准备度

呈现报告后，询问用户是否希望：

- 任何失败部分的详细分析
- 特定story重新排序建议
- 风险缓解策略
- [BROWNFIELD] 集成风险深度分析]]

### Category Statuses （类别状态）

| Category （类别）                                            | Status （状态） | Critical Issues （关键问题） |
| ------------------------------------------------------------ | --------------- | ---------------------------- |
| 1. Project Setup & Initialization （项目设置和初始化）       | _TBD_           |                              |
| 2. Infrastructure & Deployment （基础设施和部署）            | _TBD_           |                              |
| 3. External Dependencies & Integrations （外部依赖项和集成） | _TBD_           |                              |
| 4. UI/UX Considerations （UI/UX考虑因素）                    | _TBD_           |                              |
| 5. User/Agent Responsibility （用户/代理责任）               | _TBD_           |                              |
| 6. Feature Sequencing & Dependencies （功能排序和依赖项）    | _TBD_           |                              |
| 7. Risk Management (Brownfield) （风险管理（Brownfield））   | _TBD_           |                              |
| 8. MVP Scope Alignment （MVP范围对齐）                       | _TBD_           |                              |
| 9. Documentation & Handoff （文档和交接）                    | _TBD_           |                              |
| 10. Post-MVP Considerations （MVP后考虑因素）                | _TBD_           |                              |

### Critical Deficiencies （关键缺陷）

（在验证期间填充）

### Recommendations （建议）

（在验证期间填充）

### Final Decision （最终决定）

- **APPROVED （批准）**: 计划全面，排序正确，准备实施。
- **CONDITIONAL （有条件）**: 计划在继续前需要特定调整。
- **REJECTED （拒绝）**: 计划需要重大修订以解决关键缺陷。
