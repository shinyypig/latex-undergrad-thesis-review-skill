# Undergraduate Thesis Review Checklist

Use these labels at the start of each comment when applicable. The labels themselves remain in Chinese because they are intended to appear in thesis review markup; keep the surrounding skill text in English.

- `【缩写】` First use of an abbreviation lacks Chinese full name + English full name + abbreviation.
- `【语病】` Chinese grammar, collocation, missing structural particle, or sentence-readability problem.
- `【引用】` Factual or literature-summary statement lacks citation.
- `【核查】` Author surname in the prose may not match the cited bibliography entry or key naming.
- `【术语】` Same concept uses inconsistent terms across nearby text or across the thesis.
- `【结构】` Chapter, section, or whole-thesis organization is incomplete, imbalanced, or not aligned with the title/abstract.
- `【内容】` Expected substantive material is missing, too thin, or only listed without explanation.
- `【公式】` Formula, symbol, notation, numbering, unit, or equation-reference problem.
- `【图表】` Figure/table caption, label, numbering, reference order, readability, or content-consistency problem.
- `【格式】` Formatting, label, numbering, punctuation, unit, or template-compliance problem.
- `【重复】` Nearby sentences or paragraphs repeat the same core point.
- `【建议】` Optional improvement that is not a hard correctness issue.

## Priority Mapping

### Must-fix or must-verify

- `【缩写】`
- `【语病】`
- `【引用】`
- `【核查】`
- `【结构】`
- `【内容】`
- `【公式】`
- `【图表】`
- `【格式】`

### Nice-to-have optimization

- `【术语】`
- `【重复】`
- `【建议】`

If a paragraph already contains one must-fix comment, add nice-to-have comments only when they are unusually valuable.

## Sentence-level checks

- Ask whether each factual statement needs `\supercite{}`.
- Check whether each literature-summary statement of the form "X et al. propose..." or "studies show..." is cited.
- Check whether each long Chinese sentence should be split for readability.
- Check whether the subject, predicate, and object are complete and compatible.
- Check whether unsupported evaluative wording such as "significantly improves", "clearly outperforms", or "works well" needs evidence or softer wording.

## First-mention abbreviation checks

Require explicit expansion at first mention for common items such as:

- FCN, FPN, CNN, IoU, Dice, BN, GN, ReLU, ASPP
- model names or modules whose English meaning is not obvious to a student reader

Expected pattern:

- Chinese full name (English Full Name, ABBR)

## Bibliography-name checks

- When prose says `Zhang et al.`, verify the cited entry's first author is actually Zhang.
- Watch especially for keys containing person-like strings such as `liu2025...`, `lei2025...`, `wang2024...`.
- If the prose surname and key naming logic differ, leave a `【核查】` comment even if the entry may still be technically correct.

## Terminology checks

- Use one preferred term for the same concept after first mention.
- If two near-synonyms appear, prefer the one already established earlier in the thesis.
- Flag inconsistent naming when the same object, task, dataset, module, method, metric, or process is referred to by multiple expressions.

## Formula, Table, And Figure Checks

- Check whether formulas are introduced and interpreted in the surrounding text.
- Check whether key symbols or variables are explained near first use.
- Check whether equation numbers, labels, and in-text references match.
- Check whether notation, units, dimensions, and metric names are consistent across chapters.
- Check whether tables and figures are referenced in the body text before or near appearance.
- Check whether captions are specific enough to stand on their own.
- Check whether labels use ASCII, concise names, and no Chinese characters or spaces.

## Structure And Depth Checks

- Check whether the title, abstract, chapter headings, methods, experiments or design work, and conclusion describe the same actual project.
- Check whether each chapter has enough substantive content for its role; do not rely only on sentence-level fluency.
- Check whether introduction chapters contain background, significance, research objective, method or workflow preview, and chapter arrangement.
- Check whether method/design chapters contain a pipeline, module responsibilities, key variables or components, and design rationale.
- Check whether experiment/implementation chapters contain data/source material, environment, settings, baselines or comparison objects, metrics, result interpretation, and limitations/error analysis when relevant.
- Check whether conclusion chapters summarize completed work, main findings, limitations, and future work.

## Experiment And Result Checks

- Check whether data source, settings, metrics, and comparison objects are stated.
- Check whether result paragraphs interpret the numbers instead of merely repeating the table.
- Check whether claimed improvements are supported by the displayed results.

## Conclusion Checks

- Check whether the conclusion summarizes actual completed work instead of restating the introduction only.
- Check whether limitations or future work are mentioned when the thesis makes improvement claims.

## Undergraduate thesis bar

- Prefer clear, teachable, compliant expressions.
- Do not demand journal-level compression or stylistic sophistication.
- Do flag unsupported claims, confusing wording, and inconsistent naming.
