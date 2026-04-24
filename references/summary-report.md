# First-Page Review Summary Report

Use this when producing an annotated undergraduate thesis review PDF.

## Purpose

The review PDF should begin with a one-page mentor-style summary report. It gives the student and advisor a quick view of the most important problems before they read the inline comments.

This page is a review artifact only. Do not include it in a final submission PDF unless the user explicitly asks.

## Content Structure

Keep the report concise. Prefer these sections:

- `总体判断`: one sentence such as "需要重点修改后再定稿" or "局部修改后可进入格式检查".
- `评阅范围`: full thesis, selected chapters, or specific files reviewed.
- `主要问题`: 3-6 high-priority bullets, ordered by risk.
- `结构与内容`: chapter balance, missing expected sections, thin analysis, abstract/body/conclusion mismatch.
- `公式与图表`: undefined symbols, weak formula explanations, figure/table readability, result interpretation.
- `引用与规范`: missing citations, bibliography mismatch, terminology, labels, formatting.
- `优先修改建议`: concrete next actions, not generic encouragement.

Do not list every inline comment. The summary should synthesize the review.

## LaTeX File Pattern

Create `review-summary.tex` next to `Thesis.tex` unless the project already has a review folder convention.

Representative content:

```latex
\begingroup
\thispagestyle{empty}
\newgeometry{left=2.5cm,right=2.5cm,top=2.3cm,bottom=2.3cm}
\section*{本科毕业论文评阅汇总报告}

\noindent\textbf{总体判断：} 需要重点修改后再定稿。

\vspace{0.6em}
\noindent\textbf{评阅范围：} 全文结构、章节内容、公式图表、引用规范和语言表达。

\vspace{0.6em}
\noindent\textbf{主要问题：}
\begin{enumerate}
  \item 绪论或相关工作尚未充分收束到本文具体问题，研究目标和主要工作需要更明确。
  \item 方法或实验章节存在内容偏薄的问题，需要补充关键模块、数据来源、实验设置和结果解释。
  \item 部分公式缺少符号定义或正文解释，建议统一记号并补充公式用途说明。
\end{enumerate}

\vspace{0.6em}
\noindent\textbf{优先修改建议：}
\begin{enumerate}
  \item 先补齐结构性缺口，再处理局部语句润色。
  \item 逐章核对公式、图表、引用和术语是否与正文一致。
  \item 修改后重新编译并检查侧边批注位置和第一页汇总报告。
\end{enumerate}

\restoregeometry
\clearpage
\endgroup
```

Adjust the actual bullets to the thesis being reviewed. Do not leave placeholder text.

## Insertion Pattern

Insert the summary immediately after `\begin{document}` and before the original thesis cover/front matter.

For the common `hfut.cls` preprint workflow, guard it with review mode:

```latex
\ifdefstring{\HFUT@mode}{preprint}{%
  \input{review-summary.tex}
}{}
```

If the project uses another explicit review mode, adapt the guard to that mode. If there is no reliable mode flag, prefer creating a separate review entry file or ask before modifying the main submission path.

## Page Numbering

- Use `\thispagestyle{empty}` for the summary page by default.
- Keep the original thesis page-numbering commands intact.
- If inserting the page shifts the thesis numbering unexpectedly, restore the original numbering behavior immediately after the summary or before the original front matter.

## Verification

After compiling:

- Confirm the first PDF page title is `本科毕业论文评阅汇总报告`.
- Confirm the original thesis cover or original first page starts after the summary page.
- Confirm the summary is review-only and does not appear in non-review/final-submission mode.
- Confirm local side comments still render near their intended text.
- If delivery is requested, copy the compiled review PDF to `Thesis-review.pdf`; do not overwrite the original submission `Thesis.pdf` unless explicitly requested.
