# Color

Bracketed numbers are column numbers (see `sources.md`). "(inference)" and
"Extension:" mark what the sources don't state.

## 1. What color is for

- Color has three properties: **hue** (its name, e.g. red), **saturation**
  (distance from neutral gray) and **lightness** (position from dark to
  light). [11]
- Use **hue for categories** and **lightness for quantity**. Hues have no
  inherent order, so color is "not ideal for encoding quantitative data".
  [11, 14, 28, 31]
- For quantities, "principally rely on color value [lightness] and reserve
  hue to indicate different segments of the data range". [14]
- Color has four jobs: "to label, to show quantities, to represent or
  simulate reality, and to enliven or decorate". It isn't the most accurate
  channel for quantities, but it is "often the best choice for compact
  visualizations of large data sets". [14]
- For ranking, comparing profiles, peak positions or line shapes, length and
  position beat color. Redraw a heat map of profiles as line plots (filled
  under the curve) when shape is the task. [13, 15] That also leaves color
  free for a categorical variable. [13]
- Ask "Is there any reason this plot is blue and not black?" If you don't
  know, keep it black. [R6]
- To highlight, color the element of interest and keep the rest gray or
  black. [R6, 29, 31] In schematics, reserve color for emphasis. [09, 25]

## 2. Categorical palettes

- Choose colors that are distinguishable from each other but **comparable in
  visibility**. A much more intense or much lighter category biases the
  reader: lighter categories look under-represented. [11, 13]
- Build the palette by spiralling around the hue wheel while also stepping
  lightness, so the colors stay distinct in grayscale and photocopies.
  [11 Fig. 2]
- Colors are easier to tell apart when they differ in lightness and
  saturation as well as hue. [12]
- Smaller objects and thinner lines need **larger** differences in hue,
  saturation and lightness. [11]
- Avoid many similar colors. [R6]

### How many colors? (the sources disagree)

| Source | Statement |
|---|---|
| [11] Wong 2010 | "we can define a group of 6–8 colors. Beyond this number, the task of picking distinctive colors becomes difficult." For more categories, add texture or shape. |
| [21] Streit & Gehlenborg 2014 | "8–12 colors are the maximum that readers will be able to differentiate" (solid-filled bars and boxes). |
| [19] Krzywinski & Wong 2013 | For plotting symbols: more than six or seven categories → "consider" small multiples. |
| [R6] | Avoid "too many similar colors". |

**Default: 6-8 categorical colors per panel.** It matches [11], the 8-color
palette of [12] and the 6-7 of [19]. Treat 8-12 as an upper bound for large
solid fills only. Beyond that, use small multiples or a secondary channel
(marker shape, line style), not more hues.

### The colorblind-safe palette [12, Fig. 2]

Printed in [12] as a palette that "can be differentiated by individuals with
red-green color blindness". The column does not name it. It is the Okabe-Ito
palette (Okabe & Ito 2008; [R] cites them), and it is the house `colors`
list. RGB and CMYK are as printed in [12]; hex is converted.

| Name (as printed) | RGB (0-255) | CMYK (%) | Hex |
|---|---|---|---|
| Black | 0, 0, 0 | 0, 0, 0, 100 | #000000 |
| Orange | 230, 159, 0 | 0, 50, 100, 0 | #E69F00 |
| Sky blue | 86, 180, 233 | 80, 0, 0, 0 | #56B4E9 |
| Bluish green | 0, 158, 115 | 97, 0, 75, 0 | #009E73 |
| Yellow | 240, 228, 66 | 10, 5, 90, 0 | #F0E442 |
| Blue | 0, 114, 178 | 100, 50, 0, 0 | #0072B2 |
| Vermillion | 213, 94, 0 | 0, 80, 100, 0 | #D55E00 |
| Reddish purple | 204, 121, 167 | 10, 70, 0, 0 | #CC79A7 |

Notes:
- [12] carries an "amendments" notice whose content isn't in the local
  sources.
- [08] Fig. 1a shows 6 of these colors (no Yellow, no Reddish purple) with no
  name and no colorblind claim. Cite [12] for the palette.
