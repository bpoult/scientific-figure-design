---
name: scientific-figure-design
description: >-
  Design METHOD and review rubric for publication-ready scientific figures,
  grounded in the Nature Methods "Points of View" columns (Wong, Krzywinski,
  Gehlenborg, Streit et al., 2010-2016) and Rougier et al. 2014 "Ten Simple
  Rules for Better Figures". Read and follow this BEFORE designing, building,
  revising or critiquing any figure meant for a paper, poster or talk. Use it
  together with python-plotting-style (house style); for publication and
  poster figures it overrides five named house defaults. Triggers on:
  publication figure, paper figure, manuscript/journal/submission figure,
  "figure for the paper", "make this publication ready", "clean up this
  figure", poster figure, talk or slide figure, multi-panel or composite
  figure, panel layout/arrangement, figure review, figure critique, "what's
  wrong with this plot", reviewer comments on figures, choosing a plot type or
  chart type, bar vs box plot, overlay vs small multiples vs waterfall/offset
  plot, colormap choice, color palette, colorblind-safe colors, heat map
  design, legend vs direct labels, axis/tick/grid styling, figure caption,
  schematic, overview or setup diagram, graphical abstract. Supplies an
  8-step design process, a publication checklist, and references on
  perception, color, figure elements, plot types, workflow, matplotlib
  recipes and sources.
---

# Scientific Figure Design (method + review rubric)

## Scope

- **This skill** = the design METHOD (what to show, how to encode it, how to
  lay it out, how to review it) and a review rubric for any figure.
- **python-plotting-style** = the HOUSE STYLE for everyday and exploratory
  plots (palette, figsize, fonts, RIXS conventions, fitting, error
  propagation). Load it too whenever you write matplotlib code.
- Do not edit or duplicate python-plotting-style. Compose with it.

### House-style overrides (publication and poster figures ONLY)

When the figure is for a paper or a poster, replace these five
python-plotting-style defaults. For everyday and exploratory plots, house
style applies unchanged. For talk slides the same five replacements are
recommended (step 8), but apply them only if the user agrees.

| # | House default | Publication / poster replacement |
|---|---|---|
| 1 | `ax.grid(alpha=0.2)` on every plot | Grid only when it helps the reader compare values. When used: major ticks only, 15-45% opacity scaled to data density, lighter than the axes, behind the data (`ax.set_axisbelow(True)`). |
| 2 | Legend `frameon=True, fancybox=True, shadow=True` | Plain legend (`frameon=False`), or direct labels next to the data where that saves legend lookups. Keep a legend for shared keys. |
| 3 | Bold axis labels (12) and bold titles (14) | One typeface, at most 2-3 type sizes per figure, bold/italic only for emphasis. Panel letters follow the journal's style. |
| 4 | >8 series: cycle the colors, then dashed, then dotted | Small multiples (one or a few series per panel), or, for an ordered series (temperature, delay, fluence), one ordered lightness ramp. |
| 5 | RIXS maps `cmap='terrain_r'` | A perceptually ordered sequential map (lightness changes monotonically). Diverging only around a meaningful center (difference maps, zero). Keep `LogNorm` if the data span decades, and say "log scale" on the colorbar. |

Everything else in house style still applies: the Okabe-Ito `colors` list
and imports at the top of every code block, `figsize`, `constrained_layout`,
`savefig(dpi=300, bbox_inches='tight', facecolor='white')`, the poster size
table and `dpi=150`, RIXS/XAS axis labels and Δ conventions, error-bar style,
and all fitting conventions.

## The design process (execute these steps in order)

### 1. State the message, audience and medium
- Write the figure's message as ONE sentence, like a newspaper headline. If
  you can't, the figure isn't ready to be drawn. Ask the user if the message
  can't be inferred from context.
- Name the audience (yourself and collaborators, journal readers, students,
  general public) and the medium (print/PDF, screen, talk slide, poster).
- Decide whether it is **exploratory** (overviews in which unknown patterns
  can appear) or **explanatory** (one known structure made obvious). This
  skill mainly targets explanatory figures.

