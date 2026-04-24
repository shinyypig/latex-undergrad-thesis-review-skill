# Figure Content Checklist

Inspect the actual image file whenever possible, not only the LaTeX code.

## Axes, legends, and text

- Check whether x-axis and y-axis labels are present and readable.
- Check whether axis labels use consistent language with the thesis body.
- Check whether labels should be English or Chinese according to the surrounding chapter convention; flag mixed-language labels when they look accidental.
- Check whether units are present where required.
- Check whether legend entries are readable, non-overlapping, and consistent with the body-text terminology.
- Check whether font sizes are too small to survive printing.

## Semantic consistency

- Check whether the figure caption matches what the image actually shows.
- Check whether class names, method names, and abbreviations in the figure match the body text.
- Check whether subfigure labels `(a) (b) ...` match the order described in the text.
- Check whether metric names in plots or tables match the evaluation section.

## Visual quality

- Check cropping, stretching, low resolution, blurry screenshots, and clipped labels.
- Check whether curves, bars, markers, or color legends can be distinguished in grayscale printing if that matters for a thesis submission.
- Check whether whitespace or margins are excessive.

## LaTeX wrapper checks

- Check whether `\label{}` uses ASCII, concise names, and no Chinese characters or spaces.
- Check whether `\caption{}` is specific enough and consistent with nearby references.
- Check whether the figure is referenced in the body text before or near the figure's appearance.
- Check whether subfigure widths, alignment, and spacing are balanced.

## Comment Placement

- Do not insert `\comment{...}` inside `figure`, `table`, `tabular`, `adjustbox`, `caption`, or subfigure internals.
- Anchor figure/table comments in nearby normal prose, preferably the sentence that introduces, references, or interprets the figure/table.
- If no such prose exists, place one comment immediately before or after the floating environment and make the missing introduction/interpretation explicit.
