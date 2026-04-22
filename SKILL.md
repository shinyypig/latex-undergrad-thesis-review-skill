---
name: latex-undergrad-thesis-review
description: Review and annotate undergraduate LaTeX theses, especially Chinese graduation theses built on custom class files such as hfut.cls. Use when reviewing whole-thesis structure, chapter depth, formula and notation quality, chapter text, citations, labels, captions, figures, tables, and bibliography consistency; when adding mentor-style review comments with the changes package; when inserting a first-page review summary report into the annotated PDF; or when preparing a review-only layout that keeps the body-text width roughly unchanged while adding right-side page space for todo-style comments.
---

# LaTeX Undergrad Thesis Review

Treat the thesis as an undergraduate thesis. Prioritize format compliance, whole-thesis structure, chapter completeness and depth, clear academic Chinese, citation hygiene, formula and notation quality, terminology consistency, and figure/table correctness. Do not review it like a journal submission unless the user explicitly asks for that standard.

## Default Review Mode For This Workflow

This skill is designed around the concrete workflow used in the current project:

- Use `changes`
- Use side `todo` comment boxes rather than footnotes
- Prefer `\comment{...}` only unless the user explicitly asks for direct `\added` / `\deleted` / `\replaced`
- Keep review configuration in `hfut.cls`
- Insert a review-only summary report as the first page of the annotated PDF unless the user explicitly opts out
- Allow a review-only page layout in `Thesis.tex` so the body-text width stays roughly unchanged and the right side gains extra physical page width for comments

When a project already has an established review setup, adapt to it. For the common `hfut.cls` workflow in this project family, treat `mode=preprint` as the review entry point and enhance that branch directly rather than introducing a second review mode.

## Concrete Workflow

1. Determine the review scope:
   - If only one chapter is provided, review that chapter but still infer its role in the whole thesis from `Thesis.tex`, the table of contents, and neighboring chapter names when available.
   - If the main file or full thesis is available, first run a whole-thesis structure and depth pass before sentence-level annotation.
2. Read the class file and main file to determine:
   - how `changes` is loaded,
   - whether side comments use `todonotes`,
   - whether a dedicated review mode such as `reviewlayout` is active,
   - whether the page width has been expanded on the right side for review.
3. Build a thesis map when the main file is available:
   - front matter: title, Chinese/English abstract, keywords, table of contents,
   - chapter and section outline,
   - approximate balance of chapters and sections,
   - figures, tables, equations, algorithms, citations, and bibliography files.
4. Run a structure and depth audit before local comments:
   - whether the thesis contains the expected front matter, introduction, body, conclusion, references, and necessary appendices,
   - whether each chapter has enough substantive content for its role,
   - whether chapter sequence, headings, and transitions match the title, abstract, and claimed work,
   - whether methodology, experiment, implementation, result analysis, limitations, and future work are present where expected.
5. Read the target chapter `.tex` file in full.
6. Review paragraph by paragraph and sentence by sentence.
7. Review every displayed formula, equation, algorithmic expression, and important inline symbol for introduction, numbering, references, symbol definitions, unit consistency, punctuation, and notation consistency.
8. Review every referenced figure or plot at two levels:
   - LaTeX wrapper level
   - actual image-content level
9. Insert `\comment{...}` exactly at the problem location.
10. Create or update the first-page review summary report for the annotated PDF.
11. Compile with `latexmk -xelatex -outdir=tmp Thesis.tex`.
12. Verify compilation success and only inspect rendered PDF pages when the user asks for it or when there are signs that comments have become unusable.

Load [references/structure-depth-checklist.md](references/structure-depth-checklist.md) for full-thesis or chapter-completeness review. Load [references/formula-checklist.md](references/formula-checklist.md) whenever the chapter contains equations, math-heavy descriptions, algorithms, metrics, losses, or model definitions.
Load [references/summary-report.md](references/summary-report.md) before generating the first-page review summary.

## Required Placement Rule

Every `\comment` must be attached to the exact problematic location.

- For sentence-level issues such as missing citations, put the comment after the sentence-ending punctuation.
- For term, abbreviation, author-name, key-name, label, axis-label, or caption problems, attach the comment immediately after the problematic token or phrase.
- For figure or table wrapper issues, anchor the comment in the surrounding body text when possible; avoid placing `\comment` inside floating `figure` or `table` environments unless you know the layout is stable.
- For formula issues, anchor the comment immediately after the display equation, symbol definition, or sentence that introduces the equation. Avoid placing comments inside fragile math environments unless the project already does so safely.
- For broad structural issues, anchor the comment at the relevant chapter or section heading, opening paragraph, or missing-content boundary, and make the missing expectation explicit.
- Do not leave broad paragraph-end comments when the actual issue is local.

## Priority Rules

Separate issues into two buckets before writing comments.

