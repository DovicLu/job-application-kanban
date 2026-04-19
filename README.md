# 求职申请管理看板 · Job Application Kanban

> ## 🔍 项目简介
本项目是一个基于看板思想的求职申请管理系统，结合前端交互设计与 AI 能力，实现对求职过程的结构化管理与智能辅助。

相比传统表格工具，本系统通过可视化状态流转与 AI 建议机制，帮助用户在多任务、多阶段的求职过程中提升决策效率与执行效率。

![License](https://img.shields.io/badge/license-MIT-blue) ![Claude AI](https://img.shields.io/badge/Powered%20by-Claude%20AI-orange) ![Status](https://img.shields.io/badge/status-prototype-yellow)

---

## 📌 项目背景

大学生在求职季往往同时投递数十家公司，面临以下核心痛点：

| 痛点 | 描述 |
|------|------|
| 截止日期焦虑 | 多个 deadline 交织，容易遗漏 |
| 材料准备混乱 | 不清楚每家公司的笔试/面试材料进度 |
| 进度追踪困难 | 不同公司停在不同阶段，难以全局掌控 |
| 下一步不明确 | 不知道当前阶段该做什么 |

本项目通过**看板（Kanban）**视图 + **AI 智能建议**解决上述问题。

---

## ✨ 功能特性

### 核心功能
- **5 阶段看板**：待投递 → 已投递 → 笔试/测评 → 面试中 → 结果
- **截止日期预警**：距截止 ≤3 天自动标红告警，顶部横幅提醒
- **材料清单 + 进度条**：每张申请卡展示完成进度
- **面试时间展示**：面试安排直接显示在卡片上
- **统计总览**：顶部 4 项数字卡（投递数、紧急截止、面试数、Offer 数）

## 🧠 个人贡献与技术亮点

在本项目中，我主要完成了以下工作：

- 设计了基于“状态流转”的任务建模方式，实现多阶段求职流程的结构化表达
- 实现了完整前端交互逻辑（看板渲染、筛选、搜索、动态更新）
- 集成大模型 API（Claude），构建基于上下文的求职建议生成机制
- 设计 Prompt 工程，将结构化数据转化为可用于 AI 推理的输入
- 完成产品级 UI 设计（信息层级、颜色语义、交互逻辑）

该项目体现了我在**前端开发、系统设计、AI应用与产品思维**方面的综合能力。

### 交互功能
- 按职位类型筛选（技术 / 产品 / 运营 / 设计 / 数据）
- 关键词搜索公司或职位
- 点击申请卡 → AI 给出备考或下一步行动建议
- 快速新增申请（弹窗表单）

---

## 🛠 技术栈

| 层级 | 技术 |
|------|------|
| 前端框架 | 原生 HTML / CSS / JavaScript（无依赖） |
| AI 能力 | Anthropic Claude API（claude-sonnet-4-20250514） |
| 部署平台 | 可直接在浏览器打开 / GitHub Pages |
| 设计系统 | CSS Variables（支持自动暗色模式适配） |

---

## 🚀 快速开始

### 方式一：直接打开
```bash
# 克隆仓库
git clone https://github.com/your-username/job-application-kanban.git
cd job-application-kanban

# 直接用浏览器打开
open index.html
```

### 方式二：配置 Claude AI 建议功能

1. 获取 [Anthropic API Key](https://console.anthropic.com/)
2. 在 `config.js` 中填入你的 API Key：
```javascript
const CONFIG = {
  ANTHROPIC_API_KEY: "sk-ant-xxxxxxxx"
};
```
3. 重新打开 `index.html`，点击任意申请卡即可获得 AI 建议

> ⚠️ 注意：请勿将 API Key 直接提交到公开仓库，建议使用环境变量或本地配置文件（已在 `.gitignore` 中排除 `config.local.js`）

---

## 📁 文件结构

```
job-application-kanban/
├── index.html          # 主页面（看板全部逻辑）
├── config.js           # API 配置（示例，不含真实 Key）
├── prompts/
│   ├── system.md       # Claude 系统提示词
│   └── card_advice.md  # 申请卡片分析提示词模板
├── docs/
│   ├── design_spec.md  # 产品设计说明书
│   └── user_research.md # 用户痛点分析
└── README.md
```

---

## 🤖 AI 提示词设计

本项目使用了精心设计的提示词让 Claude 根据申请状态给出个性化建议。

### 系统提示词（System Prompt）
```
你是一位经验丰富的校招求职顾问，专门帮助大学生在秋招/春招季管理申请进度。
你了解各大互联网公司、咨询公司、金融机构的招聘流程。
当用户给你一条申请记录时，请根据当前阶段给出简洁、具体、可执行的下一步建议。
回答控制在 150 字以内，用 bullet point 列出 2-3 条行动项。
```

### 卡片建议提示词模板
```
申请记录：
- 公司：{company}
- 职位：{role}（{type}方向）
- 当前阶段：{stage}
- 截止日期：{deadline}（还剩 {daysLeft} 天）
- 材料完成度：{checkedCount}/{totalCount}

请给出针对当前阶段最重要的 2-3 条行动建议。
```

完整提示词见 [`prompts/`](./prompts/) 目录。

---

## 🎨 设计决策

### 为什么选择看板视图？
看板（Kanban）源于丰田生产管理，天然适合「多任务 × 多阶段」的进度追踪场景。相比表格，看板视图能让用户在 3 秒内判断每个阶段的拥堵情况，快速识别需要关注的申请。

### 颜色语义设计
| 颜色 | 含义 |
|------|------|
| 蓝色 | 信息类标签（职位类型、面试安排） |
| 橙色 | 警告（截止日期临近） |
| 红色 | 紧急（截止日期 ≤3 天） |
| 绿色 | 完成/成功（材料全部完成、已获 Offer） |
| 灰色 | 中性/待处理 |

---

## 📸 项目展示

![看板界面](./assets/demo1.png)
![AI建议](./assets/demo2.png)

## 📊 产品迭代计划

- [ ] v1.0 - 基础看板（当前版本）
- [ ] v1.1 - 数据持久化（LocalStorage）
- [ ] v1.2 - 日历视图（按截止日期查看）
- [ ] v1.3 - Offer 对比表（薪资、地点、方向比较）
- [ ] v2.0 - 多端同步（后端 + 用户账号）

---

## 📄 License

MIT License · 欢迎 Fork 和二次开发

---

## 🙋 作者

设计 & 开发：[Dovic]  
使用工具：Claude AI（Anthropic）辅助设计与代码生成  
项目类型：课程作品 / 个人项目
