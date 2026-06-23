# mall → AI-food 改造清单（v1 · 2026-06-23）

> **数据源**：mall README（webfetch）+ AI-food README（webfetch）**双 README 对照**，非源码级分析。
>
> **核心结论**：AI-food 实际上是个**功能相当完整**的工业级项目——缺的是**部署、测试、压测、README 包装**这 4 件事，不是技术栈补齐。

---

## 一、为什么不需要"补技术栈"

mall 是 Spring Boot 3.5 + MyBatis + Elasticsearch + RabbitMQ 的**商城系统**；
AI-food 是 Spring Boot 3.4 + JPA + Spring AI + WebSocket 的**社交推荐系统**。

**两个项目业务场景不同，技术栈不必对齐**。强行抄 mall 的 RabbitMQ 进 AI-food = 过度设计。

**真正应该对齐的是"工程化基线"**——4 件 mall 有、AI-food 没有的事：

## 二、改造清单（按 P0/P1/P2）

### P0 · 必做（W1 红线 + W2-W4 核心）

#### 1. README 5 段式升级（W1 红线 · 今晚做）

**现状**：AI-food 已有 README（详细），但偏技术清单，缺**作品包装视角**。

**要补的 4 段**：

```markdown
## 1. 解决了什么问题  ← 缺
> 场景：谁，在什么时候，用它做什么
> 痛点：场景里的具体痛点
> 方案：怎么解决的

## 5. 关键决策（面试会被问的）  ← 缺
> 为什么选 Spring AI 不直接调 OpenAI API？
> 为什么用 Redis Lua 不用数据库事务？
> 为什么选 Vue + Vant 不选 React？

## 7. 复盘（做完再写）  ← 缺
> 如果重做一次会改的 3 件事

## 9. 数据 & 性能（如果有）  ← 缺（待压测后填）
> 接口 P95 / P99 / 推荐准确率
```

**今晚 19:30-21:30 的任务**——按 `templates/project-readme-template.md` 升级这 4 段。

---

#### 2. Docker Compose 部署（W2 · 6-30 ~ 7-6）

**现状**：README 启动方式是 `mvn spring-boot:run`，无 Docker。

**要做到**：

```yaml
# docker-compose.yml
version: '3.8'
services:
  ai-food-backend:
    build: ./backend
    ports: ["8080:8080"]
    depends_on: [mysql, redis]
  mysql:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: ...
  redis:
    image: redis:7-alpine
  # 前端可选
```

加上：
- `backend/Dockerfile`（多阶段构建）
- `.dockerignore`
- `docker-compose up -d` 一键启动

**部署平台**：阿里云学生机（9.9/月）或腾讯云学生优惠。

---

#### 3. 单元测试 + 集成测试（W3 · 7-7 ~ 7-13）

**现状**：测试目录里没有可见的测试文件。

**目标**：
- 至少 10 条单元测试（覆盖核心 Service）
- 至少 5 条集成测试（用 Testcontainers 跑 MySQL + Redis）
- CI 跑通 GitHub Actions

**优先测试的 Service**：
- `ai/`（AI 推荐逻辑）
- `auth/`（认证）
- `like/`（Redis Lua 点赞）
- `feed/`（推荐发布）
- `bloom/`（布隆过滤器）

---

#### 4. 压测报告（W4 · 7-14 ~ 7-20）

**现状**：用户说"稳定性一般"——但没数据。

**工具**：JMeter / wrk / k6 / Gatling

**要测的**：
- 接口 P95 / P99（重点：`/api/feed`、`/api/ai/chat`、`/api/like`）
- 并发用户数（100 / 500 / 1000）
- Redis 缓存命中率
- 数据库慢查询

**产出**：`docs/performance-test-report.md` + 截图

---

#### 5. 部署上线（W2 末 · 7-6 前）

**目标**：公开可访问的 URL，写进简历。

**清单**：
- [ ] 阿里云/腾讯云学生机购买 + SSH 配置
- [ ] Docker Compose 部署
- [ ] 域名（可选）+ Nginx 反向代理
- [ ] HTTPS（Let's Encrypt 免费）
- [ ] 进程守护（systemd）
- [ ] 日志收集（写到 /var/log）

