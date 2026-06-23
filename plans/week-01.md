# Week 01 · 2026-06-23 ~ 2026-06-29 · 起点

> **本周目标**：从"看了一堆项目"切到"动起来"。结束时 GitHub 必须有 commit。
>
> ⚠️ **真正的红线是 8-31**（投递截止），本周红线（周日 commit）只是启动检查点。

---

## 本周硬截止（不可推迟）

| 项 | 截止 | 验证 |
|----|------|------|
| **AI-food 或 HexoAIAgent 至少 1 个 commit** | 周日 23:59 | `git log` 看到新 commit |
| 证据表 v2 完成（3 个真实 JD 填入） | 周五 23:59 | `evidence-table/v1-2026-06-23.md` 有 v2 内容 |
| **3 个真实岗位 JD 收集** | **周三 23:59** | `inbox/jd/` 下有 3 个 md 文件 |
| 4 件事用户已确认（学校/城市/课业/AI-food 状态） | ✅ Day 1 已完成 | 见证据表顶部"基础信息" |

---

## Day 1 · 周一 2026-06-23 ✅ 已完成

- [x] 看完 UP 主视频《2026年IT学生别再只问学习路线：先做岗位证据表》
- [x] GitHub 盘点：28 个 repo，确定 AI-food + HexoAIAgent 作为两个核心作品
- [x] 战略主线确定：Java 后端 + AI 应用集成
- [x] 建立 JobHuntingDiary 仓库并 push
- [x] 回 4 件事（学校/城市/课业/AI-food 状态）
- [x] **关键修正**：投递截止日 8-31（不是 11 月）
- [x] **关键修正**：HexoAIAgent 重构为 Java + langchain4j
- [x] 更新 evidence-table v1 + 60-day-roadmap v2 + week-01

**今日产出**：仓库结构 + 5 个核心文档 + 决策记录 v2

---

## Day 2 · 周二 2026-06-24 · 选 3 个岗位

**任务**：
- [ ] BOSS 直聘 / 牛客 / 拉勾 / V2EX 搜 **"Java 后端" + "AI 应用工程师" + 保底方向**
- [ ] **筛选标准（深圳 + 双非）**：
  - 公司在深圳
  - 主战场 80%（中小厂 + AI 应用业务）
  - 可投 15%（华为 OD 优先）
  - 少投 5%（大厂正编碰运气）
  - 薪资真实 / 公司活跃 / JD 具体 / 愿意做
- [ ] 选 3 个 JD，保存到 `JobHuntingDiary/inbox/jd/2026-06-24-{1,2,3}-{公司}-{岗位}.md`
- [ ] 每个 JD 写 3 行笔记：为什么选 / 关键词 / 信心度

**预计耗时**：2-3 小时

---

## Day 3-4 · 周三~周四 · 拆三列证据表

**任务**：
- [ ] 在 `evidence-table/v1-2026-06-23.md` 升级到 v2（填入 3 个真实 JD 的拆解）
- [ ] 每个岗位三列：必须会的技术 / 必须交付的结果 / 我现在能拿出什么
- [ ] 第三列**直接写自己已有的 repo**（AI-food / HexoAIAgent / TravelCompanion）
- [ ] 没有的格子写"❌ 无"——这就是缺口
- [ ] 提取跨岗位交集 → 锁定 W2-W4 的 30 天作品目标

**预计耗时**：3-4 小时（含思考）

---

## Day 5 · 周五 · mall → AI-food 改造清单 + RAG demo

**任务**：
- [ ] 翻 mall README，列出想吸收的 5-8 个技术点
- [ ] 写成 `JobHuntingDiary/plans/mall-to-aifood-migration.md`
- [ ] 跟 all-in-rag 教程做 RAG 本地 demo（**不要 fork 教程代码，自己写**）
- [ ] Demo 跑通后 commit 到新仓库或 HexoAIAgent 子目录
- [ ] **注意**：RAG demo 用 Python 还是 Java？跟 HexoAIAgent-Java 重构统一 → **建议 Java + langchain4j**

**预计耗时**：4-5 小时

---

## Day 6 · 周六 · HexoAIAgent-Java 架构设计

**任务**：
- [ ] 设计"HexoAIAgent-Java + langchain4j"架构图
- [ ] 写接口设计（Spring Boot 暴露哪些 REST 端点）
- [ ] 写"边界声明"（能做什么 / 不能做什么）
- [ ] Agent 工程 6 步 checklist 落实到代码层面
- [ ] 写到 `JobHuntingDiary/plans/hexo-aiagent-java-design.md`

**预计耗时**：3-4 小时

---

## Day 7 · 周日 · 第 1 个 commit + 周复盘

**任务**：
- [ ] **强制 commit**：AI-food 或 HexoAIAgent 任一仓库至少 1 个新 commit（最低底线：写 README）
- [ ] 写 `JobHuntingDiary/diary/2026-06-29-week1-review.md`（用 `templates/weekly-review-template.md`）
- [ ] 用 `progress/checklist.md` 检查 W1 完成度
- [ ] 找 Mavis 或同学做 30 分钟 review
- [ ] 评估 HexoAIAgent-Java 重构进度（决定 W5-W8 是否需要调整）

**红线**：周日 23:59 前如果没有 commit → W2 计划降级 + Mavis 警告

---

## 本周风险

| 风险 | 应对 |
|------|------|
| 选岗位拖延 | 周二定不下就随便选 3 个，先动起来 |
| 看 mall 看了 2 天没动手 | 限时 4 小时，看完直接写改造清单 |
| HexoAIAgent 重构分散精力 | W1 只做架构设计 + RAG demo，重构代码推到 W5 |
| commit 没东西可写 | 先写 README / Swagger 配置 / 一个空 test |
| 8-31 倒计时忽略 | 每周日复盘里固定检查 "距 8-31 还有 X 天" |