---
layout: page
title: Lecture notes on bacterial chemotaxis
---

## Modeling Signal Transduction in Bacterial Chemotaxis

Chemotaxis is the directed movement of cells or organisms along a chemical concentration gradient. For a cell to navigate such a gradient, it must first be able to sense it. While some larger eukaryotic cells, such as neutrophils or amoebae, are large enough to measure spatial concentration differences across the length of their cell bodies, bacteria face a fundamental physical constraint.

![E. coli](ecoli.png)

A typical *Escherichia coli* cell is approximately 2 µm long and 0.5 µm wide. At this microscopic scale, the difference in chemoattractant concentration between the front and the back of the bacterium is so minute that it is completely drowned out by the stochastic noise of molecules binding to its surface receptors. In a [classic 1977 biophysics paper](https://www.sciencedirect.com/science/article/pii/S0006349577855446?via%3Dihub), Howard Berg and Edward Purcell formally demonstrated that bacteria are simply too small to sense spatial gradients directly.

Because spatial sensing is unfeasible, *E. coli* must sense gradients in time. The bacterium must compare the concentration of its current environment to the concentration it experienced a moment ago. This temporal comparison requires the biochemical equivalent of a short-term memory.

### Locomotion: Runs and Tumbles

To act on this temporal information, *E. coli* must physically move. The bacterium propels itself using several rotating flagella (typically around five) extending from its body. The cell's movement is dictated entirely by the rotational direction of these flagella:

- **The "Run":** By default, all flagella rotate counter-clockwise (CCW). When rotating in this direction, the flagella wrap together to form a tight bundle, propelling the bacterium smoothly forward in a straight line.
- **The "Tumble":** If even a single flagellum reverses its rotation to clockwise (CW), the bundle breaks apart. The flagella splay outward in different directions, bringing the forward run to a halt and causing the bacterium to randomly tumble in place.

### The Biased Random Walk

![Random walk](random_walk.svg)

In a homogeneous environment with no chemical gradients, *E. coli* alternates continuously between these two states (typically running for about 1 second and tumbling for 0.1 seconds), executing a purely stochastic random walk. After each tumble, the bacterium faces a new, random direction for its next run.

However, when a nutrient gradient is present, the bacterium modulates this behavior. If the cell senses that the attractant concentration is increasing over time (meaning it is swimming up the gradient), it actively suppresses the tumbling frequency (*f*<sub>tumble</sub> goes down). By tumbling less when moving in a favorable direction, the cell extends its productive runs. This simple suppression transforms the standard random walk into a biased random walk, allowing the bacterial population to gradually drift toward the food source.
