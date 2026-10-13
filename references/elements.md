# Figure elements: type, axes, labels, symbols, arrows

Bracketed numbers are column numbers (see `sources.md`). "(inference)" and
"Extension:" mark what the sources don't state. Point values (pt) assume the
figure is placed at 100% of its final printed size.

## 1. Typography [16, 18, R3]

- Use **one typeface**, "no more than two or three type sizes, with
  judicious use of bold and italics if necessary". [16]
- Labels: "one typeface of fixed size", aligned to support grouping. [18]
- "Sans serif fonts work well for slides and serif fonts for posters and
  printed documents"; serif eases multiline reading, sans serif suits short
  bursts such as labels and headings. [16] Figure labels are short bursts,
  so sans serif is the usual choice even in print (inference); match the
  journal's figure font if it specifies one.
- Space by meaning: paragraph spacing larger than line spacing; list items
  close together but set apart from surrounding text. Use space-before/after
  settings, not blank lines. [16 gives 5 pt after paragraphs, 3 pt after
  bullets as an example.]
- Typography must draw attention before it is read without interfering with
  reading. [16] Be legible without shouting. [09] In a crowded layout,
  whitespace beats bold or caps for emphasis. [04, 07]
- No vertical text in talks. [R3] In papers, keep the y label as the only
  rotated text (inference).
- Capitalization, singular/plural, acronyms: pick one convention (journal or
  field) and apply it everywhere. [18]
- Extension (mapping to matplotlib): typical sizes are tick labels, axis
  labels and panel letters. Set them as two or three sizes in rcParams.

## 2. Axes [17]

- Axes, ticks and grids are **navigation**. Make them distinct from the data
  and unobtrusive (thinner, lighter, more transparent), so the data keep
  visual priority. [17]
- Axis weight: "0.5 pt is sufficient". [17]
- Don't box the plot with axes on all four sides "unless the figure is
  particularly large". [17] (Hiding the top and right spines is the usual
  way to do this; inference.)
- **No arrows on axes**: "their orientation is almost never in doubt". [17]
- Layer different kinds of lines by weight and style: axes, contours, fits
  and boundaries should not all share one line style. [17 Fig. 1]
- Rougier's tuned example moves the spines to zero where zero is meaningful.
  [R Fig. 4]

## 3. Ticks and tick labels [17, R]

- Densely labelled ticks add repetition. Use few ticks. [17, R Fig. 7]
- Remove repeated non-significant digits **by adjusting the units**. In
  [17] Fig. 2b, labels like 12,000, 12,200, …, 13,400 bp are relabelled to
  show kb at the major positions and only the hundreds in between
  (paraphrase of the figure).
- Spectroscopy mapping (inference): "7110 7112 7114 eV" → energy relative to
  a stated reference (E − E₀, or energy loss), or matplotlib's offset
  notation, with the reference named in the axis label.
- Override library tick defaults on purpose: too many ticks, three-decimal
  labels. [R5, R Fig. 7]

## 4. Grids [17, 21, 10, R8]

- "No grid may be better than a badly chosen one—use a grid when needed
  rather than by default." [17] Grid lines "if necessary", of less weight
  than the axes. [21] Light treatment of axes and grids keeps focus on the
  data. [10] Useless grid lines are chartjunk. [R8]
- When to use one (inference from [17, 21]): when readers must compare
  values across distant points, or read approximate values, and tick marks
  alone are not enough.
- **Opacity**: "use 15% as the minimum grid opacity. Maximum opacity should
  be 25%–45%, in proportion to the figure's data density." The effective
  range is 15-45%. [17 Fig. 3b] Sparse data → near 15%; dense data → 25-45%
  (reading of [17] Fig. 3b).
- Dark enough to survive LCD projectors, which wash out light colors, but
  not "a fence in front of data". [17]
- **Density**: grid spacing sets the scale at which readers judge
  differences. A dense grid implies small fluctuations matter and
  uncertainty is low. Don't send that message falsely. Denser grids also
  increase judgment error. [17 Fig. 3a]
