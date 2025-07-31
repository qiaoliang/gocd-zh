# Index Documentation Task （索引文档任务）

## Purpose （目的）

此任务通过扫描所有文档文件并确保它们被正确索引和描述来维护 `docs/index.md` 文件的完整性和完整性。它处理根级文档和子文件夹中的文档，按层次组织它们。

## Task Instructions （任务指令）

您现在作为文档索引器运行。您的目标是确保所有文档文件都在中央索引中正确编目，并为子文件夹提供适当的组织。

### Required Steps （必需步骤）

1. 首先，定位和扫描：
    - `docs/` 目录和所有子目录
    - 现有的 `docs/index.md` 文件（如果不存在则创建）
    - 文档结构中的所有markdown (`.md`) 和文本 (`.txt`) 文件
    - 注意用于层次组织的文件夹结构

2. 对于现有的 `docs/index.md`：
    - 解析当前条目
    - 注意现有文件引用和描述
    - 识别任何损坏的链接或缺失文件
    - 跟踪已索引的内容
    - 保留现有文件夹章节

3. 对于找到的每个文档文件：
    - 提取标题（从第一个标题或文件名）
    - 通过分析内容生成简短描述
    - 创建到文件的相对markdown链接
    - 检查是否已在索引中
    - 注意它属于哪个文件夹（如果在子文件夹中）
    - 如果缺失或过时，准备更新

4. 对于索引中找到的任何缺失或不存在的文件：
    - 呈现引用不存在文件的所有条目列表
    - 对于每个条目：
        - 显示完整条目详情（标题、路径、描述）
        - 在删除前要求明确确认
        - 如果文件被移动，提供更新路径的选项
        - 记录决定（删除/更新/保留）以供最终报告

5. 更新 `docs/index.md`：
    - 维护现有结构和组织
    - 为每个子文件夹创建2级章节 (`##`)
    - 首先列出根级文档
    - 添加带描述的缺失条目
    - 更新过时的条目
    - 仅删除已确认删除的条目
    - 确保整个格式一致

### Index Structure Format （索引结构格式）

索引应按以下方式组织：

```markdown
# Documentation Index （文档索引）

## Root Documents （根文档）

### [Document Title](./document.md)

Brief description of the document's purpose and contents （文档目的和内容的简短描述）.

### [Another Document](./another.md)

Description here （此处描述）.

## Folder Name （文件夹名称）

Documents within the `folder-name/` directory （`folder-name/` 目录中的文档）:

### [Document in Folder](./folder-name/document.md)

Description of this document （此文档的描述）.

### [Another in Folder](./folder-name/another.md)

Description here （此处描述）.

## Another Folder （另一个文件夹）

Documents within the `another-folder/` directory （`another-folder/` 目录中的文档）:

### [Nested Document](./another-folder/document.md)

Description of nested document （嵌套文档的描述）.
```

### Index Entry Format （索引条目格式）

每个条目应遵循此格式：

```markdown
### [Document Title](relative/path/to/file.md)

Brief description of the document's purpose and contents （文档目的和内容的简短描述）.
```

### Rules of Operation （操作规则）

1. 永远不要修改索引文件的内容
2. 当描述充分时，在index.md中保留现有描述
3. 维护索引中的任何现有分类或分组
4. 对所有链接使用相对路径（以 `./` 开始）
5. 确保描述简洁但信息丰富
6. 没有明确确认永远不要删除条目
7. 报告发现的任何损坏链接或不一致
8. 在考虑删除之前允许移动文件的路径更新
9. 使用2级标题 (`##`) 中的英文内容来创建文件夹章节
10. 按字母顺序排序文件夹，首先列出根文档
11. 在每个章节内，按标题字母顺序排序文档

### Process Output （过程输出）

任务将提供：

1. 对index.md所做更改的摘要
2. 新索引文件列表（按文件夹组织）
3. 更新条目列表
4. 呈现删除的条目列表及其状态：
    - 确认删除
    - 更新路径
    - 尽管文件缺失但仍保留
5. 发现的任何新文件夹
6. 发现的任何其他问题或不一致

### Handling Missing Files （处理缺失文件）

对于索引中引用但在文件系统中找不到的每个文件：

1. 呈现条目：

    ```markdown
    Missing file detected （检测到缺失文件）:
    Title: [Document Title]
    Path: relative/path/to/file.md
    Description: Existing description
    Section: [Root Documents | Folder Name]

    Options （选项）:

    1. Remove this entry （删除此条目）
    2. Update the file path （更新文件路径）
    3. Keep entry (mark as temporarily unavailable) （保留条目（标记为暂时不可用））

    Please choose an option (1/2/3) （请选择选项 (1/2/3)）:
    ```

2. 在采取任何行动之前等待用户确认
3. 记录决定以供最终报告

### Special Cases （特殊情况）

1. **Sharded Documents （分片文档）**: 如果文件夹包含 `index.md` 文件，将其视为分片文档：
    - 使用文件夹的 `index.md` 标题作为章节标题
    - 将文件夹的文档列为子章节
    - 在描述中注明这是多部分文档

2. **README files （README文件）**: 基于内容将 `README.md` 转换为更具描述性的标题

3. **Nested Subfolders （嵌套子文件夹）**: 对于深度嵌套的文件夹，维护层次结构但在主索引中限制为2级。更深的结构应该有自己的索引文件。

## Required Input （必需输入）

请提供：

1. `docs/` 目录的位置（默认：`./docs`）
2. 对 `docs/index.md` 写入访问的确认
3. 任何特定的分类偏好
4. 要从索引中排除的任何文件或目录（例如，`.git`、`node_modules`）
5. 是否包含隐藏文件/文件夹（以 `.` 开始）

您是否要继续进行文档索引？请提供上述必需输入。
