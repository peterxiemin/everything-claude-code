# 工作流 - 多模型协作开发 (Multi-Model Collaborative Development)

多模型协作开发工作流 (调研 → 构思 → 规划 → 执行 → 优化 → 评审)，具备智能路由：前端 → Gemini，后端 → Codex。

## 用法

```bash
/workflow <任务描述>
```

## 上下文

- 待开发任务：$ARGUMENTS
- 带有质量门禁的结构化 6 阶段工作流
- 多模型协作：Codex (后端) + Gemini (前端) + Claude (编排)

## 你的角色

你是 **编排者 (Orchestrator)**，协调多模型协作系统。

---

## 核心工作流

### 第 1 阶段：调研与分析 (Research & Analysis)

`[模式: Research]`
1. **需求增强**：细化原始需求
2. **上下文检索**：检索现有代码背景
3. **需求完整性评分**：得分 ≥7 继续，<7 停止并补充

### 第 2 阶段：方案构思 (Solution Ideation)

`[模式: Ideation]`
- **并行分析**：Codex 分析后端可行性，Gemini 分析前端 UI/UX
- **方案对比**：输出至少 2 个选项，等待用户选择

### 第 3 阶段：详细规划 (Detailed Planning)

`[模式: Plan]`
- **并行规划**：Codex 输出后端架构，Gemini 输出前端架构
- **Claude 综合**：采纳两者的精华方案，保存到 `.claude/plan/task-name.md`

### 第 4 阶段：实现 (Implementation)

`[模式: Execute]`
- 严格遵循批准的方案进行代码开发
- 遵循项目代码标准

### 第 5 阶段：代码优化 (Code Optimization)

`[模式: Optimize]`
- **并行评审**：Codex 侧重安全、性能、错误处理；Gemini 侧重无障碍性、设计一致性
- **执行优化**：整合反馈并优化代码

### 第 6 阶段：质量评审 (Quality Review)

`[模式: Review]`
- 对照方案检查完成情况
- 运行测试并报告问题
- 请求用户最终确认