- Grids go behind the data (inference; consistent with "fence in front of
  data" [17]).

## 5. Scales across panels [17, 24, 36]

- In multipanel figures, keep scales fixed where possible and show a shared
  scale with a single y axis. Changes in axis range across panels are easily
  overlooked. [17 Fig. 2a]
- Use a common scale across small multiples so they can be compared
  directly. [36]
- When ranges differ, per-panel scaling is allowed, but "any adjustment to
  scale ranges needs to be clearly presented". [24] Options: see
  `plot-types.md` §5.
- Outliers should not compress the range of the bulk of the data. An axis
  break is an option, but follow journal policy and remember breaks can
  hide patterns [17] and distort perceived absolute differences [24].

## 6. Labels and callouts [18]

- "Labels are annotations and thus are subordinate to their data points,
  not to other labels." In scatter plots, don't align labels with each
  other. [18]
- Place data labels at a **consistent offset and alignment** relative to
  their points. When the fixed position collides, fall back to a fixed
  priority order of alternative positions. [18 Fig. 1]
- Keep labels concise. Move text shared by all labels into the legend, axis
  label or panel header. [18, 27] Don't encode the same information twice
  (e.g. species by both color and code). [18, 26]
- In trees, lists and schematics, align label components in columns,
  optionally joined by dotted tab leaders. [18 Fig. 2c]
- **Callout lines**: prefer horizontal. If angled lines are needed, use one
  fixed angle, **30° or 45°**. Limit variation in length. End the lines
  consistently at the element's edge. [18]
- **No bubbles, bursts or other "visual trinkets".** [18]
- "Variety should be informed by data, not formatting." [18]
- "Space saved at the expense of clarity is not a good bargain." [18]
- Make points of interest visually distinct and point them out again in the
  caption. [R4]

## 7. Legends vs direct labels [19, R Fig. 7, 18, 26]

No source bans legends. The guidance is to **reduce legend lookups**:
- Rougier's redesign labels each series at the left of its own panel, with
  no legend box. [R Fig. 7]
- Single-letter symbols can remove legend lookups if the letters are
  distinct (avoid C/G, B/R/P, E/F/H). [19]
- Legends are still right for shared text and keys: [18] moves common text
  *into* the legend, and [26]'s redesign gains "a clear legend".
- Default (inference): with few curves that are easy to label, label them
  directly at the line ends or near a distinctive feature, in the line's
  color. Otherwise use a plain legend (no frame, shadow or fancy box) that
  doesn't sit on the data. [R Fig. 7 shows a legend over the data as a
  fault.]

## 8. Plotting symbols [19]

- One category, dense data: **open circles**. Overlapping circles don't form
  new circles (unlike squares, triangles and diamonds), and overlapping open
  symbols build up ink density, "a practical substitute for density maps".
- Several categories: use distinct symbols that form strong visual
  boundaries. Sets made only of polygons (triangles, diamonds, squares,
  pentagons) "blend and lack distinctiveness". A strong set combines open
  circle, plus, open square, filled circles and similar shapes. [19 Fig. 2a]
- Symbols should look the same size and complexity. A five-pointed star
  draws extra attention and gives its category undue importance.
- High density in black and white: use highly distinct "texture" symbols
  (open circle, +, ×-like shapes). Low overlap: vary the fill (open, filled,
  half).
- Encode the data's hierarchy: give relevant states more weight (fill and/or
  color). Use less prominent symbols for reference or context data.
- Color discriminates well, but salience drops as the number of hues grows.
- More than six or seven categories: "consider presenting the data in
  several panels with each showing a few data categories" (small
  multiples).
- Shapes encode a categorical dimension only when there are few categories.
  [32]

## 9. Arrows [20, 02, 25]

- Arrows are the "verbs" of visual communication. Readers read them as
  change, movement or causality. Use them for **direction, sequence, change
  or causality** only, not to point at things. [20]
- Show structural or spatial relationships with plain lines. [20]
- **Leaders** (lines to labelled parts): no head, or only a bullet (a small
  ball or open circle). [20, 02] Exception: the familiar arrowhead marking
  features in micrographs and other images. [20]
- **Proportion for print**: stem **0.75 pt**, arrowhead scaled to **60%**.
  The 60% is an Adobe Illustrator scaling setting with no direct matplotlib
  equivalent. [20 Fig. 2c]
- Avoid open "V on a stick" and swept-wing heads. Trapped whitespace makes a
  "sparkle" that adds noise. [20] Use plain solid heads; no stylized or
  stretched arrows. [25]
- Treat a set of arrows as one wireframe: no sharply opposing directions,
  similar directions for natural flow, and whitespace at the arrow ends.
  [20]
- Diagram edges in [25]: 0.5-pt lines with equilateral-triangle arrowheads
  of 2.5-pt sides.
- One meaning per symbol. Don't use the same arrow for beam path, motion and
  labelling. [02, 20 Fig. 1c]
- Spectroscopy mapping (inference): arrows for a peak shifting with
  temperature, dose or delay, or for scan direction. Headless leaders for
  peak labels.
