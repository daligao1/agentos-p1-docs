# AgentOS P1 方案文档（公开）

一句话任务 → LLM 规划 → 只读库 → 自动报告 → 人工审批 → 多通道投递（失败自动回退）。

- 方案落地页：GitHub Pages
- 代码：私有仓库（`agentos-p1`）
- 开源依赖：LangGraph / pytest / ruff / actions-checkout / actions-setup-python（均为 MIT 或等价宽松许可）

## 关键设计

1. **规划与执行分离**：LLM 只出步骤，工具层按白名单执行。
2. **只读是硬约束**：`mode=ro` + `query_only` + 固定 SQL 参数化，无写库工具。
3. **审批门不可绕过**：发送类工具强制 `risk=high`，`interrupt()` 停下等人。
4. **投递可回退**：Telegram → 本地 IM → 收件箱，失败落 local 并审计。
