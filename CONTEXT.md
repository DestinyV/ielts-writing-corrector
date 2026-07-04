# IELTS Writing Corrector

AI Agent 雅思写作批改技能。模拟资深雅思考官评分逻辑，提供基于官方四项标准（TA/TR、CC、LR、GRA）的专业批改报告。

## 目录结构

```
.
├── README.md           ← 项目文档
├── CHANGELOG.md        ← 版本变更记录
├── CONTEXT.md          ← 项目上下文（本文件）
├── LICENSE             ← MIT
├── VERSIONING.md       ← 通用 Skill 版本管理方案
├── .gitignore          ← Git 忽略规则
└── skills/
    └── ielts-writing-corrector/
        ├── SKILL.md            ← 核心技能定义
        ├── references/         ← 参考文件（评分细则 + 错误分类）
        └── tests/              ← 测试用例与验证记录
```

## 技能加载

Agent 平台通过 `skills/` 目录下的 `SKILL.md` 发现和加载技能。技能本身的参考文件（`references/`）由 SKILL.md 内部引用，测试文件（`tests/`）用于人工验证，不参与技能运行时加载。

## 核心术语

**评分标准：** TR（Task Response，任务回应）、TA（Task Achievement，任务完成度）、CC（Coherence & Cohesion，连贯与衔接）、LR（Lexical Resource，词汇资源）、GRA（Grammatical Range & Accuracy，语法范围与准确性）

**任务类型：** T1A（Academic Task 1，学术类图表）、T1G（General Training Task 1，培训类书信）、T2（Task 2，议论文）

**论证方法：** PEE（Point-Explanation-Example，论点-解释-例证）、Overview（概述段）
