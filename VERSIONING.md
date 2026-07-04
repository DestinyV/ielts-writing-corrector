# Skill 版本管理方案 v1.0

> 适用于任何 AI Agent Skill 项目的通用版本管理规范。
> 无论运行在 ZCode、Claude Code、Cursor、或其他 Agent 平台，均可直接套用。

---

## 1. 核心原则

Skill 是一种**指令型项目**——它定义的是 AI 的行为契约，不是可执行代码。因此版本管理的核心问题是：

> **这个版本的行为和上一版本是否兼容？用户/Agent 是否需要调整使用方式？**

三条铁律：

1. **SKILL.md 的 frontmatter 必须包含 `version` 字段** —— 这是 Skill 身份的唯一版本依据
2. **每个版本发布必须有 CHANGELOG 条目** —— 记录 Add / Change / Fix / Remove
3. **Git tag 命名严格遵循 `v<semver>`** —— v1.0.0, v2.1.0，不可省略前缀 `v`

---

## 2. 语义化版本定义

对 Skill 而言，Semver 的判定标准如下：

### MAJOR（X.0.0）—— 不兼容变更

以下任何一种变化，触发主版本号升级：

| 变更类型 | 示例 |
|---------|------|
| Skill 重命名 | `ielts-corrector` → `writing-coach` |
| 触发条件改变 | 原来触发短语改了，已有用户需要重新适应 |
| 输入格式不兼容 | 原来接受纯文本，现在强制要求 JSON |
| 输出格式不兼容 | 原来 Markdown 报告，现在改成纯 JSON API 返回 |
| 核心能力移除 | 移除 Task 1 批改能力 |
| 平台迁移 | 从 ZCode 迁移到 Claude Code，SKILL.md 格式重写 |

> 💡 **简单判断：** 用户/Agent 是否需要修改现有的使用方式来适配新版本？是 → Major

### MINOR（X.Y.0）—— 新增能力，向后兼容

| 变更类型 | 示例 |
|---------|------|
| 新增任务类型 | 原来只批改 T2，现在也支持 T1 |
| 新增输入方式 | 原来只接受粘贴，现在也支持 URL / 文件 |
| 新增输出模块 | 增加了"总分速览条"、"立即修改清单" |
| 质量显著提升 | 标签从 24→37 个，诊断深度大幅提高 |
| 新增参考文件 | 新增 `references/gt-guide.md` |

> 💡 **简单判断：** 老用户不改变使用方式，但获得了新能力？是 → Minor

### PATCH（X.Y.Z）—— 修复与微调

| 变更类型 | 示例 |
|---------|------|
| Bug 修复 | 某个标签名称写错了，修正 |
| 措辞优化 | 报告模板中某句话改得更清楚 |
| 错别字修正 | `experiance` → `experience` |
| 格式微调 | 表格对齐、emoji 调整 |
| 测试用例增补 | 新增 1 个 edge case 测试 |

> 💡 **简单判断：** 行为和能力完全不变，只是修了小问题？是 → Patch

---

## 3. 标准项目结构

每个遵循此方案的 Skill 项目应包含以下文件：

```
my-skill/
├── SKILL.md              ← [必需] 核心定义，frontmatter 含 version
├── CHANGELOG.md           ← [必需] 版本变更记录
├── README.md              ← [必需] 项目说明文档
├── VERSIONING.md          ← [推荐] 本版本管理方案（可从此项目复制）
│
├── references/            ← [可选] 参考文件
├── tests/                 ← [推荐] 测试用例
├── scripts/               ← [可选] 辅助脚本
│
├── .gitignore             ← [推荐]
└── LICENSE                ← [推荐]
```

### SKILL.md frontmatter 最小规范

```yaml
---
name: my-skill
version: 1.2.3
description: 简要描述此技能的功能和触发条件。
---
```

`version` 字段为此方案的强制要求，不与任何特定平台冲突（所有主流 Agent 平台忽略未知 frontmatter 字段）。

---

## 4. Git 工作流

### 分支策略

```
main        ← 稳定发布分支，每个 commit 对应一个 tag
  │
  ├─ develop    ← 开发集成分支（可选，单人项目可省略）
  │    │
  │    ├─ feature/xxx   ← 功能分支
  │    └─ fix/xxx       ← 修复分支
  │
  └─ tag: v1.0.0, v2.0.0, v2.1.0 ...
```

