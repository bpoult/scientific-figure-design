# Principles: perception and composition

Bracketed numbers are Points of View column numbers ([R] = Rougier et al.
2014); see `sources.md`. "(inference)" marks a mapping the sources don't
state. The sources never mention spectroscopy.

## 1. Design serves a function

- A figure is a tool for a task. It works only if the reader can decode its
  visual scheme. "Design is a requirement, not a cosmetic addition." [03]
- Represent different kinds of information in clearly different ways, so
  readers learn the figure's "visual vocabulary" quickly. [03]
- Base design on how perception works, not on intuition and precedent.
  Authors encode and readers decode. [28]
- Clear objectives drive design: what does the reader need to see, and which
  encoding brings it out? Large, colorful displays can fool us into
  believing we absorb more than we do. [01]
- Put yourself in the background. Your favorite color or a clever shape is
  not a reason. "Be legible without shouting." [09]

## 2. Accuracy ranking of visual encodings [28]

Cleveland and McGill's ranking of elementary perceptual tasks, from most to
least accurate (here "accuracy" means judging relative magnitude, not
reading off values):

1. Position on a common scale
2. Position on the same but nonaligned scales
3. Length
4. Angle, slope
5. Area
6. Volume, color saturation
7. Color hue

Consequences:
- Put the key comparison on position along a common, aligned axis. Panels
  with separate y axes drop it to rank 2. [28]
- Bars beat pies for relative differences, direction and magnitude,
  especially small differences. [28, 31] If a pie is unavoidable (parts of a
  whole), put the largest wedge just right of 12 o'clock, the second just
  left of it, and the rest counter-clockwise in descending size. [31]
- Area is misjudged: in [28] Fig. 1a the large circle is 14 times the small
  one, and it doesn't look it. If size must encode value, scale the **area**,
  not the radius. [R Fig. 6]