### Must-fix or must-verify

Comment on these by default:

- missing citations for factual or literature-summary statements,
- first-use abbreviation expansion failures,
- grammar that changes meaning or readability materially,
- author-surname and bibliography-key mismatches,
- broken or non-ASCII labels when the project requires ASCII labels,
- figure, table, or formula problems that block interpretation,
- missing formula explanation, undefined symbols, inconsistent notation, or unreferenced numbered equations,
- structurally thin chapters or sections that fail their expected thesis role,
- missing chapter elements expected in an undergraduate thesis section,
- unsupported strong claims near results or conclusions.

### Nice-to-have optimization

Comment on these only when they add clear value:

- mild wording polish,
- small terminology cleanup when the meaning is still clear,
- repetition that does not affect correctness,
- optional caption tightening,
- style improvements that do not change correctness or compliance.

## Comment Density Control

Avoid over-annotation.

- Prefer one high-signal comment per local issue.
- If a sentence already has a must-fix comment, skip minor style notes on the same sentence unless they affect submission quality.
- Default to at most one nice-to-have comment per paragraph.
- If a paragraph already has two comments, add another only when it is clearly must-fix.
- When several nearby issues share one root cause, write one consolidated local comment instead of multiple near-duplicate comments.

## Preprint Configuration Pattern

For the `hfut.cls`-style workflow, the review layout has two layers, both centered on `preprint`.

### 1. Class-file layer

Use `changes` and `todonotes` from `hfut.cls`, not from the chapter file. Patch the `preprint` branch directly.

Representative pattern:

```latex
\ifdefstring{\HFUT@mode}{preprint}{
    \RequirePackage[mathlines]{lineno}
    \linenumbers
    \RequirePackage[xcolor=dvipdf,markup=default,todonotes={textsize=scriptsize,textwidth=3.1cm,color=cyan!12,linecolor=cyan!45!black,bordercolor=cyan!45!black}]{changes}
    \setcommentmarkup{\todo{\arabic{authorcommentcount}. #1}}
    \geometry{paperwidth=22.2cm,paperheight=29.7cm}
}
```

Also keep the margin-note helper in the class file, for example:

```latex
\newcommand{\HFUT@preprintlayout}{%
    \setlength{\marginparwidth}{4cm}%
    \setlength{\marginparsep}{8pt}%
    \addtolength{\textwidth}{-1.2cm}%
}
\HFUT@preprintlayout
\AtBeginDocument{\apptocmd{\newgeometry}{\HFUT@preprintlayout}{}{}}
```

Important:

- Keep using `preprint` for annotated output unless the project already has a different review mode in active use.
- If project pages use `\tikz` directly, ensure `tikz` is explicitly loaded in the class file.
- If the project has an established comment-numbering style such as `1. ...`, preserve it in `\setcommentmarkup` instead of switching to bracketed numbering.
- If review output needs wider paper, prefer setting `paperwidth` and `paperheight` through `\geometry{...}` in the class-file review branch. Do not rely on `\newgeometry` to change paper size, because `geometry` will ignore those keys there.

### 2. Main-file page-width layer

If the user wants the body-text width to remain roughly unchanged while still making room for side `todo` boxes, do not merely shrink `\textwidth`. Instead, expand the physical page width to the right in `Thesis.tex`.

Representative pattern used in this project:

```latex
\newgeometry{left=3cm, right=4.2cm, top=2.54cm, bottom=2.54cm}
...
\newgeometry{left=2.8cm, right=4cm, top=3.14cm, bottom=3.14cm}
```

Interpretation:

- Standard A4 width is `21.0cm`
- Review width here is `22.2cm`
- The extra `1.2cm` is added only on the right side
- This compensates for the class-file review layout reduction and gives `todo` comments actual page space

Use this approach only for review PDFs. It is not a final-submission layout.

## Comment Style Policy

- Default to `\comment{...}` only.
- Use concise, direct mentor-style comments.
- Prefix comments with issue labels when appropriate. Load [references/review-checklist.md](references/review-checklist.md).
- Do not assume an author id such as `Advisor` unless the repository already uses one or the user asks for it.

## First-Page Summary Report

The annotated review PDF should start with a concise review summary page before the thesis cover or first original page. This is a review artifact only; do not include it in a final submission PDF unless the user explicitly asks.

Default implementation:

- Create or update `review-summary.tex` next to `Thesis.tex`.
- Input it immediately after `\begin{document}` and before the original thesis front matter, guarded by the review/preprint mode when the project supports such a mode.
- Keep the summary to one page whenever possible.
- Summarize the highest-priority issues found during the review: overall judgment, structure/depth, formula/notation, citations, figures/tables, writing/format, and next actions.
- Do not let the summary replace local `\comment{...}` annotations; it is an executive summary of the same review.