### 2. List and classify the variables
- List every variable the figure could show. Record each one's type:
  categorical (unordered), ordered (ordinal, or a physical series such as
  temperature), or quantitative (one-signed, or signed around a meaningful
  center).
- Mark the **key comparison**: the one judgment the reader must make to get
  the message (A vs B, a trend over T, a peak shift, a distribution).
- Drop variables that don't serve the message. Keep the nesting of the data
  (sample > condition > scan) visible in the layout.

### 3. Choose encodings and plot type
- Give the key comparison the most accurate channel: **position on a common
  aligned scale** > position on nonaligned scales > length > angle/slope >
  area > volume/saturation > hue.
- Hue for categories, lightness for quantity. Encode each variable once.
  Don't encode quantities as area, angle or 3D.
- Pick the plot type by the question, not by habit
  (`references/plot-types.md`): bars for counts, box plots for
  distributions, small multiples for tangled overlays, 2D for non-spatial
  data.
- To compare two curves, plot their difference explicitly. Don't make the
  reader judge the gap between them (inference from the curve-gap illusion).

### 4. Sketch the layout
- Sketch on paper (or in words) before coding: panels, axes, reading order.
- Order panels to tell the story: context, then the main result, then the
  supporting evidence. A row reads as a sequence; pairs read as comparisons.
- Group with Gestalt cues. Proximity and similarity group loosely;
  connection and enclosure group strongly. Enclosure overrides the others,
  so use frames only where a unit must read as one.
- Align every panel edge, label and colorbar to a few grid lines.
- Whitespace hierarchy: tight gaps within a group, wider gaps between
  groups. Merge leftover space into regular blocks.

### 5. Build with restraint
- Data first. Axes, ticks, grids, labels and legends are navigation:
  thinner, lighter and fewer than the data marks (axes about 0.5 pt; grid,
  if any, at 15-45% opacity).
- One highlight color over gray/black context. Everything else neutral.
- Remove chartjunk: four-sided boxes, axis arrows, background fills,
  gradients, shadows, 3D effects, repeated words, surplus examples.
- Share and fix scales across panels that are compared. Flag every
  truncation, break, offset or per-panel rescale.
- Override library defaults on purpose (`references/matplotlib.md`).

### 6. Review and iterate
- Run the publication checklist below on the rendered figure at its final
  size. Squint at it (or view it as a thumbnail): what stands out first
  should be the message.
- If color carries meaning, check it in grayscale and with a red-green
  simulation.
- Revise and redraw. Don't keep the first version. Ask a colleague (or the
  user) what they read from it.

### 7. Write the caption
- Figure plus caption must be readable without the main text.
- Say how to read the figure (what each encoding means), repeat the key
  point, and state every non-default choice: whisker definition, error-bar
  meaning and n, color-scale range and norm, offsets, truncations,
  rescaling, normalization, binning.
- If readers need exact numbers, give them (on the figure or in the text).
  Don't make them estimate bar heights.

### 8. Make medium-specific versions
- **Paper**: full detail, fine lines, the caption carries the explanation.
- **Talk**: one message per slide, fewer traces and ticks, thicker lines,
  bigger text and points, strong contrast, no vertical text. Build complex
  figures up over several slides.
- **Poster**: readable from a distance (house poster table), few details, a
  strong visual entry point, reading order obvious from the layout.
- Never paste the paper figure unchanged into a talk.

## Publication checklist (yes/no; every "no" needs a fix or a stated reason)

Message and structure
1. Can you state the message in one sentence, and does the most salient
   element carry it?
2. Is every panel needed, and is the panel order the reading order?
3. Do grouping and spacing match the comparisons (tight within groups, wide
   between)?
4. Are panel edges, labels and colorbars aligned to a common grid?

Encoding
5. Is the key comparison on position along a common, aligned axis?
6. Is the plot type right for the question (counts, distribution, trend,
   overlap, correlation)?
7. Are curves that must be compared on the same axes or drawn as an explicit
   difference, rather than judged across a gap?
8. Is each variable encoded once, with no area, angle, 3D or hue used for
   precise quantities?
9. Are there about 6-8 categories or fewer per panel (otherwise small
   multiples, or an ordered ramp for an ordered series)?

