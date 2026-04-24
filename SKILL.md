---
name: latex-undergrad-thesis-review
description: Review and annotate undergraduate LaTeX theses, especially Chinese graduation theses built on custom class files such as hfut.cls. Use for whole-thesis or chapter-level review, structure/depth audit, formula/notation checks, citation and bibliography hygiene, figure/table review, mentor-style changes comments, first-page review summaries, and review-only preprint layouts with right-side todo comments.
---

# LaTeX Undergrad Thesis Review

Review as an undergraduate thesis, not as a journal paper. Prioritize completeness, format compliance, chapter depth, supported claims, formula/notation clarity, figure/table readability, citation hygiene, terminology consistency, and clear academic Chinese.

## Token Economy Rules

Use a scan-first workflow. Do not read every file or every reference by default.

1. First identify scope and project shape with cheap commands:
   - `rg --files`
   - `wc -l Thesis.tex tex/*.tex ref.bib`
   - `rg -n "\\\\(section|subsection|subsubsection)\\{|\\\\includegraphics|\\\\caption\\{|\\\\label\\{|\\\\cite|\\\\begin\\{equation|\\\\begin\\{align|\\\\\\[" Thesis.tex tex/*.tex`
   - `rg -n "changes|todonotes|HFUT@mode|preprint|newgeometry|comment" hfut.cls Thesis.tex tex/*.tex`
2. Read only the main file, class-file review branch, abstract/info, and target chapters needed for the user request.
3. Load reference files only when triggered:
   - full thesis or chapter-completeness review: `references/structure-depth-checklist.md`
   - formulas/math/metrics/loss/model definitions found: `references/formula-checklist.md`
   - figures/plots/screenshots found and content inspection is needed: `references/figure-content-checklist.md`
   - local issue labels needed: `references/review-checklist.md`
   - first-page summary generation: `references/summary-report.md`
   - standards are unclear: `references/thesis-standards.md`
4. Summarize findings internally; do not paste long source excerpts into the response.
5. Default comment density:
   - full thesis first pass: about 20-35 high-signal comments,
   - single chapter: about 6-12 comments,
   - if one issue pattern repeats, comment the first 1-2 representative locations and mention the pattern in the summary.

## Default Output Mode

Unless the user asks otherwise:

- Use `changes` comments: `\comment{...}` only.
- Use side `todo` comment boxes, not footnotes.
- Keep review setup in `hfut.cls` when that class controls review packages.
- Use the existing review mode if present; for `hfut.cls`, use `mode=preprint`.
- Insert a review-only first-page summary report before the original thesis front matter.
- Keep the body text width roughly unchanged by widening the review PDF to the right.
- Preserve the student's structure and wording; prefer comments over direct rewriting.

## Minimal Workflow

1. Determine scope: full thesis, selected chapter, or specific issue type.
2. Scan project structure, class review setup, headings, formulas, figures/tables, citations, and bibliography.
3. Build a compact thesis map: title/abstract, chapters, balance, figures/tables/equations, experiment/result/conclusion coverage.
4. Audit structure before sentence polish:
   - title, abstract, body, experiments/design, and conclusion describe the same work,
   - chapters contain enough substance for their role,
   - method/system chapters explain pipeline, modules, inputs/outputs, formulas or rationale,
   - experiment/implementation chapters explain data, settings, baselines, metrics, results, analysis, limitations,
   - conclusion summarizes completed work, findings, limitations, and future work.
5. Read target `.tex` files and inspect only relevant image assets.
6. Insert concise `\comment{...}` at exact problem locations.
7. Create/update `review-summary.tex`.
8. Compile and fix review-introduced errors.
9. Deliver the annotated PDF path and the main issue summary.

## Comment Priorities

Must comment by default:

- missing citations for factual or literature-summary claims,
- first-use abbreviations without Chinese full name + English full name + abbreviation,
- materially confusing grammar,
- author-name/bibliography-key mismatch,
- non-ASCII or broken labels when the project expects ASCII labels,
- figure/table/formula issues that block interpretation,
- missing formula explanation, undefined symbols, inconsistent notation, or unreferenced numbered equations,
- structurally thin sections/chapters,
- unsupported strong claims in results or conclusion.

Comment sparingly:

- mild wording polish,
- minor terminology cleanup,
- repetition that does not affect correctness,
- optional caption tightening,
- purely stylistic preferences.

