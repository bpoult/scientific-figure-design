# Matplotlib recipes (compose with python-plotting-style)

The sources give no matplotlib code, so **every recipe here is an
Extension**; the numbers come from the cited columns. Tested with matplotlib
3.8 (BIP env). House rules still apply (`colors` + imports atop every block,
`constrained_layout`, `savefig`, RIXS labels, fitting). Assumed header:

```python
import numpy as np
import matplotlib as mpl
import matplotlib.pyplot as plt
from matplotlib.colors import LogNorm, TwoSlopeNorm, CenteredNorm, LinearSegmentedColormap
colors = ['#000000', '#E69F00', '#56B4E9', '#009E73', '#F0E442', '#0072B2', '#D55E00', '#CC79A7']
```

## 1. Medium presets (replace house bold/grid/legend defaults)

Point sizes are print values [17, 20]: build at final width, or pass
`scale = figure width / printed width` (house `(6, 4)` in a 3.5-in column →
`6 / 3.5`). Paper/talk sizes are inferences ([R3] says only "thicker",
"bigger"); poster follows the house table.

```python
def medium_rc(medium='paper', scale=1.0):
    """rcParams for publication figures. scale = fig width / printed width."""
    tick, label, ax_lw, line_lw, ms = {'paper': (7, 8, 0.5, 1.0, 3),   # 0.5 pt [17]
                                       'talk': (16, 20, 1.0, 2.5, 7),
                                       'poster': (26, 28, 1.5, 3.0, 9)}[medium]
    s = scale
    return {'font.family': 'sans-serif', 'font.size': tick * s,     # one face [16]
            'xtick.labelsize': tick * s, 'ytick.labelsize': tick * s,
            'legend.fontsize': tick * s, 'axes.labelsize': label * s,
            'axes.titlesize': label * s,                            # 2 sizes [16]
            'axes.labelweight': 'normal', 'axes.titleweight': 'normal',
            'axes.linewidth': ax_lw * s, 'xtick.major.width': ax_lw * s,
            'ytick.major.width': ax_lw * s, 'lines.linewidth': line_lw * s,
            'lines.markersize': ms * s,
            'axes.spines.top': False, 'axes.spines.right': False,   # no box [17]
            'axes.grid': False, 'axes.axisbelow': True,             # grid if needed
            'grid.color': 'k', 'grid.alpha': 0.15, 'grid.linewidth': ax_lw * s,
            'legend.frameon': False, 'axes.prop_cycle': mpl.cycler(color=colors)}

with plt.rc_context(medium_rc('paper', scale=6 / 3.5)):
    fig, ax = plt.subplots(figsize=(6, 4), constrained_layout=True)
```

Talk: no vertical text [R3]; put the y label on top as
`ax.set_title('Intensity (arb. units)', loc='left')`.

## 2. Axes, ticks, grid [17, 21]

```python
def nav_style(ax, grid=None, grid_alpha=0.15):
    """grid=None (default), 'y', 'x' or 'both'. alpha 0.15 sparse -> 0.45 dense."""
    ax.spines[['top', 'right']].set_visible(False)
    ax.grid(False)
    if grid:                                        # behind the data, major only
        ax.grid(True, axis=grid, which='major', color='k', alpha=grid_alpha, lw=0.5)
        ax.set_axisbelow(True)
    ax.locator_params(nbins=5)                      # few ticks [17, R Fig. 7]
```
- No axis arrows. Drop repeated digits by changing units [17]: plot `E - E0`
  as `'$E - E_0$ (eV)'` (name E0), or rescale into the unit,
  `'Counts (10$^3$)'`. Log axes and breaks only if clearly stated [24].

## 3. Shared scales and aligned labels [17, 36]

`plt.subplots(3, 1, sharex=True, sharey=True, constrained_layout=True)` then
`fig.align_ylabels(axs)`. Use `sharey=False` only on purpose and say so in
the caption [24]. Panel max with a global minimum [24]:
`for ax, y in zip(axs, Y): ax.set_ylim(global_min, y.max() * 1.05)`.

## 4. Data + residual panel (curve-gap fix; inference from [28])

Under `constrained_layout`, `hspace=0` still leaves a gap (checked); use
`make_axes_locatable` for flush panels.
```python
from mpl_toolkits.axes_grid1 import make_axes_locatable
fig, ax = plt.subplots(figsize=(6, 4), constrained_layout=True)
ax.plot(x, y, 'o', mfc='none', mec='k', mew=0.5, ms=3)        # open circles [19]
ax.plot(x, yfit, color=colors[6])
res = make_axes_locatable(ax).append_axes('bottom', size='30%', pad=0, sharex=ax)
res.plot(x, y - yfit, color='k', lw=0.75); res.axhline(0, color='0.5', lw=0.5)
ax.tick_params(labelbottom=False); res.set_xlabel('Energy (eV)')
ax.set_ylabel('Intensity (arb. units)'); res.set_ylabel('Resid.')
for a in (ax, res):                       # align_ylabels misses appended axes
    a.yaxis.set_label_coords(-0.12, 0.5)
```