Color
10. Is hue used only for categories and lightness for quantity?
11. Is the colormap perceptually ordered, with diverging maps used only
    around a stated, meaningful center?
12. Does the figure survive grayscale and red-green color blindness, with
    no red/green pairs?
13. Is color used for emphasis on a neutral base, with no unexplained color
    ("why is this blue and not black?")?

Axes, labels, marks
14. Are axes thin (about 0.5 pt), with no four-sided box, no axis arrows and
    no grid that isn't needed?
15. Do compared panels share scales, and is every truncation, break, offset
    or rescale shown on the figure and stated in the caption?
16. Do axis labels give quantity and units, and are tick labels free of
    repeated non-significant digits?
17. Is there one typeface, at most 2-3 sizes, bold only for emphasis, and no
    vertical text that could be horizontal?
18. Are labels at a consistent offset from their data, callouts horizontal
    or at one fixed angle, and leaders headless?
19. Are arrows used only for direction, sequence or causality?
20. Do markers stay distinct where they overlap (open circles for one dense
    series; no polygon-only sets; no stars)?
21. Are legends plain, and replaced by direct labels where that saves
    lookups?

Honesty and completeness
22. Do bars start at zero, or is the other baseline justified and stated?
23. Are distributions shown as distributions (box plots or points), with the
    whisker or error-bar definition and n stated?
24. Is the full relevant range shown, with no exaggeration through axis
    limits, aspect ratio or colormap limits?
25. Does the caption make the figure readable without the main text?
26. Was the figure checked at final print size, with a separate talk or
    poster version where needed?

## References (read the one you need)

- `references/principles.md`: perception and composition. Accuracy ranking,
  curve-gap illusion, salience, Gestalt grouping order, negative space,
  layout grids, dominance and restraint, storytelling, simplifying.
- `references/color.md`: categorical vs sequential vs diverging; the
  Okabe-Ito table (RGB as printed, plus hex); how many colors; color
  blindness; heat-map ordering; grayscale check.
- `references/elements.md`: typography; axes, ticks and grids with every
  number; labels and callouts; legends vs direct labels; plotting symbols;
  arrows.
- `references/plot-types.md`: "which plot for which question"; bars and box
  plots; sets; time; untangling and small multiples; overlay vs stacked vs
  offset; multidimensional data and 3D; diagrams.
- `references/workflow.md`: sketch first; exploratory vs explanatory;
  always plot the data; sampling and aggregation; Rougier's ten rules;
  medium-specific versions; caption rules; the full review rubric with the
  reason and source column for each checklist item.
- `references/matplotlib.md`: recipes that implement the method on top of
  house style. Medium presets, spines/ticks/grid, shared scales, nested
  panel spacing, direct labels, highlight over gray, colormaps and norms,
  small multiples, offset plots, checks.
- `references/sources.md`: all 41 columns plus Rougier, with authors, year,
  DOI, thesis and local PDF path.

Bracketed numbers in the references (e.g. [17], [R]) are column numbers in
`references/sources.md`.

## Honest limits

- None of the sources mentions spectroscopy, RIXS or XAS. Only Rougier
  mentions matplotlib, as the tool its figures were made with. Every
  RIXS/XAS mapping and every matplotlib recipe here is an **inference**; the
  references mark these "(inference)" or "Extension:".
- **Offset/waterfall plots are not covered by the sources.** Closest
  guidance: [40] overlaying profiles on a shared y axis makes comparing peak
  shapes and heights easier than separate vertically stacked tracks, at the
  cost of occlusion and color mixing; [24] any adjustment to scale ranges
  must be clearly presented. Treat an offset as a scale manipulation and
  state it on the axis or in the caption.
- The point sizes (0.5 pt axes, 0.75 pt arrows) are print values. They hold
  only if the figure is placed at 100% scale, so build the figure at its
  final printed width.
- The sources disagree on how many categorical colors readers can tell apart
  (6-8 [11] vs 8-12 [21]) and on diverging maps for one-signed data ([14] vs
  [40]). `references/color.md` gives both views and the default to use.
