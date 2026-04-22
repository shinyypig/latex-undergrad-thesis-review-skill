# Structure And Depth Checklist

Use this when reviewing a full undergraduate thesis or when a chapter's role can be inferred from the main file.

## First Pass: Build The Thesis Map

Record a compact map before detailed comments:

- title and stated topic scope,
- Chinese/English abstract and keywords,
- chapter and section outline,
- rough chapter balance: very short, normal, or disproportionately long,
- figures, tables, equations, algorithms, citations, and appendices,
- whether each abstract/conclusion claim has a matching method, design, experiment, or result section.

Do not impose a universal word count unless the school requires one. Use size only as a warning signal; judge whether the chapter contains the expected substance.

## Undergraduate Quality Bar

A thesis should show that the student can understand the topic, organize prior work, apply professional knowledge, complete a design/research task, explain evidence, and write according to academic norms.

Flag as `【结构】` or `【内容】` when a section is grammatically readable but still underdeveloped.

## Common Structural Problems

- The title promises a method, system, dataset, experiment, or application that the body barely discusses.
- The abstract claims results or innovation that cannot be found in the main chapters.
- The introduction gives generic background but lacks objective, research content, method preview, or chapter arrangement.
- Related work is only a source-by-source list and does not classify, compare, or lead to the thesis task.
- Method/design chapters name modules but do not explain inputs, outputs, principles, formulas, or why those modules are used.
- Experiment/implementation chapters omit data source, preprocessing, environment, parameter settings, baselines, metrics, or result interpretation.
- Results are only figures/tables, with no analysis of what changed and why.
- A chapter or section has only one or two short paragraphs where the heading implies a substantive discussion.
- The conclusion repeats the introduction, omits limitations, or gives generic future work unrelated to the actual project.

## Chapter-Specific Expectations

### Introduction

Expected content: background, significance, research status summary, research objective, main work or workflow, and chapter arrangement.

Typical comments:

- `【结构】本节尚未明确论文的研究目标和主要工作，建议在背景之后补充“本文要解决什么问题、采用什么方法、完成哪些工作”。`
- `【内容】这里主要是通用背景，尚未过渡到本文具体课题，建议补充与题目直接相关的问题定义或应用场景。`

### Related Work

Expected content: classification of prior methods, comparison dimensions, citations near claims, and a transition to the student's method/design.

Typical comments:

- `【结构】相关研究目前更像文献罗列，建议按方法类别或问题维度重新组织，并说明各类方法的优缺点。`
- `【引用】该研究现状判断需要紧跟参考文献，避免形成无来源的概括性表述。`

### Method Or System Design

Expected content: overall pipeline, module responsibilities, inputs/outputs, core formulas or algorithms, design rationale, and relation to figures/tables.

Typical comments:

- `【内容】本节只列出了模块名称，缺少各模块的输入、输出和作用说明，难以支撑后续实现或实验。`
- `【公式】该公式中的关键符号尚未定义，建议在公式前后解释变量含义和计算目的。`

### Experiment Or Implementation

Expected content: data/source material, preprocessing, environment, settings, baselines/comparison objects, metrics, results, and analysis.

Typical comments:

- `【内容】实验设置不够完整，建议补充数据来源、划分方式、评价指标和主要参数设置。`
- `【内容】这里仅展示结果表，缺少对主要差异和原因的解释，建议结合指标变化说明实验结论。`

### Conclusion

Expected content: completed work, main findings, limitations, and future work.

Typical comments:

- `【结构】结论应给出全文最终结论，而不是简单重复绪论内容；建议概括已完成工作、主要结果和不足。`
- `【内容】未来工作较泛，建议结合本文实验或系统实现中暴露的问题提出可执行的改进方向。`

## Comment Placement

- For missing chapter-level content, anchor the comment at the chapter or section heading, or immediately after the first paragraph that reveals the gap.
- For mismatch between abstract/conclusion and body, anchor the comment at the claim in the abstract/conclusion.
- For thin sections, anchor the comment at the section heading or at the end of the only substantive paragraph.
- Avoid repeating the same structural comment in every paragraph; one precise chapter-level comment is usually enough.
