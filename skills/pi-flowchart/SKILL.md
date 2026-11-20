---
name: pi-flowchart
description: Create or restyle standalone HTML flowcharts with a visual style inspired by pi.dev. Use when the user asks for Pi website styling on a process, decision tree, or workflow diagram, including Pi study notes.
---

# Pi Flowchart

Turn the requested workflow into a browser-ready HTML diagram using the visual language of the Pi website.

1. Extract the steps, decision conditions, outcomes, and return paths from the request or supplied material. Use short action labels for steps and questions for decisions. Label each outgoing decision path with its condition. For Pi commands or behavior that the user has not supplied, verify the details against the [Pi documentation](https://docs.pi.dev/).
2. Read [the visual reference](references/visual-style.md) before styling. Use [the standalone session-branching example](assets/session-branching.html) to start a new page or to see how the style and branching layout work together. For an existing HTML page, apply the style to its diagram and preserve the surrounding layout and behavior.
3. Use the simplest layout that shows the full flow. Use an ordered list for a straight sequence and HTML node cards with directional connectors for branches. Keep node text selectable and readable at narrow widths. When spatial relationships carry information the markup cannot convey, provide an equivalent text description of the routes. Follow the requested content language.
4. For a standalone diagram, save one `.html` file with embedded CSS and any necessary scripts. Use offline-ready assets and the requested filename when provided. Open the output in a browser when available and check a narrow and a wide viewport for clipped text, misplaced arrows, and ambiguous branches. Return the file path.
