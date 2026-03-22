---
name: openclaw-control-center
description: OpenClaw 可视化控制中心技能。内置简洁模式（通俗易懂）+ 专业模式（完整数据），支持一键切换。当用户需要查看系统状态、打开控制台、或需要可视化运营面板时触发。
---

# openclaw-control-center

> 🦞 OpenClaw 可视化控制中心 — 让 AI 的运行状态一目了然

## 功能概述

**双模式可视化仪表盘**，所有触发方式均采集实时数据：

| 模式 | 触发 | 输出 |
|------|------|------|
| 🌿 简洁模式（默认） | `打开控制中心` | 大数字 + 说人话 + 说明提示 |
| 📊 专业模式 | `控制中心 --pro` | 完整表格 + 架构图 + API 端点 |
| 🔄 切换模式 | 页面顶部按钮 | 无需重新生成，直接切换 |

---

## 简洁模式 — 面向普通人

**核心三问**，每问配通俗说明：

| 卡片 | 数据 | 说明栏 |
|------|------|--------|
| 🌟 系统是否正常？ | ✓/⚠️/✕ + 状态列表 | 📌 绿色=正常，黄色=注意，红色=有问题 |
| 🧠 AI 用了多少？ | Token消耗 + 进度条 | 📌 Token=阅读量，越高越慢越贵 |
| 👥 谁在干活？ | 工作中/待命/空闲 三态 | 📌 工作中=正在处理，待命=有任务未开始 |

次要信息：定时任务 / 记忆系统 / 插件 / 安全设置（均附带通俗说明）

---

## 专业模式 — 面向技术人员

**完整数据表格 + 架构图 + API 端点：**

- 🚀 系统核心指标（Agent / Node.js / Shell / Build / 架构）
- 🧠 Token 趋势柱状图（7天）+ 详细消耗表
- 💻 会话管理（全部会话 Key / 通道 / Token / 详情）
- ⏰ Cron Jobs 表格（Job ID / Payload / Timeout / Delivery）
- 🧩 插件表格（类型 / 状态 / 说明 / 路径）
- 📡 消息渠道（WebSocket 地址 / 连接状态）
- 🧠 记忆系统（文件表格 + 三层架构说明）
- 🔗 OpenClaw 三层架构图（Tools → Skills → Plugins）
- 🔐 安全配置表格（5项默认安全策略）
- 🔌 Gateway API 端点（6个端点 + 鉴权说明）
- ⚡ Lobster 工作流引擎图

---

## 执行流程

### Step 1 — 采集实时数据（并行）

- `session_status()` → 系统状态 / 模型 / Token / 上下文
- `sessions_list()` → 全部会话
- `cron(action="list")` → 定时任务详情
- `gateway(action="config.get")` → Gateway / 插件 / 渠道配置

### Step 2 — 生成 HTML 仪表盘

生成 `~/.qclaw/workspace/control-center.html`，包含：
- 实时时间戳
- 简洁 + 专业两个模式（内置切换按钮）
- 所有数据以卡片/表格形式展示

### Step 3 — 浏览器打开

`Start-Process control-center.html` 自动用默认浏览器打开，默认显示简洁模式。

---

## 触发方式汇总

| 触发词 | 行为 |
|--------|------|
| `打开控制中心` | 生成简洁模式仪表盘 |
| `控制中心` | 简洁模式（默认） |
| `控制中心 --pro` | 专业模式 |
| `控制中心 --html` | 生成 HTML 并打开浏览器 |
| `系统状态` | 简洁模式系统状态 |
| `dashboard` | 简洁模式 |
| `系统总览` | 简洁模式 |

---

## 依赖

- OpenClaw 2026.3+（内置 browser / session_status / cron / gateway 等工具）
- 浏览器（Chrome / Edge / Firefox 均支持）
- 无需额外 npm / Node.js / git（静态实现）

---

## 错误处理

- 工具调用失败：记录错误，继续生成其余部分
- 缺失数据：显示 "—" 而非报错
- 超时（>5s）：标记 "⚠️ 获取超时"
- 无浏览器权限：提示用户手动打开 HTML 文件

---

## 灵感来源

GitHub: https://github.com/TianyiDataScience/openclaw-control-center

本技能为**静态实现版**，优势是无需安装即可使用。如需 React + WebSocket 全功能版，参看 README.md 部署指引。
