# LaTeX 本科毕业论文审阅技能

用于审阅和批注本科 LaTeX 毕业论文，尤其适合中文论文、自定义类文件和 `hfut.cls` 风格项目。

## 主要能力

- 全文结构、章节深度和本科论文合格性审查
- 公式、符号、编号、引用和指标定义检查
- 图表包装器与实际图片内容检查
- 文献引用、术语一致性、缩写首次展开和中文学术表达检查
- 使用 `changes` / `\comment{...}` 输出导师式侧边批注
- 生成审阅版 PDF 首页汇总报告
- 支持 `preprint` 审阅布局与右侧批注空间

## 设计原则

`SKILL.md` 是低 token 的调度器：先扫描项目，再按需加载 `references/` 中的详细清单。不要把所有 reference 一次性读入上下文。

默认工作流：

1. 用 `rg` / `wc` 扫描主文件、章节、公式、图表、引用和审阅配置。
2. 只阅读主文件、类文件相关分支、摘要信息和目标章节。
3. 按需加载对应 reference。
4. 插入高信号 `\comment{...}` 批注。
5. 生成 `review-summary.tex`。
6. 编译 `latexmk -xelatex -outdir=tmp Thesis.tex`。
7. 交付 `tmp/Thesis.pdf`，通常复制为 `Thesis-review.pdf`。

## 文件结构

```text
.
├── SKILL.md
├── README.md
├── agents/openai.yaml
├── assets/
└── references/
    ├── figure-content-checklist.md
    ├── formula-checklist.md
    ├── review-checklist.md
    ├── structure-depth-checklist.md
    ├── summary-report.md
    └── thesis-standards.md
```

## 关键防错

- 不要把 `\comment{...}` 放进 `figure`、`table`、`tabular`、`adjustbox`、`caption`、`equation`、`align` 等浮动或脆弱环境。
- 图表/公式问题应锚定在附近正文句子或环境前后。
- 不覆盖原始提交版 `Thesis.pdf`，除非用户明确要求。
