# Formula And Notation Checklist

Use this whenever the thesis contains display equations, important inline symbols, loss functions, metrics, transformations, algorithms, model definitions, or statistical quantities.

## Discovery

Search for common LaTeX math constructs:

```bash
rg -n "\\\\begin\\{(equation|align|gather|multline|split|cases)\\}|\\\\\\[|\\$\\$|\\\\label\\{eq:|\\\\eqref\\{|\\\\ref\\{" .
```

Also inspect algorithm environments, metric definitions, table headers, figure axes, and prose around model/loss/evaluation descriptions.

## Required Formula Checks

- The formula is introduced before or near the display; the reader should know why it appears.
- Important variables, symbols, subscripts, superscripts, operators, and parameters are defined at first use.
- The surrounding prose interprets the formula rather than leaving it as an isolated display.
- Formula punctuation fits the sentence: commas, periods, and explanatory clauses should make the equation part of the text.
- Numbering follows the template or school rule; when many formulas exist, chapter-based numbering may be expected.
- Numbered equations that are discussed later have stable labels and are referenced with `\eqref` or the project's preferred style.
- Labels are ASCII, concise, and consistent, usually with an `eq:` prefix when the project uses prefixes.
- Long formulas break at relation or operator symbols such as `=`, `\approx`, `<`, `>`, `+`, `-`, `\times`, or `/`.
- Units and dimensions are consistent; variables in formulas agree with table metrics, figure axes, and text descriptions.
- Notation stays consistent across chapters: do not use the same symbol for different concepts or different symbols for the same concept without explanation.

## Common Problems To Comment On

- Formula appears without a lead-in sentence.
- A loss/metric/model formula defines only part of the notation.
- Formula uses symbols that differ from a nearby figure, table, algorithm, or implementation description.
- Equation is numbered but never referenced, or prose references a formula without a label.
- The same equation is repeated across chapters without explanation.
- A result claim depends on a metric formula that has not been defined.
- A denominator, normalization term, index range, or summation set is unclear.
- Units are missing or incompatible with the variables described in text.
- Formula formatting causes overfull lines, broken alignment, or hard-to-read multi-line equations.

## Comment Labels

Use `【公式】` for math-specific issues.

Typical comments:

- `【公式】该公式出现前缺少引入说明，建议先交代该式用于计算什么指标或描述哪个模块。`
- `【公式】式中符号尚未完整定义，建议补充每个变量、下标和参数的含义。`
- `【公式】这里编号了公式但正文未引用，建议补充引用说明，或按模板要求取消编号。`
- `【公式】该符号与前文表述不一致，建议统一记号，避免读者误认为是不同变量。`

## Placement

- For a missing lead-in, place `\comment{...}` after the sentence immediately before the formula or at the start of the formula's surrounding paragraph.
- For undefined symbols, place the comment after the formula or after the incomplete symbol definition sentence.
- For reference/numbering issues, place the comment near the `\label`, `\eqref`, or the sentence that should reference the equation.
- Avoid inserting comments inside `equation`, `align`, `gather`, `split`, `cases`, `array`, or other math environments unless the project's review markup is known to compile safely there.
- If a formula environment itself is fragile, anchor the comment in the lead-in sentence or immediately after the display environment in normal prose.
