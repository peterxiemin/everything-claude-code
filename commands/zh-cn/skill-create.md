---
name: skill-create
description: 分析本地 Git 历史以提取编码模式并生成 SKILL.md 文件。
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /skill-create - 本地技能生成

分析你代码库的 Git 历史，提取编码模式，并生成 `SKILL.md` 文件，以此教导 Claude 了解你团队的实践。

## 用法

```bash
/skill-create                    # 分析当前仓库
/skill-create --commits 100      # 分析最近 100 个提交
/skill-create --output ./skills  # 指定输出目录
/skill-create --instincts        # 同时为 continuous-learning-v2 生成“直觉” (instincts)
```

## 它的作用

1. **解析 Git 历史** - 分析提交记录、文件更改和模式
2. **检测模式** - 识别循环出现的工作流和约定
3. **生成 SKILL.md** - 创建有效的 Claude Code 技能文件
4. **可选创建直觉** - 用于持续学习系统

## 分析步骤

### 第 1 步：收集 Git 数据
分析最近的提交消息、文件更改频率以及命名约定。

### 第 2 步：检测模式
识别以下类型的模式：
- **提交约定** (如 `feat:`, `fix:`)
- **文件联动更改** (总是一起更改的文件)
- **架构约定** (文件夹结构和命名)
- **测试模式** (测试文件的位置、命名、覆盖率)

### 第 3 步：生成 SKILL.md
生成包含提交约定、代码架构、工作流和测试模式的 Markdown 文件。

### 第 4 步：生成直觉 (如果使用了 --instincts)
为持续学习系统生成 YAML 格式的直觉定义。
