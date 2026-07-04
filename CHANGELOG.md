# Changelog

本项目遵循 [Semantic Versioning](https://semver.org/lang/zh-CN/)，格式基于 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.0.0/)。

---

## [2.1.0] — 2026-07-04

### Added
- Step 0: 多源输入识别与获取（URL / .md / .txt / .docx / .pdf / 图片 / 目录）
- 混合输入处理 + 获取失败兜底策略
- 内容提取后向用户确认摘要机制
- `README.md` 项目文档
- `CHANGELOG.md` 版本记录
- `VERSIONING.md` 通用 Skill 版本管理方案

### Changed
- SKILL.md `description` 更新体现多输入支持
- 核心能力新增"多源输入获取"
- SKILL.md frontmatter 新增 `version` 字段

---

## [2.0.0] — 2026-07-04

### Added
- GT 书信语气速查表 + 7 种信件类型指南 + 5 项格式检查清单
- 4 个 GT 专用标签：`[语域]` `[格式错误]` `[要点遗漏]` `[要点不均]`
- 总分速览条 `████░░` 可视化
- 立即修改清单（3 项可即刻执行）
- 输出前 5 项自检清单
- 术语强制括号解释规则
- 开头段常见问题诊断（common-errors.md §8）
- 错误标签扩充至 37 个

### Changed
- 报告模板全面表格化（评分/修改清单/结构分析/词汇升级/提分路线）
- 批改原则重组为 5 个子章节
- 标签使用规范：强制从速查表选取

### Fixed
- 标签体系不一致（自创标签 → 标准化）
- Task 1 逐段精批覆盖不足

---

## [1.0.0] — 2026-07-04

### Added
- 初始发布
- Academic Task 1 / GT Task 1 / Task 2 三种任务类型识别
- TR/TA、CC、LR、GRA 四项 0-9 分独立评分
- 逐段精批 + 词汇升级表 + 7.5+ 范文参考
- 提分路线图
- 中国考生高频错误分类（初始 24 标签）
- 官方评分细则参考（band-descriptors.md）
- 4 个验证测试用例
