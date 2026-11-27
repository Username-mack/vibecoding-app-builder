---
name: vibecoding-app-builder
description: "Build a complete, usable custom application through VibeCoding with an AI agent, using a PRD-driven five-step workflow: draft a PRD from a rough idea, let the human trim requirements, add explicit visual/interaction rules, generate the app with hard constraints (no fake data, real CRUD, working interactions, explicit storage), then iterate and fix encoding issues. Use when the user wants to create an app or internal tool by describing needs to an AI (VibeCoding, vibe coding, 用AI做软件, 零代码做应用, 让AI写个小系统), especially small CRUD tools, project management systems, or when referencing a VibeCoding tutorial workflow."
agent_created: true
license: MIT
metadata:
  author: WorkBuddy
  version: "1.0"
  source: "Bilibili BV1Qfg56sEfb — 2分钟VibeCoding项目管理系统（UP主：英雄哪里出来）"
---

# VibeCoding 应用构建器

## 核心理念

把「说不清的需求」变成「写得下的规范」，再让 AI 按规范生成应用。

- **人的职责**：做减法、定规则、做主观判断。
- **AI 的职责**：补全需求、生成文档、写代码、执行细节。

本 skill 提炼自一段 VibeCoding 实操视频（B 站 BV1Qfg56sEfb，UP 主「英雄哪里出来」）。原视频全程只用豆包的「办公任务」模式 + 本地电脑技能，零代码做出一个项目管理系统。此处把流程抽象为**工具无关**的方法，适用于 WorkBuddy、Codex、Claude Code、Cursor 等任何能写文档、能生成代码的 AI Agent。

## 何时使用

- 用户想「用 AI 做一个 XX 系统 / 小工具 / 管理后台」，但需求还很模糊。
- 用户提到 VibeCoding、vibe coding、零代码做应用、让 AI 写个小系统。
- 用户做完一版应用后想迭代、想避免 AI 产出「默认界面」或「假数据」。

## 五步工作流

按顺序执行；每一步的产出是下一步的输入。详细提示词话术见 `references/prompting-playbook.md`。

### 第 1 步：粗描述 → AI 补全需求文档（PRD）

目的：不要求用户一开始就把需求讲清楚，先让 AI 补全。

操作要点：

1. 让用户用大白话说个大概（例如「做一个管理多个 VibeCoding 项目的系统」）。
2. 让 AI 生成完整需求文档（PRD），要求它自行拆解需求、搭建文档结构、逐模块填充正文。
3. 原视频操作：打开「办公任务」模式 → 本地电脑技能选择「文档」→ 要求「出个需求文档 PRD」；AI 会自主创建飞书文档并逐模块填充。
4. 通用做法（无飞书时）：让 Agent 把 PRD 写入项目根目录的 `requirements.md`，章节包含：目标、用户与角色、功能清单、数据模型、验收标准。

产出：`requirements.md`（初版 PRD，内容通常偏多）。

### 第 2 步：人工做减法（需求精简）

目的：删掉用户不需要的需求——**这是主观判断，AI 无法代劳**。

操作要点：

1. 逐章阅读 PRD 的大标题，让用户/执行者判断哪些模块不需要。
2. 直接删除不需要的整块需求。典型可删项：个人自用时不需要的角色体系、权限与安全体系。
3. 原则：**做减法比做加法简单**；先删大块，再抠细节。
4. 不要在这一步扩写新需求，只删。

产出：精简后的 `requirements.md`。

### 第 3 步：补充视觉与交互规则（关键，最容易被跳过）

目的：功能需求不描述界面长什么样，必须显式补上，否则 AI 会产出「默认界面」。

操作要点：

1. 向 AI 明确要求：设计视觉风格 + 交互动效，并补充进需求文档。
2. 尽可能清晰细致：配色/主题、布局、卡片与表格样式、动画、切换效果、空状态等。
3. 指定插入位置（例如「在第 5 章之后新增『视觉与交互规范』一章」），便于定位。
4. 若用户没有明确偏好，先给 2–3 个风格选项让用户选，再落文档。

产出：带「视觉与交互规范」章节的完整 PRD。

### 第 4 步：应用生成（必须同时给出四条硬约束）

目的：让 AI 在明确方向上生成可运行的应用，而不是演示性 Demo。

原视频操作：「办公任务」下技能选择「应用生成」。生成时同时给出以下四条硬约束：

1. **别用假数据**——不要 mock / 占位数据。
2. **真正实现增删改查**——CRUD 必须真跑通。
3. **所有交互务必有效**——按钮、表单、跳转都不能是摆设。
4. **明确数据存储方式**——写明是本地文件、IndexedDB、浏览器 localStorage 还是数据库。

没有详细需求和交互文档时，AI 干活方向不明确，容易产出不可用的壳子。

产出：可运行的应用代码。

### 第 5 步：测试、迭代与排错

目的：从「能跑」到「能直接用」。

操作要点：

1. 逐项测试功能：必填项校验、保存、查询、删除、切换等。
2. 迭代增强：追加视觉效果（如背景动效）、填入真实数据。
3. 乱码处理：中文乱码多为本地编码问题，与 AI 无关。常用 GBK 与 UTF-8 互转——GBK 乱码转 UTF-8，UTF-8 乱码转 GBK。
4. 最终交付前确认：应用可直接打开使用，且四类硬约束均满足。

产出：完善、可直接使用的成品。

## 输出检查清单

交付前逐条确认：

- [ ] PRD 经过人工精简，无多余模块。
- [ ] PRD 含视觉与交互规范章节。
- [ ] 应用无假数据。
- [ ] 增删改查真实可用。
- [ ] 所有交互有效。
- [ ] 数据存储方式已明确且已实现。
- [ ] 中文显示无乱码。

## 边界与限制

- 需求精简必须由人做主观判断，不要让 AI 自行决定删什么。
- 不追求一次生成完美；本工作流的核心是小步迭代，每步把「不确定」变成「写下来的确定」。
- 涉及真实业务数据时，先确认数据存储位置与权限，再让 AI 写入。
- 视频原文中「第 5 章以后插入」等表述指的是该次 PRD 的章节位置，实际执行时按当前 PRD 结构定位。

## 资源

- `references/prompting-playbook.md`：逐步可复制的提示词话术（含原视频话术与通用模板）。
