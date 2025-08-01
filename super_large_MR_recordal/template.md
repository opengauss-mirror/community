## 超大MR合入例外备案申请
### 一、MR基本信息：
| MR标题  | XXXX |
|---|---|
| MR链接  | XXXX |
| MR类型  | 新需求/Bug fix/子需求 |
| 涉及需求  | XXXX |
| MR行数  | 新增：xx行，删除：xx行 |
| 申请人  | XXXX |

### 二、申请例外自检：
| 序号  | 自检项 | 结果 |
|---|---|---|
| 1  | 是否尝试过抽取公用逻辑 | 是/否 |
| 2  | 是否尝试拆分成多个独立的子需求 | 是/否 |
| 3  | 是否包含多个功能，且单个功能代码实现超过500行 | 是/否 |
| 4  | 是否同时包含新需求实现和历史的重构优化 | 是/否 |
| 5  | 是否涉及删除了超过1000行的整个文件 | 是/否 |
| 6  | 是否是由自动重构工具生成的MR | 是/否 |
| 7  | 是否属于整块特性的代码回合 | 是/否 |
| 8  | 是否属于由底层平台/组件变更导致 | 是/否 |

### 三、申请例外原因：

原因举例：
比如当前需求是一个完整的功能，其中包含各个子模块之间的代码存在依赖关系/
该需求属于特性的整体回合/该需求经过了充分的自验证，前期经过committer检视发现了xx个问题（证明检视的充分性），增量覆盖率xx% / 做过哪些拆分优化的尝试等

### 四、SUB CMC审视结论：

| 会议时间  | 2025年7月7日 |
|---|---|
| 参与committer  |  |
| 会议结论  | 通过/不通过 |
| 备注  |  |
