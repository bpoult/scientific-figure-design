# Plot types: which plot for which question

Bracketed numbers are column numbers (see `sources.md`). "(inference)" and
"Extension:" mark what the sources don't state. Every column picks the form
only after asking what the data are and which comparison the reader must
make. "Creating a simple yet effective plot requires an understanding of
data and tasks." [21]

## 1. Question → plot

| Question | Plot | Source |
|---|---|---|
| Compare totals and show their parts | stacked bars | [21] |
| Compare one component across items | layered bars (one panel per component, common baseline) | [21] |
| Compare components within each item | grouped bars | [21] |
| Parts of a whole | bars (grouped) preferred; pie only with ordered wedges | [21, 28, 31] |
| Compare distributions | box plots, whisker rule stated | [21] |
| Overlap of 2-3 sets | area-proportional Euler diagram | [22] |
| Overlap of >3 sets | matrix layout with intersection-size bars (UpSet-style) | [22] |
| Pairwise overlap of 10+ sets | clustered heat map of pairwise sizes (conditional, see §3) | [22] |
| Trend over time | line or bar chart, time on x | [23] |
| Recurring (cyclic) timing or peak height | superimposed aligned cycles | [23] |
| Many time series, qualitative view | sparklines (if journal style allows) | [23] |
| Trajectory in a 2D variable space | connected traces, time in brightness | [23] |
| Many curves, similar ranges | small multiples, common scale | [24, 36] |
| Many curves, different ranges | small multiples, scaling chosen and labelled | [24] |
| Compare peak shapes/heights of a few profiles | overlay on a shared y axis | [40] |
| Classify curve shapes across many items | small multiples, filled under the curve | [36] |
| Pairwise correlations among many variables | scatter-plot matrix (SPLOM) | [33] |
| Follow individual items across many variables | parallel coordinates | [33, 15] |
| Matrix of values (non-spatial) | 2D heat map, never a 3D bar or surface | [32] |
| Network: local paths, small | node-link diagram | [37] |
| Network: large, clusters and hubs | reordered adjacency matrix | [37] |
| Directed flow or process | grid-aligned node-link diagram | [25, 26] |
| Data that really are 3D-spatial | 3D, with occlusion minimized | [32] |

Rougier: use "the simplest type of plots that can convey your message"; pie
charts and 3D charts for comparing quantities "are known to induce an
incorrect perception of quantities". [R7] Know the standard figure types of
your field. They allow comparison and help you spot errors. [R9]

## 2. Bars vs box plots [21]

- "Bar charts are appropriate for counts, whereas box plots should be used
  to represent the characteristics of a distribution." [21]
- Bars of means with error bars "can be misleading": bars start at zero, so
  part of the range a bar covers may never have been observed. "If our goal
  is to represent and compare distributions", use a representation that
  reflects the data, such as a box plot. In [21] Fig. 2, bars ± s.d. hide
  the very different shapes of uniform, normal, Poisson and exponential
  samples. [21]
- **Box plot**: box from Q1 to Q3 (the IQR), a line at the median. Whiskers
  are "typically" the most extreme points within Q1 − 1.5 × IQR and
  Q3 + 1.5 × IQR, with each outlier beyond them marked. Other definitions
  exist (e.g. min/max), so "always annotate the range of the whiskers". [21]
- Order bars by height and boxes by median, unless the items have an
  implicit order. [21]
- "Use zero as a base line for bar charts unless there is a reason for
  choosing a different reference point." [21] A truncated bar axis makes
  similar values look very different, even when labelled. [R Fig. 6]
- Solid fills, no outlines. Tick marks, and grid lines if necessary, lighter
  than the axes. [21]
- Stacked bars: totals plus contributions, but only the bottom segment has a
  common baseline. Layered bars: every category gets its own baseline, so
  within-category comparison is more accurate. Grouped bars: compare
  categories within an item; with equal totals they replace several pie
  charts. [21 Fig. 1]
- Don't make readers estimate bar values. Give the numbers if they matter.
  [R4]
- [21] links a box-plot web tool, http://boxplot.tyerslab.com/ (Spitzer et
  al. 2014).
- Spectroscopy mapping (inference): a fit parameter over many repeats or
  scans is a distribution → box plot (or the points). A count or a quantity
  with a true zero → bars.

