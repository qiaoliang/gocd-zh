# Document Sharding Task （文档分片任务）

## Purpose （目的）

- 基于2级章节将大型文档分割为多个较小的文档
- 创建文件夹结构来组织分片文档
- 维护所有内容完整性，包括代码块、图表和markdown格式

## Primary Method: Automatic with markdown-tree （主要方法：使用markdown-tree自动）

[[LLM: 首先，检查 {root}/core-config.yaml 中是否设置了 markdownExploder 为 true。如果是，尝试运行命令：`md-tree explode {input file} {output path}`。

如果命令成功，通知用户文档已成功分片并停止 - 不要继续。

如果命令失败（特别是出现命令未找到或不可用的错误），通知用户："markdownExploder 设置已启用但 md-tree 命令不可用。请：

1. 全局安装 @kayvan/markdown-tree-parser：`npm install -g @kayvan/markdown-tree-parser`
2. 或在 {root}/core-config.yaml 中将 markdownExploder 设置为 false

**重要：在此停止 - 在采取上述操作之一之前不要继续手动分片。**"

如果 markdownExploder 设置为 false，通知用户："markdownExploder 设置当前为 false。为了更好的性能和可靠性，您应该：

1. 在 {root}/core-config.yaml 中将 markdownExploder 设置为 true
2. 全局安装 @kayvan/markdown-tree-parser：`npm install -g @kayvan/markdown-tree-parser`

我现在将继续手动分片过程。"

然后仅在 markdownExploder 为 false 时继续下面的手动方法。]]

### Installation and Usage （安装和使用）

1. **Install globally （全局安装）**:

    ```bash
    npm install -g @kayvan/markdown-tree-parser
    ```

2. **Use the explode command （使用explode命令）**:

    ```bash
    # For PRD
    md-tree explode docs/prd.md docs/prd

    # For Architecture
    md-tree explode docs/architecture.md docs/architecture

    # For any document
    md-tree explode [source-document] [destination-folder]
    ```

3. **What it does （它的作用）**:
    - 自动按2级章节分割文档
    - 创建正确命名的文件
    - 适当调整标题级别
    - 处理代码块和特殊markdown的所有边缘情况

如果用户已安装 @kayvan/markdown-tree-parser，使用它并跳过下面的手动过程。

---

## Manual Method (if @kayvan/markdown-tree-parser is not available or user indicated manual method) （手动方法（如果@kayvan/markdown-tree-parser不可用或用户指示手动方法））

### Task Instructions （任务指令）

1. Identify Document and Target Location （识别文档和目标位置）

- 确定要分片的文档（用户提供的路径）
- 在 `docs/` 下创建一个与文档同名的文件夹（无扩展名）
- 示例：`docs/prd.md` → 创建文件夹 `docs/prd/`

2. Parse and Extract Sections （解析和提取章节）

关键代理分片规则：

1. 读取整个文档内容
2. 识别所有2级章节（## 标题）
3. 对于每个2级章节：
    - 提取章节标题和直到下一个2级章节的所有内容
    - 包括所有子章节、代码块、图表、列表、表格等
    - 对以下内容要极其小心：
        - 围栏代码块（```）- 确保捕获完整块，包括结束反引号，并考虑可能误导的2级内容，这些内容实际上是围栏章节示例的一部分
        - Mermaid图表 - 保留完整的图表语法
        - 嵌套markdown元素
        - 可能包含代码块内##的多行内容

关键：使用理解markdown上下文的正确解析。代码块内的##不是章节标题。]]

### 3. Create Individual Files （创建单独文件）

对于每个提取的章节：

1. **Generate filename （生成文件名）**: 将章节标题转换为小写连字符格式
    - 删除特殊字符
    - 用连字符替换空格
    - 示例："## Tech Stack" → `tech-stack.md`

2. **Adjust heading levels （调整标题级别）**:
    - 2级标题在新分片文档中变为1级（# 而不是 ##）
    - 所有子章节级别减少1：

    ```txt
      - ### → ##
      - #### → ###
      - ##### → ####
      - etc.
    ```

3. **Write content （写入内容）**: 将调整后的内容保存到新文件

### 4. Create Index File （创建索引文件）

在分片文件夹中创建 `index.md` 文件，该文件：

1. 包含原始1级标题和第一个2级章节之前的任何内容
2. 列出所有分片文件的链接：

```markdown
# Original Document Title （原始文档标题）

[Original introduction content if any （原始介绍内容，如果有）]

## Sections （章节）

- [Section Name 1](./section-name-1.md)
- [Section Name 2](./section-name-2.md)
- [Section Name 3](./section-name-3.md)
  ...
```

### 5. Preserve Special Content （保留特殊内容）

1. **Code blocks （代码块）**: 必须捕获完整块，包括：

    ```language
    content
    ```

2. **Mermaid diagrams （Mermaid图表）**: 保留完整语法：

    ```mermaid
    graph TD
    ...
    ```

3. **Tables （表格）**: 维护正确的markdown表格格式

4. **Lists （列表）**: 保留缩进和嵌套

5. **Inline code （内联代码）**: 保留反引号

6. **Links and references （链接和引用）**: 保持所有markdown链接完整

7. **Template markup （模板标记）**: 如果文档包含 {{placeholders}}，精确保留

### 6. Validation （验证）

分片后：

1. 验证所有章节是否已提取
2. 检查是否有内容丢失
3. 确保标题级别已正确调整
4. 确认所有文件已成功创建

### 7. Report Results （报告结果）

提供摘要：

```text
Document sharded successfully （文档分片成功）:
- Source （源）: [original document path]
- Destination （目标）: docs/[folder-name]/
- Files created （创建的文件）: [count]
- Sections （章节）:
  - section-name-1.md: "Section Title 1"
  - section-name-2.md: "Section Title 2"
  ...
```

## Important Notes （重要说明）

- 永远不要修改实际内容，只调整标题级别
- 保留所有格式，包括重要的空白
- 处理边缘情况，如包含##符号的章节中的代码块
- 确保分片是可逆的（可以从分片重建原始文档）