**单人项目简化流（推荐）：**

```
main:  [v1.0.0] --- [v2.0.0] --- [v2.1.0] --- ...
```

直接在 `main` 上开发，每次稳定版本打 tag。适合大多数 Skill 项目。

### Commit 规范

使用 [Conventional Commits](https://www.conventionalcommits.org/)：

```
feat: Add GT letter tone quick-reference table
fix: Correct [模板化] label to [模板开头]
docs: Add README.md
chore: Bump version to 2.1.0
```

### 发布流程

```bash
# 1. 确保所有改动已测试验证
# 2. 更新版本号
vim SKILL.md          # version: X.Y.Z

# 3. 更新 CHANGELOG
vim CHANGELOG.md       # 新增版本条目

# 4. 提交版本发布
git add -A
git commit -m "chore: Release vX.Y.Z"

# 5. 打标签
git tag -a vX.Y.Z -m "vX.Y.Z: <一句话总结>"

# 6. 推送
git push origin main
git push origin vX.Y.Z
```

---

## 5. CHANGELOG 格式

严格遵循 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.0.0/)，四个标准分类：

| 分类 | 含义 |
|------|------|
| **Added** | 新增的功能、能力、输入方式 |
| **Changed** | 变更的现有行为（兼容范围内） |
| **Fixed** | Bug 修复 |
| **Removed** | 移除的功能（通常伴随 Major 版本） |

模板：

```markdown
## [X.Y.Z] — YYYY-MM-DD

### Added
- 新增内容

### Changed
- 变更内容

### Fixed
- 修复内容
```

---

## 6. 版本号生命周期示例

以 `ielts-writing-corrector` 为例：

```
v1.0.0  初始发布
  │     T1A / T1G / T2 识别 + 四项评分 + 逐段精批
  │
v2.0.0  重大升级 (Minor 累积 → Major)
  │     报告表格化 + GT 专项 + 标签 37 个 + 术语解释 + 自检清单
  │     ⚠ 输出报告格式显著变化，升级主版本号
  │
v2.1.0  功能增强 (Minor)
  │     Step 0 多源输入 + README + CHANGELOG
  │
v2.1.1  小修 (Patch)
         typo 修正
```

---

## 7. 常见问题

### Q: 为什么用 Git tag 而不是只在 SKILL.md 里写 version？

Git tag 是业界标准的不可变版本标记，GitHub/GitLab 自动生成 Release 页面，支持版本对比 (`git diff v1.0.0 v2.0.0`)，且不依赖任何平台的解析能力。

### Q: 如果我的平台不支持 SKILL.md frontmatter 的 version 字段？

所有主流 Agent 平台都忽略未知 frontmatter 字段，添加 `version` 不会导致任何兼容性问题。如果平台未来支持原生的版本管理，你的历史数据立即可用。

### Q: 单人项目真的需要这么规范吗？

需要。Skill 的消费者是 AI Agent，不是人类——AI 更需要清晰的版本信号来判断行为是否变化。一份好的 CHANGELOG 可以帮助 Agent 理解"这个版本相比上次使用时有什么不同"。

### Q: 什么时候 Minor 应该升级为 Major？

当累积的 Minor 变更已经显著改变了 Skill 的行为模式时，应在下一个版本升级 Major。例如：`v1.0 → v2.0` 不一定是某个不兼容变更，也可以是对大量 Minor 变更的"里程碑式"总结。

---

## 8. 快速启动清单

在新 Skill 项目中应用此方案：

- [ ] 在 SKILL.md frontmatter 添加 `version: 0.1.0`
- [ ] 创建空 `CHANGELOG.md`：
  ```markdown
  # Changelog
  ## [0.1.0] — YYYY-MM-DD
  ### Added
  - 初始版本
  ```
- [ ] 创建 `README.md`（至少包含简介 + 安装说明 + 使用示例）
- [ ] 复制本 `VERSIONING.md` 到项目中
- [ ] `git init` → `git add -A` → `git commit -m "chore: Init v0.1.0"`
- [ ] `git tag -a v0.1.0 -m "v0.1.0: Initial version"`
- [ ] 设置远程仓库并推送

---

*本方案本身遵循语义化版本，当前版本 `v1.0`。*