## 3. Sets and intersections [22]

- Intersections are easy to show for up to 3-4 sets. n sets have 2^n
  possible intersections (3 → 8, 10 → 1,024).
- Euler diagrams (empty intersections omitted) suit 2 or 3 sets. Make them
  area-proportional; ellipses reach proportionality more often than circles.
  Area is a weak channel, but acceptable here because there are few
  intersections and the form is familiar.
- More than 3 sets: matrix layout. Columns = intersections shown as binary
  membership patterns, with a bar for each intersection's size and set-size
  bars along the rows. Bars can be log-transformed and sorted by size, or by
  set combination, depending on the task. Drop empty intersections when
  there are many sets. (Tool: vcg.github.io/upset/.)
- "Plotting all intersections of 10 or more sets at once is usually not
  feasible. Depending on the data and the questions, however, it can still be
  beneficial to plot" pairwise intersections as a clustered heat map, with
  set sizes along an edge. It hides higher-order intersections.

## 4. Temporal data [23, 38]

- Time can be encoded as position, brightness/saturation, or animation.
  "Position … should be considered first", with time on the horizontal axis.
  [23]
- Recurring patterns: cut the time axis into cycles, align them and
  superimpose them, so peak timing and height can be compared. Shift the
  axis origin to center the feature. If cycle lengths vary, either normalize
  them (stresses the pattern) or don't (shows the length differences). [23]
- Choose linear layouts over radial/radar charts "unless there is a
  compelling reason to show a continuous curve for aligned cyclic patterns".
  [23]
- When both spatial axes are already used, show time as connected traces,
  optionally with time in brightness or saturation. Mark start and end
  (filled vs hollow markers). [23]
- Animation makes recurring patterns and time-point comparisons hard. Weigh
  it against small multiples. [23] Stepping through frames limits the viewer
  to pairwise comparisons; small multiples allow comparison across "a dozen
  or more conditions". [38] In papers, use small multiples (inference: print
  is static).
- Extension: for an ordered series of overlaid spectra (pump-probe delay,
  temperature), a monotone lightness ramp encoding the series order extends
  [23]'s brightness encoding for traces. [23] doesn't discuss line overlays.

## 5. Untangling complex plots [24]

"Carefully designed subplots scaled to the data are often superior to a
single complex overview plot." [24]
- One plot scaled to all the data becomes "a jumble of lines". Overplotting,
  occlusion, poorly separated channels (color + dash + symbol), compressed
  small-range traces and added error bars all hide patterns.
- "When categories have similar ranges, small multiples may solve the
  problem." Keep design elements consistent across the multiples. The extra
  page space is worth it.
- When ranges differ, choose a scaling scheme that matches the message:
  - common scale: honest absolute comparison, but small-range panels flatten;
  - each panel to its own range: within-category change, weak cross-panel
    comparison;
  - each panel's maximum with a **global minimum**: variation in context.
  - progressive truncation: panel ranges shrink step by step, linked by
    reference lines or shaded backgrounds.
- Truncation can deceive: "any adjustment to scale ranges needs to be
  clearly presented". **Flag every truncation, break or rescale** on the
  figure and in the caption.
- Show the other data faintly (light gray) behind each panel's highlighted
  series, for context. Avoid too much embellishment. [24 Fig. 1c, R Fig. 7]
- **Aspect ratio**: it changes how slopes are perceived. "Choosing one that
  orients the average trace to 45 degrees is a useful rule of thumb" (after
  Cleveland's banking). [24] The same 45° rule applies to the mean absolute
  line angle in parallel coordinates. [33]
- **Overview + detail**: a full-range panel next to a cropped detail panel,
  linked by matching shaded backgrounds. A vertical stack helps readers spot
  common changes. [24 Fig. 2f]
- **Nonlinear axes** (log, probit, logit, reciprocal) increase dynamic range
  and can linearize Gaussian or sigmoidal data. [24]
- Axis breaks separate non-overlapping ranges but distort perceived absolute
  differences. [24] Follow journal policy; breaks can hide patterns. [17]

## 6. Overlay vs stacked tracks vs offset (waterfall) plots

