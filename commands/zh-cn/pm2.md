# PM2 初始化 (PM2 Init)

自动分析项目并生成 PM2 服务管理命令。

**命令**：`$ARGUMENTS`

---

## 工作流

1. 检查 PM2 (如果缺失，通过 `npm install -g pm2` 安装)
2. 扫描项目以识别服务 (前端/后端/数据库)
3. 生成配置文件和各服务的命令文件

---

## 服务检测

| 类型 | 检测依据 | 默认端口 |
|------|-----------|----------|
| Vite | vite.config.* | 5173 |
| Next.js | next.config.* | 3000 |
| Express/Node | server/backend/api 目录 + package.json | 3000 |
| FastAPI/Flask | requirements.txt / pyproject.toml | 8000 |
| Go | go.mod / main.go | 8080 |

---

## 生成的文件

```
项目根目录/
├── ecosystem.config.cjs              # PM2 配置文件
└── .claude/
    ├── commands/
    │   ├── pm2-all.md                # 启动全部 + 监控
    │   ├── pm2-all-stop.md           # 停止全部
    │   ├── pm2-{port}.md             # 启动单个 + 查看日志
    │   ├── pm2-status.md             # 查看状态
    └── scripts/
        └── pm2-monit.ps1             # PM2 监控脚本
```

---

## 关键规则

1. **配置文件**：使用 `ecosystem.config.cjs` (而非 .js)
2. **Node.js**：直接指定 bin 路径和解释器
3. **打开新窗口**：使用 `wt.exe` (Windows Terminal) 或相应平台的终端命令
4. **更新 CLAUDE.md**：在项目 `CLAUDE.md` 中追加 PM2 服务信息

---

## 执行后摘要示例

```
## PM2 初始化完成

**服务列表：**

| 端口 | 名称 | 类型 |
|------|------|------|
| {port} | {name} | {type} |

**Claude 命令：** /pm2-all, /pm2-all-stop, /pm2-{port}, /pm2-status

**提示：** 首次启动后请运行 `pm2 save` 以保存进程列表。
```
