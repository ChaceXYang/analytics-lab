# 项目长期记忆（MEMORY.md）

## 协作工作方式（2026-08-15 用户明确约定，最高优先级）

用户杨淳栯要求后续 H&M 项目（及后续项目）按以下模式执行，**替代之前"我给代码他跑"的模式**：

1. 先把项目拆解成清晰的小步骤/里程碑，列出来让用户确认。
2. 每次只指导一个步骤：告诉用户「这一步实现什么功能」+「涉及哪些知识点/API（只给名称/文档线索，不给完整代码）」。
3. 用户先自己写代码，写完贴回来。
4. 我审查：指出问题，用提问/提示引导修改，**不直接帮他改好**。
5. 只有用户明确说"请给我代码示例"或"帮我写出这段代码"时，才给代码。
6. 用户卡住时，按顺序：① 引导性问题 → ② 思路提示 → ③ 伪代码 → ④ 最小代码片段。

背景：源于用户对"AI 代写 = 作弊"的顾虑，他主动选择"自己写 + 我引导"来获得真本事。

## 项目环境事实

- git 仓库根：`E:/analytics-lab`（projects 是其子目录）。
- `.gitignore` 已含 `*.csv` 和 `projects/*/data/`，原始数据放 data/ 不会进版本库。
- H&M 数据已在 `hm-customer-retention-rfm/data/`：transactions_train.csv(3.49GB) / customers.csv(207MB) / articles.csv(36MB)。
- 项目文档：`C:/Users/34327/Desktop/KnowledgeVault/20-job/项目/`（项目选择.md + 数据分析项目实战手册_v2.1.md，第 7 章为 H&M 完整流程）。

## 书位置偏好（2026-08-17 起）

- 用户按《利用Python进行数据分析》（Wes McKinney，第3版）学 pandas，手头有纸质书。
- 用户要求：讲 API 线索时标注"书里第几章/第几节"，避免他误以为"学了忘完了"。
- **规则补充（2026-08-17）**：书上有的 API → 标书位置让他自己翻；**书上没有的 API → 我直接教用法（给最小示例）**，不再让他查官方文档。
- **重要事实**：该书第3版全书**没有 `usecols` 参数**（grep 零匹配）；`chunksize` 在第6章 6.1「逐块读取文本文件」小节有专门讲解。书里没有的 API 要明确说"查官方文档"，不要让他自我怀疑。
- 书位置速查（第3版）：
  - 第5章 pandas 入门：5.2 常用功能（apply）/ 5.3 描述性统计（value_counts、unique）
  - 第6章 数据载入：read_csv 基础 / 表6-2 参数（nrows、parse_dates、chunksize）/ 6.1「逐块读取」/ 6.4 数据库交互（sqlite）
  - 第7章 数据清洗：7.1 缺失值 / 7.2 数据变换（含「离散化与分箱」pd.cut、「删除重复」duplicated/drop_duplicates）
  - 第8章 数据规整：8.2 合并（pd.concat）/ 8.3 重塑与透视（pivot_table）
  - 第9章 绘图：9.2 pandas 与 seaborn
  - 第10章 数据聚合与分组：groupby().agg() / as_index=False / reset_index（把分组键变回列，18272 行附近）
  - 第11章 时间序列：to_period
- **命名聚合** `agg(新列名=(原列, 函数))`：书里**没有**（pandas 0.25+ 新语法），直接教。这是避免 agg 字典产生 MultiIndex 列名的现代写法，手册 Step 0-1 用的就是它。
- 书的 md 全文在 `C:/Users/34327/Desktop/KnowledgeVault/40-reading/library/Python for Data Analysis ... (Wes McKinney).md`。

## SQL 教材（2026-08-18 发现）

- 用户有《SQL必知必会（第5版）（中文版）》md：`C:/Users/34327/Desktop/KnowledgeVault/40-reading/library/SQL/SQL必知必会（第5版）（中文版).md`
- 该书用 **ANSI 标准 `INNER JOIN` 显式写法**（非省略写法）。用户学的是 INNER JOIN。我引导时写 `JOIN`（省略 INNER）曾让他没反应过来——`JOIN` = `INNER JOIN` 同义，后续 SQL 引导可统一用 `JOIN ... ON ...`，但要说明等价。