The sources never discuss offset/waterfall plots ("waterfall": 0 hits).
- [40]: overlaying profiles with transparency in one row on a shared y axis
  makes "comparing the shapes and heights of peaks easier than having the
  profiles arranged in separate and vertically stacked tracks". Drawbacks:
  "some data is obscured", and colors mix.
- [39]: align regions on a common reference point, stack them, sort them by
  a metric, and add a summary profile (mean ± spread) underneath.
- [24]: small multiples with clearly presented scaling.
- [23]: superimpose a few comparable curves (5 in [23]); [24]: use multiples
  for many curves or different ranges (12 in [24]). Neither gives a numeric
  switch point.

Extension (recommended default for spectra):
- **≤ ~5 comparable spectra, heights matter** → overlay on a shared y axis.
- **Many spectra, shape or trend matters** → small multiples with a shared x
  axis, or a 2D map with line cuts.
- **Offset plot**, when vertical stacking is clearly the field standard
  [R9]: use one constant offset, sort by the physical variable, label each
  trace directly at its baseline, and **state the offset** ("offset by 0.5
  for clarity") in the axis label or caption. The offset is a scale
  manipulation under [24]. Absolute intensity is no longer comparable
  between traces, because the curves no longer share a common baseline.
  Don't use one if intensity comparison is the point.

## 7. Multidimensional data [32, 33, 34]

- "Three-dimensional visualizations are effective for spatial data but
  rarely for other data types." [32] Perspective distorts lengths,
  foreground objects occlude, and software shading confounds
  color-as-quantity. A 3D bar chart of a matrix → a 2D heat map.
  [32 Fig. 2]
- The exception is inherently spatial data (e.g. crystallographic
  structures). [32] RIXS and XAS maps are not spatial, so use 2D
  (inference).
- If you do use 3D: minimize occlusion, avoid semitransparent surfaces with
  color, and place labels after projection (in 2D), not in the 3D scene.
  [32]
- Extra dimensions in 2D: size or color for further quantities; shapes for a
  few categories; small multiples; SPLOM; heat maps; parallel coordinates;
  dimensionality reduction (PCA, MDS) if some information loss is
  acceptable. [32]
- Each added encoding layer (color, then size, then symbol) costs clarity.
  "The number of dimensions and the selection and layering of encodings can
  have a profound effect on clarity." [34 Fig. 1]
- **Parallel coordinates vs SPLOM** [33]: the choice "depends on the
  analytical task". Parallel coordinates follow individual items across
  dimensions and show clusters, trends and outliers. Scale all axes the same
  when the dimensions share a type and unit. They are poor for mostly
  categorical or few-valued data. SPLOMs show pairwise correlations but make
  following one item hard. Set the mean absolute line angle near 45°.
- Spend position on what matters most. [34] spends it on the domain
  structure (a network schematic repeated as small multiples) rather than on
  quantities. Procedure: list variables → classify → encode → keep the
  nesting of the data in the layout.

## 8. Diagrams (schematics, setups, pathways, circuits) [25, 26, 02, 30]

- Place nodes on a **grid**. Flow runs **left to right and top to bottom**;
  feedback loops run clockwise. Break the convention only sparingly. [25]
- Edge angles in multiples of **30° or 45°**. Draw curves from circular
  guides. Attach edges at a fixed set of connector points. [25]
- **0.5-pt** edge lines, plain solid arrowheads (2.5-pt equilateral
  triangles in [25]), no stylized arrows. [25]
- Desaturated node colors, so text stays legible. No gradients or drop
  shadows. Mostly black/gray with **one highlight color** (or very few). [25,
  26, 09]
- Size nodes for the longest label or abbreviate. Don't reshape single
  nodes. [25]
- Never encode a variable twice. Vary an element only if it encodes
  something. [26]
- If position implies anatomy or geometry, readers will assume it is
  accurate. Mark uncertainty. Otherwise rearrange for clarity. [26]
- Show only the structure the message needs. [26] Concepts, not data. [02]
- Redraw the previous step's elements and highlight only what changed.
  Account for every element added or removed. [02]
- Arrows for progression, headless leaders for labels. Action labels on
  arrows, object labels next to objects. [02, 27]
- Spectroscopy mapping (inference): beamline and setup schematics, energy
  level diagrams and pump-probe timing diagrams follow these rules.
