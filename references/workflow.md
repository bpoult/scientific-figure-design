# Workflow: from sketch to caption, and the review rubric

Bracketed numbers are column numbers (see `sources.md`). "(inference)" and
"Extension:" mark what the sources don't state.

## 1. Sketch first [35, 03, 09]

- Drawing by hand is a thinking tool. It forces you to put things in a
  definite place: "Words afford us a level of ambiguity that is not extended
  to pictures." [35]
- Work fast and roughly, and refine many times, to explore many
  possibilities. Give up visual accuracy at this stage. [35]
- Pencil and paper have no learning curve. Software makes you think about
  *how* to draw rather than *what*. [35]
- Drawing extends working memory: "It is difficult for us to remember the
  attributes of more than a few objects for longer than several seconds."
  [35]
- Design is exploratory and needs fluid refinement. Master your main
  graphics tool so it never limits the design. [03]
- Don't keep your first idea. "Revise and redraw." [09]
- Extension (for an AI assistant): before writing `plt.subplots`, write the
  sketch out in words: the panel grid, what each panel shows, the shared
  axes, the reading order, the highlight. Ask the user to confirm it when
  the figure is complex.

## 2. Exploratory vs explanatory figures [36, 01, R1]

- Two purposes: communicating findings (a known structure is highlighted)
  and guiding exploration ("the researcher suspects that regularities are
  present but does not know exactly what they are"). [36]
- Exploration: overviews in which patterns can emerge; iterate between
  hypotheses and plots. Presentation: one message, made obvious. [36]
- Visualization pays off for exploration and to give a mental image of what
  algorithms found. Not every question needs a picture. [01]
- Audience decides detail [R1]: for yourself and collaborators, steps can be
  skipped; for a journal, the figure must be correct and complete; students
  need extra explanation; the public needs a simple, possibly approximated
  figure.
- House style covers exploratory plots; this skill's overrides apply when a
  figure moves to publication (inference).

## 3. Always plot the data [36]

- "It is essential to look at data in a graphical form and not rely solely
  on computational metrics." Anscombe's quartet: four datasets with the same
  means, variances, correlations and regression lines look completely
  different when plotted. [36]
- Spectroscopy mapping (inference): show fits with residuals, not only R²
  or χ². Identical fit statistics can hide different line shapes.

## 4. Sampling, aggregation, overview + detail [36, 39, 40, 10]

- "Displaying too much data simultaneously often presents a visual burden
  that should be avoided." Leave some data out ([36] showed 1 of 4
  replicates). With many components, sample a subset. As understanding
  grows, drop features of less interest and bring others in. [36]
- Plot simple low-dimensional "slices", ideally one plot per component, on
  a common scale. [36]
- Binning works only if the features are larger than the bins; smaller
  features vanish. [39] Spectroscopy mapping (inference): don't rebin
  coarser than the narrowest feature (pre-edge, elastic line).
- Remove uninteresting stretches but keep order and context ("accordion"
  view). [39]
- Every reduction trades overview against detail; the right balance depends
  on the resolution at which the data must be read. [40]
- Summaries complement raw data; they don't replace it. Show raw data as a
  second layer (inset, supplementary panel). [40, 39]
- Overview + detail panel pairs: see `plot-types.md` §5. [24]
- Aggregate to the level the message needs. [10]
- Try two or three encodings of the same data and keep the one that makes
  the relevant feature most noticeable. [37, 38, 39, 41]

## 5. Rougier's ten rules in brief [R]

1. **Know your audience.** Decide early who the figure is for.
2. **Identify your message.** The message guides the design.
3. **Adapt the figure to the support medium.** Paper, screen, projector and
   poster each need their own version.
4. **Captions are not optional.** Explain how to read the figure and what
   can't be drawn.
5. **Do not trust the defaults.** They are "good enough for any plot but
   they are best for none."
6. **Use color effectively.** Highlight in color over gray/black; match the
   colormap class to the data; no jet without a reason.
7. **Do not mislead the reader.** Simplest plot type; full range of values
   when relevant; area (not radius) for size; ask colleagues how they read
   it.
8. **Avoid chartjunk.** Too many colors or labels, gratuitous backgrounds,
   useless grid lines. A background element is fine when it encodes
   something and the caption explains it.
9. **Message trumps beauty.** Use your field's standard figure types; adapt,
   don't copy, from the literature.
10. **Get the right tool.** Matplotlib for 2D plotting; Inkscape to polish
    script-made figures; visualization tools can differ from analysis
    tools.

## 6. Medium-specific versions [R3, 29, 08, 17, 16, 10]

"Ideally, each type of support medium requires a different figure, and you
should abandon the practice of extracting a figure from your article to be
put, as is, in your oral presentation." [R3]