## 5. Grouping by spacing: tight within, wide between [05, 07]

```python
fig = plt.figure(figsize=(7, 4), constrained_layout=True)
fig.get_layout_engine().set(w_pad=2 / 72, h_pad=2 / 72, wspace=0, hspace=0)
left, right = fig.subfigures(1, 2, wspace=0.08)        # gap BETWEEN groups
axl = left.subplots(2, 1, sharex=True, sharey=True)    # tight WITHIN group
axr = right.subplots(2, 1, sharex=True, sharey=True)
```
A series (temperature, dose) → one row or column in physical order, not an
even 2x2 grid [05]. Panel letters at one axes-fraction position (house).

## 6. Direct labels and callouts [18, R Fig. 7]

```python
def label_line(ax, line, x_at, text=None, dx=4, ha='left'):
    """Label a line in its own color at x_at, fixed offset dx (points)."""
    xd, yd = line.get_data()
    ax.annotate(text or line.get_label(), xy=(x_at, np.interp(x_at, xd, yd)),
                xytext=(dx, 0), textcoords='offset points',
                ha=ha, va='center', color=line.get_color())

def callout(ax, x, y, text, d=8):
    """Headless leader at a fixed 45 deg (dx = dy) and fixed length [18, 20]."""
    ax.annotate(text, xy=(x, y), xytext=(d, d), textcoords='offset points', ha='left',
                va='bottom', arrowprops=dict(arrowstyle='-', lw=0.5, color='0.3', shrinkB=2))
```
Same `d` for every callout; `(d, 0)` for horizontal leaders. On collision,
move to the next position in one fixed priority order [18]. No bbox bubbles.
If a legend is needed: `ax.legend(frameon=False)`, off the data.

## 7. Markers [19]

One dense series: `'o', mfc='none', mec='k', mew=0.5`. Several: open `'o'`,
`'+'`, open `'s'`, filled `'o'`, `'x'`; not only `'^' 'v' 'D' 's' 'p'`; no
`'*'`. `scatter(s=...)` is **area** (pt²): map values linearly to `s`, not
via a squared radius [R Fig. 6]. Prefer position to size [28].

## 8. One highlight over gray context [29, 31, 24, R6]

```python
def highlight_over_gray(ax, x, Y, focus, color=colors[5]):
    for i, y in enumerate(Y):
        if i != focus:
            ax.plot(x, y, color='0.8', lw=0.75, zorder=1)
    return ax.plot(x, Y[focus], color=color, lw=1.5, zorder=3)[0]
```
Fits: data black, the discussed component in one color, others light gray.

## 9. Small multiples [24, 36, 19]

```python
def small_multiples(x, Y, labels, ncols=1, sharey=True, panel=(3.0, 1.0), context=True):
    n = len(Y); nrows = -(-n // ncols)
    fig, axs = plt.subplots(nrows, ncols, sharex=True, sharey=sharey, squeeze=False,
                            figsize=(panel[0] * ncols, panel[1] * nrows),
                            constrained_layout=True)
    for i, ax in enumerate(axs.flat):
        ax.set_visible(i < n)
        for j, y in enumerate(Y[:n] if (context and i < n) else []):
            if j != i: ax.plot(x, y, color='0.85', lw=0.5, zorder=1)   # context [24]
        if i < n:
            ax.plot(x, Y[i], color='k', lw=1.0, zorder=3)
            ax.text(0.01, 0.95, labels[i], transform=ax.transAxes, va='top')  # no legend
            ax.spines[['top', 'right']].set_visible(False)
    fig.align_ylabels(axs[:, 0])
    return fig, axs
```
Replaces house ">8 traces → dashed/dotted". Ordered series in ONE panel:
lightness ramp `plt.cm.viridis(np.linspace(0, 0.85, n))` (stops before yellow).

## 10. Offset (waterfall) plot (Extension; not covered by the sources)

An offset is a scale manipulation: state it [24]. Prefer an overlay (few
spectra, heights matter [40]) or small multiples (many spectra).
```python
def offset_plot(ax, x, Y, labels, offset, unit='arb. units'):
    """Constant offset, ordered ramp, direct labels at each baseline."""
    cols = plt.cm.viridis(np.linspace(0, 0.85, len(Y)))
    for i, (y, lab) in enumerate(zip(Y, labels)):     # Y sorted by the series variable
        base = i * offset
        ax.plot(x, y + base, color=cols[i], lw=1.0)
        ax.axhline(base, color=cols[i], lw=0.5, alpha=0.4, zorder=0)  # each zero
        ax.annotate(lab, xy=(x[-1], base), xytext=(4, 0), textcoords='offset points', va='bottom', color=cols[i])
    ax.set_ylabel(f'Intensity ({unit}), offset by {offset:g} per trace')
    ax.set_yticks([])        # ticks would mislead; add a scale bar if size matters
```
Use instead of house `plot_emission_waterfall`; repeat the offset in caption.