- Yellow (#F0E442) is very light on white. Under [11]'s thin-line and
  comparable-visibility rules, avoid it for thin lines or small markers, or
  thicken it (inference).
- Black is in the palette. When black is the data or highlight color, don't
  also use it for a category (inference).

## 3. Color blindness [12, 15]

- Up to **8% of men** and **0.5% of women** of Northern European ancestry
  have the common red-green deficiency. With three male reviewers, the chance
  that at least one is color blind is **22%**. [12]
- It isn't only pure red and green: "any color with components of red and
  green can cause trouble". [12] Avoid red-green as a combination. [15]
- Carry contrast in **lightness** too, not hue alone. A hue-only figure
  disappears in grayscale (the Ishihara plate). [12 Fig. 1]
- Simulate before publishing (protanopia, deuteranopia). [12] names
  Illustrator/Photoshop proof setups and Vischeck.
- **Two-channel images** (immunofluorescence; by extension elemental or
  two-signal maps): replace red with **magenta** (copy the red channel into
  blue), so the channels read as magenta and green. Add a key saying the
  overlap shows as white. Replacing green with turquoise also works. [12]
- Use colorblind-safe colors in diagrams too. [26]

## 4. Sequential maps (one-signed data)

- For data that are only positive (or only negative), use a map that varies
  **only lightness**. The sources' example is **10% to 90% black**.
  [14, 15, 31]
- Rainbow scales are "inherently problematic". Their hue transitions are
  uneven, so equal value steps don't look equal. Using only a few rainbow
  colors doesn't fix that. [11, 31] Avoid jet/rainbow without an explicit
  reason. [R6] A rainbow and a diverging map both hid fine detail that a
  sequential map revealed. [R Fig. 5]
- Yellow ramps have a very narrow lightness range. [31]
- Avoid **abrupt transitions** in hue or lightness. They accentuate certain
  ranges. [13]
- Fit the map to the data on purpose and say which you chose [14]:
  (i) zero to the theoretical maximum keeps context; (ii) observed min
  (lightest) to max (darkest) gives contrast when zero isn't a meaningful
  reference.
- First decide which values must stand out: the extremes, or special values
  such as zero, a threshold, "sea level" or 32 °F. A deliberate break at a
  special value is fine. [14 Fig. 1d]
- Extension: in matplotlib, `Greys`, `Purples`, `Blues` (single hue) and
  `viridis`, `cividis`, `magma` (multi-hue) all increase monotonically in
  lightness; the sources name none of them except [R]'s "purple one". Measured
  CIE L* at 11 even steps (matplotlib 3.8): viridis 15→91 monotonic; cividis
  14→91 monotonic; `terrain_r` 100, 78, 55, 54, 77, 98, 86, 76, 66, 50, 28.
  That is not monotonic, so terrain_r breaks the lightness rule. That's why
  the skill overrides it for publication.
- Extension: for RIXS maps spanning decades, keep `LogNorm` (a nonlinear
  scale, which [24] accepts if clearly presented) and say "log scale" on the
  colorbar or in the caption.
- Labelling the colorbar with quantity, units and scale is good practice,
  but it is an inference: [14] and [15] don't state it.

## 5. Diverging maps (signed data around a meaningful center)

- For data with positive and negative values: **hue for sign** (e.g. red vs
  blue), **saturation for magnitude**, **no saturation (white/neutral) at
  zero**. [14 Fig. 1c] [15] describes the same construction as three hues
  (blue-white-red), which makes the low and high ends distinct.
- Warning: some software applies a diverging map by default. On data with no
  zero crossing, increasing values may not get increasing saturation, which
  misrepresents the data. [14 Fig. 1e]
- [R6]: diverging maps show deviation from a median-like reference.

### Diverging on one-signed data? (the sources disagree)

| Source | Statement |
|---|---|
| [14] Gehlenborg & Wong 2012 | A default diverging map "inadvertently applied to data ranges without a zero crossing" can misrepresent the data. Choose the map type for the data. |
| [40] Nielsen & Wong 2012 | For heat-map rows of (non-negative) read-coverage tracks, "Employing a divergent color gradient can help emphasize the extremes." |

**Default: [14].** Use a diverging map only around a meaningful center:
zero for differences and residuals, a reference value, a threshold.
**Exception ([40]):** when the goal is to separate highs from lows around a
chosen midpoint, a diverging map is acceptable *if you choose the midpoint
deliberately and state it* in the caption or colorbar.

Spectroscopy mapping (inference): difference spectra/maps (pumped −
unpumped, sample − reference) and fit residuals are signed around zero, so
use a diverging map centered at zero (`TwoSlopeNorm(vcenter=0)` or symmetric
limits). Raw RIXS/XAS intensity is one-signed, so use a sequential map.

## 6. Color is relative [11, 13, 15]

- The background changes how a color looks. The same swatch looks different
  on two backgrounds, and two different swatches can look alike (Albers).
  [11 Fig. 1]
- In heat maps, identical cells look different because of their neighbors.
  Don't expect readers to read values from cell colors. [11 Fig. 1c, 15]
  "Color is a relative medium and can be unreliable when used to represent
  discrete values." [15]
- Color can create size biases: equal areas in vibrant colors can look more
  different than equal areas in muted colors. [13]
- Overusing color creates clutter. [13]
- Pair a color map with line cuts when values matter: position beats color
  (inference from [28] and [15]).

## 7. Heat maps [15, 37, 34]

- Heat maps "rely fundamentally on color encoding and on meaningful
  reordering of the rows and columns". [15]
- Clustering reveals structure, but n rows linked by a cluster tree have
  2^(n−1) possible orderings, so one static map is one of many outcomes, and
  the linear order can place distant relatives side by side. Insert gaps
  that follow the tree (gap maps). [15]
- If one axis is inherently ordered (time, dose, energy, temperature), keep
  it in order and cluster only the other axis. [15] Row and column order can
  both reveal and hide patterns. [34]
- For ordered columns, parallel coordinates are a good alternative: spatial
  encoding is more accurate and small discrepancies stand out. Beyond "a few
  dozen profiles" the lines blur. [15]
- Reorder adjacency matrices so filled cells sit together: clusters become
  diagonal blocks and hubs become full rows. [37]
- Heat-map rows are compact but weak for quantitative reading. They are best
  for broad high vs low ranges. [40]

## 8. Checks before you publish

1. **Grayscale check**: convert the figure (or the key) to grayscale.
   Categories must stay distinct and none may look under-represented.
   [11, 12, 13]
2. **Color-blindness simulation**: protanopia and deuteranopia. [12]
3. **Squint test**: visibility should be even across categories [11], and
   what stands out should be what matters [08].
4. Does the colormap make unimportant values (background, lows) the most
   salient? [08]
5. Is the map class right: sequential for one-signed, diverging only around
   a stated center, categorical for classes? [14, R6]