- Hue has no inherent order ("does yellow represent a smaller value than
  blue?"). Don't use it for magnitude. [11, 28]
- Graphs are for patterns and trends. Tables are for precise numbers. [28]
- When you invent a new graph type, build it from high-ranked tasks. [28]

## 3. The curve-gap illusion [28]

- The vertical gap between two curves is misjudged. A constant difference
  looks as if it shrinks where the curves are steep, because we perceive the
  minimum (perpendicular) distance. [28 Fig. 1a]
- Fix (inference; [28] diagnoses but prescribes no fix): when the
  difference matters, plot it, e.g. a residual or difference panel below on
  a shared x axis. This applies to data vs fit, sample vs reference, and
  pumped vs unpumped spectra.

## 4. Salience: what pops out and what doesn't

- Salience is contrast with surroundings. It increases reading **speed**
  ([28] was about accuracy). [29]
- Pop out pre-attentively: color, orientation, size, motion. [29] Also
  listed as salient features: shape, an added mark, grouping. [29 Fig. 1b]
  Shape alone pops out weakly: a "P" among "A"s is hard to find. [29]
- To make something easy to find, make its primary visual feature differ
  **substantially** from its neighbors. [29]
- Searching for a conjunction of two features takes concentration. Layer
  only a few noncompeting features per view. Otherwise show multiple views,
  each with a subset of the parameters. [29, 31]
- Salience should equal relevance. What stands out is taken as most
  important. [08] Larger items are read first; a diagonal stands out among
  horizontals and verticals; color stands out on black and white. [08]
- Accidental salience misleads. In a blue-to-red heat map, deep red highs
  can be less visible than deep blue lows, so the lows become the most
  salient. Hue visibility is asymmetric. [08] Abrupt jumps in a color scale
  accentuate particular ranges. [13]
- Motion is the strongest cue. Animate only what matters most, and never
  loop an animation next to text you want read. [08, 29]
- Highlighting suits slides especially. [08] notes it is "not appropriate
  for all journal publications". But print figures in [29], [31] and [R]
  use one highlight color over gray context, so use it in papers too, with
  restraint.
- Test: stand back and squint. [08] (Also [11] for color evenness.)

## 5. Gestalt grouping [05, 06]

- Similarity (color, size, shape; repeated font, size, orientation, spacing)
  and proximity give "loose confederations". [05]
- Connection (lines) and enclosure (a common region) give a unified whole.
  [05] Lines bring out the overall shape of the data. [05 Fig. 2b]
- **Strength order**: enclosure overrides similarity, proximity and
  connection. Connection beats proximity and similarity. [05 Fig. 2a] Use
  enclosure only where a unit must read as one, or to draw attention to a
  group. [05]
- Panels in an evenly spaced 2x2 grid are ambiguous (compare? read in
  sequence?). Two pairwise comparisons → two visibly separated pairs.
  Sequential reading → one row. Row vs column spacing decides whether items
  group vertically or horizontally. [05 Fig. 1c,d]
- Visual completion: we perceive illusory contours and complete hidden
  shapes. So drop extraneous lines, boxes and bullets and let alignment
  imply the structure. [06]
- Treat text and graphics as shapes with edges. Draw background guide
  shapes, snap components to them, then remove the guides. Use separate
  guides for different kinds of information (e.g. action labels vs names).
  The eye notices small misalignments. [06]

## 6. Negative space and hierarchy [07, 30]

- Whitespace is "as much a part of a composition as the titles, words and
  pictures". [07] It frames content and gives the eyes a place to rest. [06]
- Crowded figures and posters are hard to read mainly because the
  whitespace is **irregular**. [07] Box every block (by eye), then align the
  boxes so the whitespace forms regular, contiguous blocks. [07]
- Spacing signals hierarchy: larger gaps between sections, thinner gutters
  within. [07, 30] Merge scattered empty areas into regular shapes. [30]
- To emphasize something in a congested layout, surround it with more
  whitespace. This beats bold or caps. [07, 04 Fig. 2c]
- Scale images proportionally. Reshape text blocks instead. [07]

## 7. Layout grid and alignment [04, 06, 27]

- Set up a grid or guides **before** placing content. Grids anchor content,
  add stability and keep slides consistent. [04]
- Align to a few imaginary horizontal and vertical lines. [27]
- Golden section (≈1.618 ≈ 13:8) and the rule of thirds give strong
  placement points. [04] They are tools, not goals; [04] itself notes that
  compositional aesthetics can serve a different purpose from communication.
- Let the intent of the figure drive the layout. For sequences, stack
  horizontal groups vertically with aligned connecting arrows. Use
  orientation or misalignment to set side branches apart from the main
  path. [30]

## 8. Dominance and restraint [04, 09, 17]

- Plan the eye's path: what is read first, second, third. Develop dominance
  in some elements and restraint in others. [04]
- Equal visual weight everywhere leaves no entry point. "Without contrast,
  you're dead" (Paul Rand, quoted in [04]).
- Two ways to attract attention: make the element visually different, or
  frame it in white space. [04]
- Chartjunk (textures, gradients, many shapes) makes selective emphasis
  impossible. If you can't easily emphasize an element, the figure is
  overstated. Chartjunk "can never rescue a thin data set". [09]
- Navigational elements (axes, ticks, grids) must be distinct and
  unobtrusive so the data keep visual priority. [17]
- A light visual style is what makes selective emphasis possible. [34]

## 9. Storytelling: "unfold it, don't dump it" [10]

- Use story structure across panels: introduction, question, buildup,
  resolution. Make each panel's content **and purpose** clear.
- Start from the headline: "If your study were reported in the newspaper,
  what would the headline be?"
- Leave out detail that doesn't advance the plot. Don't show all your
  hard-won data. Inviting readers to draw their own conclusions is risky,
  because even simple messages can hide in simple data.
- Aggregate or bin to the level of detail the message needs (e.g. ten raw
  values → three bins → a bar chart with an asterisk). Use conventional
  notation.
- Light axes and grids keep the focus on the trend. Choose the vertical
  scale to bring out the intended comparison, and stay accurate.
- Panel-order example for spectroscopy (inference): map → line cut or
  spectrum → fit → parameter trend.

## 10. Simplify to clarify [27, 09, 02]

- "The best way to simplify is to reduce the number of elements on the
  page." Use the fewest possible marks without losing sophistication. Tufte's
  data:ink ratio: remove whatever is decorative or erasable without losing
  data. [27]
- Judge every component against the figure's primary goal. Build a
  hierarchy, remove extras, refine the rest. [27]
- Pull repeated label words ("reaction 1", "reaction 2") into a header.
  Show the minimum number of examples. [27]
- Group so that many parts read as a few. Action labels go on arrows;
  object labels go next to the objects. [27]
- Simple is not simplistic. [27] Use the simplest representation and
  "omit needless words". [09]
- Parallel construction: express coordinate ideas in similar form. Related
  items share a form and differ only in tone; a series of symbols should
  show progression. [09]
- One meaning per symbol (arrows for progression, headless leaders for
  labels). Keep a depiction consistent across steps and account for every
  element added or removed. [02, 30]
- Overview/schematic figures show concepts, not data. Real data inside an
  overview figure is ambiguous. [02]
- "Revise and redraw." Don't keep your first idea. [09]
- Bin continuous size and shade scales into a few ranges rather than asking
  readers to tell apart 8 sizes and 11 shades. [31]