Use [references/summary-report.md](references/summary-report.md) for the exact content structure, LaTeX insertion pattern, and verification steps.

## Text Review Priorities

Apply this order unless the user narrows the scope:

1. Whole-thesis structure, chapter balance, and undergraduate-thesis completeness
2. Missing expected content in each chapter or section
3. Formula, notation, table, and figure conventions
4. Missing citations for factual or literature-summary statements
5. First-use abbreviation expansion
6. Author surname and bibliography key consistency
7. Terminology consistency
8. Chinese grammar and readability
9. Redundancy and paragraph logic

Load [references/review-checklist.md](references/review-checklist.md) for local issue labels and [references/thesis-standards.md](references/thesis-standards.md) for broader undergraduate thesis requirements.

## Structure And Depth Inspection

Do not begin and end with sentence-level language polishing. For full theses and for chapters whose role can be inferred, check whether the work would pass an undergraduate "合格性" review:

- The title, abstract, introduction, chapter arrangement, experiments or design work, and conclusion must describe the same actual project.
- A chapter with only a few paragraphs, only definitions, only pasted background, or only result tables without analysis is structurally weak even if individual sentences are grammatical.
- Method or system-design chapters need an overall pipeline, module responsibilities, key variables or components, and design rationale.
- Experiment or implementation chapters need data/source material, environment or settings, baseline or comparison objects when relevant, metrics, result interpretation, and limitations or error analysis when improvement claims are made.
- Conclusion must not merely repeat the introduction; it should summarize completed work, main findings, limitations, and future work.

Use [references/structure-depth-checklist.md](references/structure-depth-checklist.md) for the detailed audit procedure and local comment anchors.

## Formula And Notation Inspection

Formula review is mandatory when math appears, including loss functions, metrics, transformations, algorithm definitions, model modules, statistical quantities, and evaluation formulas.

Check:

- whether the formula is introduced before or near the display,
- whether each important symbol is defined at first use,
- whether equation numbering and `\label` / `\ref` / `\eqref` usage are consistent,
- whether notation, subscripts, dimensions, and units stay consistent across chapters,
- whether the surrounding sentence punctuation and interpretation make the formula part of the prose,
- whether long formulas are broken at appropriate relation or operator symbols.

Use [references/formula-checklist.md](references/formula-checklist.md) when formulas or math-heavy prose are present.

## Figure And Plot Inspection

Do not stop at the LaTeX wrapper. If a chapter contains figures, plots, screenshots, or result charts:

1. Find the referenced asset path from `\includegraphics`, TikZ, pgfplots, or generated outputs.
2. Open the actual image file when possible.
3. Check:
   - x-axis and y-axis labels
   - legend text
   - units
   - label language consistency with the body text
   - readability after printing
   - clipping, blur, stretching, and cropping
   - whether method names and class names match the body text
4. Also check the LaTeX wrapper:
   - `\caption{}`
   - `\label{}`
   - subfigure ordering
   - reference order in the body text

Load [references/figure-content-checklist.md](references/figure-content-checklist.md) when figures are present.

## Undergraduate Thesis Norms

Do not only check sentence-level language. Also check whether the chapter satisfies the usual bar for an undergraduate thesis:

- whether the section has the content it is expected to contain,
- whether the structure is complete enough for a student thesis,
- whether formulas, tables, and figures are introduced and explained,
- whether experiments are described with enough information for a reader to understand what was compared and how,
- whether the conclusion summarizes work, limitations, and possible future work rather than only repeating claims.

For these broader checks, load [references/thesis-standards.md](references/thesis-standards.md), [references/structure-depth-checklist.md](references/structure-depth-checklist.md), and [references/formula-checklist.md](references/formula-checklist.md) when math is present.

## Editing Constraints

- Preserve the student's structure unless the user explicitly allows broader intervention.
- Do not silently rewrite content that is merely stylistic.
- Prefer comments over direct correction unless the user asks for direct revision markup.
- If side comments become too dense on one page, shorten or drop only the lowest-priority comments, not the whole review standard.
- When the user wants the prior real workflow preserved, follow the established `preprint + changes + todo side box + widened paper width` approach rather than inventing a new markup system.

## Compile And Verify

After meaningful review edits, compile with:

```bash
latexmk -xelatex -outdir=tmp Thesis.tex
```

Then verify:

- PDF builds successfully
- comments render when compilation succeeds and the user wants render checking
- the first page of the review PDF is the review summary report
- local comments still sit near the intended issue when you do inspect the rendered pages
- widened paper size and right-side review area are still active
- no new hard LaTeX errors were introduced

Warnings such as `Marginpar moved` are common with side comments. Treat them as a practical rendering issue only if they materially hide or detach comments from the intended page context.

If the user explicitly says PDF rendering is not necessary, stop after successful compilation unless there is evidence of layout failure from the log.
