# scientific-figure-design

A [Claude Code](https://docs.claude.com/en/docs/claude-code) skill that gives
Claude a design **method** and review **rubric** for publication-ready
scientific figures. It draws on the
[Nature Methods "Points of View" columns](https://communities.springernature.com/posts/data-visualization-a-view-of-every-points-of-view-column)
(Wong, Krzywinski, Gehlenborg, Streit et al., 2010-2016) and Rougier et al.
2014, "Ten Simple Rules for Better Figures".

## What it provides

- An 8-step design process: message and audience, variables, encodings and
  plot type, layout sketch, building with restraint, review, caption, and
  versions for each medium (paper, poster, talk).
- A yes/no publication checklist.
- Reference files that Claude loads only when it needs them:

| File | Topic |
| --- | --- |
| `references/principles.md` | Perception and composition |
| `references/color.md` | Categorical, sequential and diverging color; colorblind safety |
| `references/elements.md` | Typography, axes, ticks, grids, legends, labels |
| `references/plot-types.md` | Which plot answers which question |
| `references/workflow.md` | Sketching, exploratory vs explanatory figures, iteration |
| `references/matplotlib.md` | Matplotlib recipes that implement the method |
| `references/sources.md` | Full bibliography (41 columns plus Rougier) |

## Installation

Clone the repo into your Claude Code skills directory:

```bash
# personal (all projects)
git clone https://github.com/bpoult/scientific-figure-design.git ~/.claude/skills/scientific-figure-design

# or for a single project
git clone https://github.com/bpoult/scientific-figure-design.git .claude/skills/scientific-figure-design
```

Claude loads the skill on its own when a task involves designing or
reviewing a figure. You can also call it directly with
`/scientific-figure-design`.

## Companion skill

This skill is built to work alongside a `python-plotting-style` house-style
skill. For publication and poster figures, it overrides five named defaults
from that skill (see `SKILL.md`). If you don't have that skill, the method
and checklist still work on their own.

## License

[MIT](LICENSE)