---

### P1 · 建议做（W5-W8）

| 项 | 价值 | 截止 |
|----|------|------|
| Spring Boot Actuator | `/actuator/health` 健康检查 | W5 |
| SpringDoc 替换/补充 Knife4j | OpenAPI 3.0 标准（部分企业 JD 要求） | W6 |
| API 限流细化 | 防刷 + 保护后端 | W7 |
| 慢 SQL 优化 + 索引分析 | 性能基线 | W8 |

### P2 · 可选

| 项 | 价值 |
|----|------|
| Elasticsearch 全文搜索 | 业务增强（feed 搜索） |
| ELK 日志收集 | 排查问题 |
| Grafana + Prometheus 监控 | 可视化指标 |

---

## 三、AI-food 简历写法（基于真实技术栈）

✅ **正确写法**（强调 AI 应用 + 工程化）：

> **AI-food · 智能美食推荐与社交平台** | [demo URL]
>
> - 基于 Java 21 + Spring Boot 3.4 + Spring AI 1.0.0-M6 的 LLM 集成后端 + Vue 3 移动端前端
> - 多轮对话式推荐：7 个参数收集 → LLM 生成 → 上下文记忆
> - 完整社交功能：WebSocket 聊天 + Redis Lua 点赞 + 布隆过滤器推荐去重
> - 工程化：Docker Compose 一键部署 + Swagger/Knife4j API 文档 + Redis 多级缓存 + IP 限流
> - 测试：JUnit 单元测试 X 条 + Testcontainers 集成测试 Y 条 + JMeter 压测报告

❌ **错误写法**（信息密度低）：

> 熟练使用 Java、Spring Boot、Redis、Vue 等技术栈，独立开发 AI-food 项目

---

## 四、决策记录（AI-food 关键技术选择）

| 决策 | 选择 | 替代方案 | 为什么 |
|------|------|---------|--------|
| LLM 集成 | **Spring AI** | 直接调 OpenAI SDK | 与 Spring Boot 生态一致；后续切换模型方便 |
| 前端框架 | **Vue 3 + Vant** | React + Ant Design Mobile | 移动端优先；个人熟悉度高 |
| 缓存策略 | **Redis + Caffeine + Redisson** | 仅 Redis | 多级缓存降低 Redis 压力；Redisson 提供分布式锁 |
| 点赞原子性 | **Redis Lua 脚本** | 数据库事务 + 乐观锁 | 性能更高；避免数据库连接池打满 |
| 推荐去重 | **布隆过滤器** | 数据库唯一索引 | O(1) 判断；内存占用低；允许误判 |

---

## 五、本周（W1）任务清单

- [x] **已生成**：本改造清单（mall-to-aifood-migration.md）
- [ ] **Day 1 今晚**：升级 AI-food README 5 段式（W1 红线 commit）
- [ ] **Day 5 周五**：本文档 v2 补充（基于实际 clone 后看到的源码）
- [ ] **Day 7 周日**：W1 复盘，评估本清单的准确性

---

## 六、避坑（不要做的事）

- ❌ **不要硬塞 RabbitMQ**——AI-food 用 WebSocket 做 IM，不需要 MQ
- ❌ **不要硬塞 Elasticsearch**——当前搜索需求不大，Caffeine + Redis 已够
- ❌ **不要 fork mall 改造成新项目**——AI-food 业务场景完全不同
- ❌ **不要重写**——AI-food 已经能用，包装 > 重写
- ❌ **不要追新框架**——Spring Boot 3.4 已经够现代

---

## 七、风险

| 风险 | 应对 |
|------|------|
| 实际源码比 README 复杂 | Day 5 周五真正 clone 后更新本文档 v2 |
| Docker 部署踩坑 | W2 整周留给部署，预留 2 天 buffer |
| 压测暴露严重性能问题 | W4 末才压测，发现问题有 1-2 周迭代时间 |
| 公开 URL 被攻击 | 加 IP 限流（已有）+ Nginx fail2ban |