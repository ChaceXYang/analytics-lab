# analytics-lab

Portfolio projects and hands-on practice on my path to becoming a data analyst.
数据分析求职作品集与练习仓库。

## Portfolio Projects 项目集

Real data · SQL + Python · no machine learning · conclusions that point to business actions.
真实数据 · SQL + Python 双栈 · 不使用机器学习 · 结论指向业务动作。

| Project 项目 | Business Question 业务问题 | Stack | Status |
|---|---|---|---|
| [H&M Customer Retention & RFM](projects/hm-customer-retention-rfm/) | 复购 vs 拉新？同期群留存与 RFM 分层 | SQL · Python | ✅ 已完成（2026-08-19）|
| [Freddie Mac Mortgage Vintage Risk](projects/freddie-mac-mortgage-vintage-risk/) | 哪些放款 vintage 违约率最高？审批规则红线画在哪？ | SQL · Python | ⏸ 待启动（数据已备）|

## Learning Records 学习记录

| Folder | Content |
|---|---|
| `py4da/` | Code-along notebooks for *Python for Data Analysis* (Wes McKinney, 3rd ed.) |
| `py4da/examples/` | Sample datasets used by the notebooks |
| `python/` | General Python practice: FreeCodeCamp course notebook, NumPy, pandas demo |

## Progress

- [x] Python basics (FreeCodeCamp course)
- [x] NumPy fundamentals
- [x] pandas: data loading, cleaning, groupby aggregation
- [x] SQL: multi-table joins, subqueries, window functions
- [x] **P0: H&M retention & RFM** — 分块读取(3.7GB) → 清洗入库 → RFM 分层 → 同期群留存 → 复购结构 → 品类帕累托 → 沉睡客群 → 3 张可视化 → GitHub 发布。核心结论：复购客户 64% 人贡献 94% 收入；首月留存断崖至 44%；前 3 类服装品类贡献 79% 收入

## Conventions

- Notebooks are named by chapter, e.g. `Practicing_Ch3.ipynb`
- Commit messages follow `chXX: topic` for learning records, `project: step` for portfolio work
- Raw datasets are never committed; each project has a `data/README.md` explaining how to obtain them

---
*Study notes, plans & weekly reviews live in a private Obsidian vault.*