## 11. Colormaps and norms [14, 15, 31, R6]

```python
# One-signed intensity (RIXS/XAS map): sequential, monotonic lightness
pc = ax.pcolormesh(Ei, Et, I, cmap='viridis', norm=LogNorm(vmin=I[I > 0].min()))
fig.colorbar(pc, ax=ax, label='Intensity (arb. units, log scale)')
k10_90 = LinearSegmentedColormap.from_list('k10_90', ['0.9', '0.1'])  # sources' 10-90% black
# Signed difference / residual map: diverging, neutral at zero
pd = ax2.pcolormesh(Ei, Et, D, cmap='RdBu_r', norm=CenteredNorm(0, np.nanmax(np.abs(D))))
fig.colorbar(pd, ax=ax2, label=r'$\Delta$Intensity (arb. units)')
```
- Monotonic lightness: `viridis`, `cividis`, `Greys`, `Purples`, `Blues`.
  Not: `terrain_r`, `jet`, `rainbow`, `hsv` (`color.md` §4).
- `TwoSlopeNorm(vcenter=0, vmin=a, vmax=b)` with |a| ≠ |b| gives equal |Δ|
  unequal saturation. Prefer symmetric `CenteredNorm`, or state the
  asymmetry (inference).
- Set `vmin`/`vmax` on purpose (theoretical vs observed [14]); say which.
- Two channels: magenta + green [12]: `np.dstack([a, b, a])` (a → magenta,
  b → green, both 0-1). Heat maps: keep ordered axes in order [15].

## 12. Arrows and diagram edges [20, 25]

```python
from matplotlib.patches import ArrowStyle
HEAD = ArrowStyle('-|>', head_length=2.17, head_width=1.25)  # 2.5-pt equilateral [25]
ax.annotate('', xy=(x1, y1), xytext=(x0, y0), arrowprops=dict(arrowstyle=HEAD,
            mutation_scale=1, lw=0.5, color='k', shrinkA=2, shrinkB=2))  # end gaps [20]
```
`mutation_scale=1` puts the head in points (checked: 2.17 long, 2.5 wide).
[20]'s 0.75-pt stem + "60%" head is an Illustrator setting: `lw=0.75`, tune
the head by eye. Solid `'-|>'`, never open `'->'` [20].

## 13. Bars, boxes, aspect ratio [21, 24]

```python
ax.boxplot(groups, whis=1.5)        # caption: "whiskers: 1.5 x IQR" [21]
ax.bar(names, counts, color='0.4', edgecolor='none')  # counts; zero baseline [21]

def bank45(ax, x, y):
    """Median segment at 45 deg ([24] rule of thumb; median approximation)."""
    sx, sy = np.ptp(ax.get_xlim()), np.ptp(ax.get_ylim())
    s = np.abs(np.diff(y) / sy) / np.abs(np.diff(x) / sx)
    ax.set_box_aspect(1 / np.median(s[s > 0]))
```
`bank45`: trends and kinetics only, not mostly-flat peaky spectra (inference).

## 14. Checks before you send [11, 12, 13, R3]

```python
_lin = lambda c: np.where(c <= 0.04045, c / 12.92, ((c + 0.055) / 1.055) ** 2.4)

def lightness(cmap, n=11):
    """CIE L* along a colormap; must be monotonic for sequential data."""
    Y = _lin(plt.get_cmap(cmap)(np.linspace(0, 1, n))[:, :3]) @ [0.2126, 0.7152, 0.0722]
    return np.where(Y > 216 / 24389, 116 * np.cbrt(Y) - 16, Y * 24389 / 27)

_CVD = {'protan': [[0.152286, 1.052583, -0.204868], [0.114503, 0.786281, 0.099216],
                   [-0.003882, -0.048116, 1.051998]],
        'deutan': [[0.367322, 0.860646, -0.227968], [0.280085, 0.672501, 0.047413],
                   [-0.011820, 0.042940, 0.968881]]}   # Machado et al. 2009 (external)

def check_png(path, kind='deutan'):
    """Write <path>_<kind>.png for kind 'gray', 'protan' or 'deutan'."""
    from PIL import Image
    im, out = Image.open(path).convert('RGB'), path.replace('.png', f'_{kind}.png')
    if kind == 'gray':
        return im.convert('L').save(out)
    sim = np.clip(_lin(np.asarray(im, float) / 255) @ np.array(_CVD[kind]).T, 0, 1)
    srgb = np.where(sim <= 0.0031308, 12.92 * sim, 1.055 * sim ** (1 / 2.4) - 0.055)
    Image.fromarray((srgb * 255).round().astype(np.uint8)).save(out)
```
Then view the PNG at final size and as a thumbnail (squint test; CVD sim is approximate).
