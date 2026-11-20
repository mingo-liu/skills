# Visual Style

The reference is the [official Pi homepage](https://pi.dev/). Its cool ink-blue and warm paper surfaces, serif typography, terminal monospace, faint square grid, and slate-blue accents translate well to a diagram. Use those cues in an original diagram layout with system fonts and CSS-drawn details.

## Palette

| Role | Dark | Light |
| --- | --- | --- |
| Page | `#0d1116` | `#ebe7e4` |
| Diagram canvas | `#161d27` | `#eef1f3` |
| Node surface | `#212730` | `#f4f2f0` |
| Emphasized node | `#252f3d` | `#e4e9ef` |
| Main text | `#ebe7e4` | `#252f3d` |
| Secondary text | `#9fa4ab` | `#5c5752` |
| Subtle rule | `#495059` | `#bdb3ac` |
| Accent | `#6a9fcc` | `#4b607c` |

These are adapted from the homepage palette. For a new standalone chart, follow the system color preference unless the user requests a theme. For an existing page, match its theme. Set `color-scheme` to match the active palette. Use the accent or another sufficiently contrasting tone for connector lines and labels. Reserve subtle rules for framing.

## Typography and Layout

- Set the title in Georgia or a similar locally available serif. Use a system monospace stack for commands, decision labels, and short metadata. Use the serif for supporting sentences and let the browser choose local fallbacks for other scripts.
- Give the chart its own framed panel beneath a concise title. A low-contrast square grid at about 20 px spacing can add texture inside the panel. Keep node surfaces opaque so the grid stays behind the diagram.
- Use slim borders and modest corner radii for terminal-like cards. Give decision cards an accent rule and a visible question. Put branch conditions alongside orthogonal connectors and point arrowheads toward their destination. Keep long return paths outside the reading lanes and label where they lead.
- Let cards grow with their text. Reflow branches into labeled lanes when they can no longer sit comfortably side by side. Check that connectors meet the intended nodes after wrapping and that the text alone explains each choice.
