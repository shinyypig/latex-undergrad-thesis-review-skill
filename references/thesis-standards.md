# Undergraduate Thesis Standards

Use these requirements as a practical baseline for reviewing an undergraduate thesis. Apply them as review heuristics rather than as absolute law when the school template, college notice, or advisor instructions clearly differ.

## Normative Baseline

Use the school's own本科毕业论文（设计）规范 first. When it is absent or incomplete, use this baseline:

- GB/T 7713.1-style thesis structure: front matter, main body, references, necessary appendices, and ending material.
- Undergraduate thesis抽检 perspective: judge "选题意义、写作安排、逻辑构建、专业能力、学术规范" as a合格性 review, not as journal-level novelty review.
- GB/T 7714-style citation and bibliography consistency, following the version required by the school template or BibTeX style.
- Standard Chinese academic writing, legal units of measurement, consistent terminology, symbols, abbreviations, punctuation, figures, tables, formulas, and references.

## Core Principle

Judge the thesis by undergraduate standards:

- complete and compliant,
- readable and teachable,
- method and experiment descriptions basically self-contained,
- claims supported by citations or results,
- structure coherent from title and abstract through introduction, main body, and conclusion,
- chapters balanced enough that the thesis does not look padded in one place and empty in another.

Do not over-demand journal-level novelty, theoretical depth, or extremely compressed writing.

## Whole-Thesis Structure Pass

Before writing many local comments, map the thesis at the document level:

- title, Chinese/English abstract, keywords,
- table of contents and chapter sequence,
- approximate size and density of each chapter or major section,
- figures, tables, formulas, algorithms, citations, bibliography, and appendices,
- whether the title, abstract, introduction, methods, experiments/design, and conclusion all describe the same work.

Flag structural problems when:

- a required or expected component is missing,
- a chapter is only a few paragraphs or mostly placeholders,
- a chapter consists mainly of definitions, literature listing, screenshots, tables, or formulas without explanatory prose,
- a claimed contribution in the abstract or conclusion has no matching method, experiment, design, or result section,
- chapter headings promise content that the body does not deliver,
- conclusion, limitations, or future work are absent when the thesis makes improvement or application claims.

## Front Matter

### Title

- Check whether the title matches the actual technical scope.
- Check whether the title is too broad, too vague, or inconsistent with the body text.
- Check whether key terms in the title are used consistently in the chapter text.

### Abstract And Keywords

- Check whether the abstract contains at least:
  - background or problem,
  - method or approach,
  - experiment or application context,
  - main result or conclusion.
- Check whether the abstract avoids unnecessary citations, figures, tables, and unexplained abbreviations.
- Check whether keywords are consistent with the title and body.
- Check whether Chinese and English abstracts correspond in meaning when both exist.

## Chapter Expectations

### Introduction

- Check whether it includes background, significance, related-status summary, research objective, research content or workflow, and chapter arrangement.
- Check whether the problem statement is concrete enough.
- Check whether the chapter arrangement matches the actual later chapters.
- Check whether it avoids spending most of the chapter on generic background without narrowing to the student's topic.

### Related Work / Domestic And Foreign Status

- Check whether related work is classified or organized rather than listed mechanically.
- Check whether different methods are compared on meaningful dimensions.
- Check whether the chapter eventually leads to the need for the student's method or design choice.
- Check whether cited work is summarized accurately and close citations are present.

### Method / System Design

- Check whether the method chapter clearly explains the overall pipeline, modules, variables, and design motivation.
- Check whether symbols in formulas are defined near first use.
- Check whether architecture figures and algorithm descriptions align with the body text.
- Check whether module descriptions are more than a naming list; each important module should explain input, output, function, and reason for use.
- Check whether formulas, pseudo-code, or model diagrams are connected to the actual implementation or experiment.

### Experiments / Implementation

- Check whether the data source, split, preprocessing, settings, baselines, and evaluation metrics are stated.
- Check whether table and figure results are interpreted rather than only displayed.
- Check whether comparison is fair enough for an undergraduate thesis.
- Check whether ablation, parameter study, or error analysis is present when the thesis claims an improvement.
- Check whether implementation environment, software/hardware, parameter settings, and reproduced baselines are sufficient for a reader to understand what was done.
- Check whether result claims match the numbers in tables/figures and avoid unsupported wording.

### Conclusion

- Check whether the conclusion summarizes completed work and main findings.
- Check whether limitations are acknowledged when appropriate.
- Check whether future work is not generic filler only.
- Check whether it is a final overall conclusion, not a simple repeat of chapter summaries or introduction wording.

## Citation And Reference Norms

- Check whether all non-trivial factual claims or literature summaries have citations.
- Check whether citations are attached close to the relevant statement.
- Check whether cited references actually appear in the bibliography.
- Check whether bibliography entries are complete enough and consistently formatted under the project's style.
- Check whether uncited references remain in the bibliography.

## Formula Norms

- Check whether important formulas are introduced in the body text before or near the display equation.
- Check whether variables and symbols are explained at first use.
- Check whether formula punctuation matches the surrounding sentence.
- Check whether the notation is consistent across sections.
- Check whether formulas are not inserted without interpretation.
- Check whether equations are numbered when the project/school style expects numbering, especially when there are two or more display equations.
- Check whether equation numbers, labels, and `\eqref` / `\ref` targets match.
- Check whether long formulas break at relation or operator symbols and remain readable.
- Check whether units, dimensions, subscripts, superscripts, vector/matrix notation, and metric definitions stay consistent across chapters.
- Check whether derivations or transformations explain the step that matters for the student's method rather than dumping a final expression.

## Figure And Table Norms

- Check whether every important figure and table is referenced in the body text.
- Check whether captions are informative rather than only naming the object.
- Check whether numbering and subfigure ordering are consistent.
- Check whether tables are readable and not overloaded with unexplained abbreviations.
- Check whether result tables state metrics, units, and comparison objects clearly.
- Check whether figures and tables have enough interpretation in the surrounding prose, especially in result sections.

## Writing Norms

- Prefer objective academic language over colloquial claims.
- Flag unsupported wording such as "significantly improves", "substantially increases", or "works very well" when no evidence is given nearby.
- Check whether paragraph logic flows from claim to evidence to conclusion.
- Check whether first-person phrasing, spoken-language fillers, and subjective evaluation are excessive for the school's style.

## Formatting And Consistency

- Check whether labels are ASCII and concise.
- Check whether chapter names, section names, captions, and in-text references use the same terminology.
- Check whether English terms, units, punctuation, and capitalization are used consistently.
- Check whether full-width and half-width punctuation are mixed awkwardly around English tokens, formulas, or citations.