| | Paper | Talk / slide | Poster |
|---|---|---|---|
| Detail | Full; reader can study it [R3] | Minimal, one message, salient [R3] | Few details, strong entry point (inference) |
| Lines, points | Fine (0.5 pt axes [17]) | Thicker lines, bigger points [R3] | Thick (house: `linewidth=3` minimum) |
| Text | 2-3 sizes [16] | Bigger; **no vertical text** [R3] | House poster table; minimal vertical text (inference) |
| Ticks, traces | As needed | Fewer [R Fig. 3] | Fewer (inference) |
| Color contrast | Normal | Strong [R3] | Strong (inference) |
| Highlighting | With restraint [08] | Encouraged; audience listens and reads at once [08, 29] | Encouraged (inference) |
| Grid | If needed, 15-45% | Remember projectors wash out light lines [17] | As talk (inference) |
| Explanation | Caption | Speaker; build up over slides (inference from [10]) | Short takeaway titles [10] |

Also: salience lowers cognitive load, which matters most on slides and
posters, where visual and spoken information compete. [29] Typeface: sans
serif works well for slides. [16] Layout for slides and posters: set a grid
first and plan the reading path. [04, 07]

## 7. Caption rules [R4, 21, 24, 14, 10]

- The caption explains how to read the figure and gives the precision that
  can't be drawn. Anticipate the questions people would ask in front of a
  poster. [R4]
- Point out the points of interest again, after making them visually
  distinct. [R4]
- If numbers matter, give them. Don't make readers estimate bar heights.
  [R4]
- State: the whisker definition [21]; every scale adjustment, truncation,
  break [24] and offset (extension); the color-scale range choice,
  theoretical vs observed [14]; the error-bar meaning and n (inference);
  normalization and binning (inference).
- Headlines and takeaway titles must follow journal style. [10]
- Test: can the figure plus caption be understood without the main text?
  (inference from [R4])

## 8. Review rubric (expanded checklist)

Run it on the rendered figure at final size. Items match SKILL.md.

| # | Check | Why | Source |
|---|---|---|---|
| 1 | One-sentence message; most salient element carries it | What stands out is taken as most important | [10, R2, 08] |
| 2 | Every panel needed; panel order = reading order | Unfold the story; cut what doesn't advance it | [10, 27, 04] |
| 3 | Tight within groups, wide between | Proximity and whitespace signal grouping and hierarchy | [05, 07, 30] |
| 4 | Edges, labels, colorbars aligned to a grid | Grids anchor content; small misalignments are noticed | [04, 06] |
| 5 | Key comparison on common aligned position | Most accurate perceptual task | [28] |
| 6 | Plot type fits the question | Data and task decide the form | [21, 22, 23, 24, 33] |
| 7 | Compared curves overlaid or differenced | Gaps between curves are misjudged | [28] (fix is inference) |
| 8 | Each variable encoded once; no area/angle/3D/hue for quantities | Low-ranked channels; double encoding wastes channels | [28, 26, 32, R7] |
| 9 | ≤ about 6-8 categories per panel | Distinct colors and symbols run out | [11, 19, 21] |
| 10 | Hue = category, lightness = quantity | Hues have no inherent order | [11, 14] |
| 11 | Ordered colormap; diverging only around a stated center | Rainbows and misplaced diverging maps misrepresent values | [11, 14, 31, R6; exception 40] |
| 12 | Survives grayscale and red-green CVD | 8% of men; 22% chance with three reviewers | [12, 15] |
| 13 | Color only for emphasis on a neutral base | Color stands out on black and white; overuse is clutter | [08, 13, R6] |
| 14 | Thin axes, no box, no axis arrows, no needless grid | Navigation must not compete with data | [17, 21, R8] |
| 15 | Shared scales; every truncation/break/offset/rescale flagged | Range changes are easily overlooked and can deceive | [17, 24, R Fig. 6] |
| 16 | Quantity + units; no repeated tick digits | Repetition adds clutter; adjust the units | [17] |
| 17 | One typeface, 2-3 sizes, bold for emphasis, no needless vertical text | Consistency; legibility at distance | [16, 18, R3] |
| 18 | Consistent label offsets; callouts horizontal or one fixed angle; headless leaders | Labels belong to their data; variety by data, not formatting | [18, 20] |
| 19 | Arrows only for direction/sequence/causality | Arrows are read as change and causality | [20] |
| 20 | Distinct overlapping markers; no polygon-only sets, no stars | Polygons blend; stars inflate importance | [19] |
| 21 | Plain legend or direct labels | Fewer lookups; no decoration | [R Fig. 7, 19, 18] |
| 22 | Bars from zero, or baseline justified | Bars imply magnitude from the baseline | [21, R Fig. 6] |
| 23 | Distributions shown as distributions; whiskers/error bars and n stated | Bars ± s.d. can hide distribution shape | [21, 36] |
| 24 | Full relevant range; no exaggeration by limits, aspect or color limits | Auto-scaling can be technically labelled but misleading | [R7, 24, 14] |
| 25 | Caption makes it self-contained | Captions are not optional | [R4] |
| 26 | Checked at final size; separate talk/poster version | Each medium needs its own figure | [R3] |
