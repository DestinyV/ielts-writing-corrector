# Changelog

本项目遵循 [Semantic Versioning](https://semver.org/lang/zh-CN/)，格式基于 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.0.0/)。

---

## [1.0.0] — 2026-07-04

### Added
- Academic Task 1 / GT Task 1 / Task 2 三种任务类型自动识别
- 基于官方四项标准（TA/TR、CC、LR、GRA）的 0-9 分独立评分
- 逐段精批（37 个标准化错误标签，含问题类型 + 修改建议）
- 总分速览条 `████░░` 可视化四项分数分布
- 词汇升级表（原文 → 问题 → 升级建议 + Band 级别标注）
- Band 7.5-8.0 范文参考段落
- 🔧 立即修改清单（3 项可即刻执行的改动）
- 🚀 提分路线图（🔴现在 → 🟡本周 → 🟢本月）
- Step 0 多源输入识别（URL / .md / .txt / .docx / .pdf / 图片 / 目录）
- GT 书信专项支持：语气速查表 + 7 种信件类型指南 + 格式检查清单
- 术语首次出现强制括号解释规则 + 输出前 5 项自检清单
- 中国考生高频错误分类参考（`references/common-errors.md`，8 类 37 标签）
- 官方评分细则参考（`references/band-descriptors.md`）
- GT 书信开头段常见问题诊断
- `README.md` 项目文档
- `VERSIONING.md` 通用 Skill 版本管理方案
- 4 个验证测试用例