Use Chinese issue labels such as `【结构】`, `【内容】`, `【公式】`, `【图表】`, `【引用】`, `【缩写】`, `【核查】`, `【格式】`. Load `references/review-checklist.md` if unsure.

## Placement Rules

Every `\comment` must be attached to the exact problem location.

- Sentence issue: after the sentence-ending punctuation.
- Term/abbreviation/key/label/caption issue: immediately after the problematic phrase when safe.
- Formula issue: after the display equation or after the sentence defining the symbols. Avoid putting comments inside math environments.
- Structure issue: at the relevant heading, opening paragraph, or missing-content boundary.
- Figure/table issue: anchor in surrounding body text, preferably where the figure/table is introduced or interpreted.

Hard rule: do not put `\comment` inside `figure`, `table`, `tabular`, `adjustbox`, `caption`, `equation`, `align`, `cases`, or other fragile/floating environments unless the project already proves this compiles. If a table/figure itself has a problem, place the comment before or after the environment in normal prose. This avoids `Float(s) lost` and fragile-command failures.

## Review Layout For `hfut.cls`

For the common `hfut.cls` workflow, patch the `preprint` branch rather than adding a new mode.

Class layer pattern:

```latex
\ifdefstring{\HFUT@mode}{preprint}{
    \RequirePackage[mathlines]{lineno}
    \linenumbers
    \RequirePackage[xcolor=dvipdf,markup=default,todonotes={textsize=scriptsize,textwidth=3.1cm,color=cyan!12,linecolor=cyan!45!black,bordercolor=cyan!45!black}]{changes}
    \setcommentmarkup{\todo{\arabic{authorcommentcount}. #1}}
    \geometry{paperwidth=22.2cm,paperheight=29.7cm}
    \newcommand{\HFUT@preprintlayout}{%
        \setlength{\marginparwidth}{4cm}%
        \setlength{\marginparsep}{8pt}%
        \addtolength{\textwidth}{-1.2cm}%
    }
    \AtBeginDocument{%
        \HFUT@preprintlayout
        \apptocmd{\newgeometry}{\HFUT@preprintlayout}{}{}%
    }
}
```

Main-file review width pattern:

```latex
\documentclass[mode=preprint,font=adobe]{hfut}
...
\begin{document}
\makeatletter
\ifdefstring{\HFUT@mode}{preprint}{%
  \input{review-summary.tex}
}{}
\makeatother
\newgeometry{left=3cm, right=4.2cm, top=2.54cm, bottom=2.54cm}
...
\newgeometry{left=2.8cm, right=4cm, top=3.14cm, bottom=3.14cm}
```

Notes:

- Do not rely on `\newgeometry` to change paper size; set `paperwidth/paperheight` through `\geometry{...}` in the class review branch.
- Preserve an existing comment-numbering style when present.
- If project pages use direct TikZ, ensure the needed TikZ package is loaded by the class or preamble.
- The widened layout is review-only, not final submission layout.

## First-Page Summary

Create `review-summary.tex` next to `Thesis.tex` unless the project has a convention. Keep it to one page when possible. Summarize only top risks:

- overall judgment,
- review scope,
- 3-6 major issues,
- structure/content,
- formulas/figures,
- citations/format,
- priority next actions.

Load `references/summary-report.md` only before writing the summary.

## Compile And Verify

Compile after meaningful edits:

```bash
latexmk -xelatex -outdir=tmp Thesis.tex
```

`latexmk` may run `biber` for `biblatex`; let it do so. If stale root-level aux files confuse the run, clean generated aux files carefully, never source files.

Verification checklist:

- `tmp/Thesis.pdf` builds successfully,
- first page is the review summary,
- comments render in side boxes,
- right-side widened review area is active,
- no hard LaTeX errors remain.

Common warnings such as `Marginpar moved` are acceptable unless comments are detached or unreadable. If compilation fails after adding comments, first check whether a `\comment` was placed in a float, table, caption, math, or other fragile environment.

## Deliverables

If compiling succeeds, keep `tmp/Thesis.pdf` and also copy it to `Thesis-review.pdf` unless the user asks for a different name. Do not overwrite the original final-submission `Thesis.pdf` unless explicitly requested.

In the final response, report:

- files changed,
- number and scope of comments,
- PDF path,
- compile command result,
- any remaining warnings or limitations.
