---
layout: page
title: Lecture notes on bacterial chemotaxis
math: true
---

## Modeling Signal Transduction in Bacterial Chemotaxis

Chemotaxis is the directed movement of cells or organisms along a chemical concentration gradient. For a cell to navigate such a gradient, it must first be able to sense it. While some larger eukaryotic cells, such as neutrophils or amoebae, are large enough to measure spatial concentration differences across the length of their cell bodies, bacteria face a fundamental physical constraint.

<figure>
  <img src="ecoli.png" alt="E. coli">
  <figcaption>An <em>E. coli</em> cell, roughly 2 µm long and 0.5 µm wide, propelled by a bundle of rotating flagella.</figcaption>
</figure>

A typical *Escherichia coli* cell is approximately 2 µm long and 0.5 µm wide. At this microscopic scale, the difference in chemoattractant concentration between the front and the back of the bacterium is so minute that it is completely drowned out by the stochastic noise of molecules binding to its surface receptors. In a [classic 1977 biophysics paper](https://www.sciencedirect.com/science/article/pii/S0006349577855446?via%3Dihub), Howard Berg and Edward Purcell formally demonstrated that bacteria are simply too small to sense spatial gradients directly.

Because spatial sensing is unfeasible, *E. coli* must sense gradients in time. The bacterium must compare the concentration of its current environment to the concentration it experienced a moment ago. This temporal comparison requires the biochemical equivalent of a short-term memory.

### Locomotion: Runs and Tumbles

To act on this temporal information, *E. coli* must physically move. The bacterium propels itself using several rotating flagella (typically around five) extending from its body. The cell's movement is dictated entirely by the rotational direction of these flagella:

- **The "Run":** By default, all flagella rotate counter-clockwise (CCW). When rotating in this direction, the flagella wrap together to form a tight bundle, propelling the bacterium smoothly forward in a straight line.
- **The "Tumble":** If even a single flagellum reverses its rotation to clockwise (CW), the bundle breaks apart. The flagella splay outward in different directions, bringing the forward run to a halt and causing the bacterium to randomly tumble in place.

### The Biased Random Walk

<figure>
  <img src="random_walk.svg" alt="Random walk trajectory of E. coli">
  <figcaption>An <em>E. coli</em> trajectory consisting of straight runs interrupted by tumbles that randomly reorient the next run. In a homogeneous environment this produces an unbiased random walk; in a gradient, suppressed tumbling during favorable runs biases the walk toward the source.</figcaption>
</figure>

In a homogeneous environment with no chemical gradients, *E. coli* alternates continuously between these two states (typically running for about 1 second and tumbling for 0.1 seconds), executing a purely stochastic random walk. After each tumble, the bacterium faces a new, random direction for its next run.

However, when a nutrient gradient is present, the bacterium modulates this behavior. If the cell senses that the attractant concentration is increasing over time (meaning it is swimming up the gradient), it actively suppresses the tumbling frequency ($$f_{\text{tumble}}$$ goes down). By tumbling less when moving in a favorable direction, the cell extends its productive runs. This simple suppression transforms the standard random walk into a biased random walk, allowing the bacterial population to gradually drift toward the food source.

### Inside the Cell: The (simplified!) signaling network

To understand how *E. coli* successfully modulates its tumbling frequency, we must look inside the cell at the molecular components of the chemotaxis machinery. This system consists of three primary parts: transmembrane receptors that detect the attractant, an intracellular signaling network that processes the information, and the flagellar motor that executes the physical output.

<figure>
  <img src="inside_ecoli.svg" alt="Simplified schematic of the E. coli chemotaxis signaling network">
  <figcaption><strong>Heavily simplified</strong> schematic of the chemotaxis signaling network: transmembrane receptors detect attractant, the active receptor state phosphorylates CheY, and CheY-P binds the flagellar motor to switch its rotation. The real network includes additional components (CheA, CheW, CheR, CheB, CheZ) and feedback loops that are omitted here for clarity.</figcaption>
</figure>

The signaling process begins at the cell surface with transmembrane receptors. These receptor proteins feature a ligand-binding domain extending into the extracellular environment and a long signaling domain reaching into the cytoplasm. The receptors are dynamic, constantly shifting between an "active" and an "inactive" structural conformation.

Somewhat counter-intuitively, the binding of a chemoattractant ligand to the outside of the receptor increases the probability that the receptor will enter the inactive state. The relationship between ligand concentration and receptor activity follows a steep Hill-curve: in a ligand-free environment, the receptors are highly active, but as ligand concentration increases, receptor activity plummets.

<figure>
  <img src="response1.svg" alt="Hill-curve response of receptor activity to ligand concentration">
  <figcaption>Receptor activity as a function of ligand concentration. Increasing ligand concentration drives the receptor toward the inactive state along a steep Hill curve.</figcaption>
</figure>

When the cytoplasmic domain of a receptor is in the active state, it initiates a phosphorylation cascade. The active receptor facilitates the phosphorylation of a cytoplasmic signaling protein called CheY. Once phosphorylated, the resulting CheY-P molecules diffuse rapidly through the cell body until they reach the motor complexes at the base of the flagella.

Upon binding to the motor complex, CheY-P acts as the molecular trigger that forces the motor to switch from its default counter-clockwise rotation (which promotes smooth running) to a clockwise rotation.

By connecting these components, we can understand the cell's baseline logic:

- **Without attractant:** Receptors are mostly active, leading to high levels of CheY-P production. This abundant CheY-P binds to the motors, causing frequent clockwise rotation and resulting in a high tumbling frequency.
- **With attractant:** Ligand binding shifts the receptors into the inactive state, halting the production of CheY-P. Without CheY-P to trigger clockwise rotation, the motors maintain their default counter-clockwise state, suppressing tumbling and extending the cell's runs.

Through this relatively simple pathway, the bacterium successfully translates the extracellular ligand concentration into a direct, mechanical behavioral output (tumbling frequency).

### The Phenomenon of Exact Adaptation

If we only consider the basic receptor-to-motor signaling pathway, we might expect that a sudden, permanent increase in attractant concentration would lead to a permanent decrease in tumbling frequency. However, experimental observations reveal a much more sophisticated dynamic.

<figure>
  <img src="adaptation.svg" alt="Tumbling frequency response to a step in ligand concentration, showing exact adaptation">
  <figcaption>Response of the tumbling frequency to a sudden change in ligand concentration. The frequency drops (or spikes) within milliseconds and then recovers exactly back to its pre-stimulus baseline over the course of minutes — the hallmark of <em>exact adaptation</em>.</figcaption>
</figure>

When *E. coli* is exposed to a sudden step-increase in ligand concentration, the tumbling frequency (and the concentration of CheY-P) drops incredibly fast — within approximately 200 microseconds. But rather than staying at this new, low level, the tumbling frequency slowly recovers over the next several minutes, eventually returning to the exact same baseline value it had before the attractant was added. This occurs even though the bacterium remains in the higher food concentration.

A similar but inverted process happens if the ligand concentration is suddenly reduced: the tumbling frequency immediately spikes, but mysteriously recovers back to the original baseline.

This behavior is known as *exact adaptation*. It serves a critical evolutionary purpose: by constantly resetting its baseline activity, the cell ensures it never becomes blind or saturated in high-nutrient environments. Because the tumbling frequency always returns to its set point, the bacterium is always ready to respond to further increases or decreases in attractant.

### Methylation: The Molecular Memory

The mathematical necessity here is two-fold: *E. coli* must possess a memory mechanism to perform a biased random walk over time, and it must maintain a constant steady-state tumbling frequency irrespective of the absolute ligand concentration.

The cell elegantly solves both problems using methyl-accepting receptors. In addition to binding ligands on the outside of the cell, these transmembrane receptors can be modified on the inside of the cell through the addition of methyl groups.

These methyl groups act as molecular tuning dials that fundamentally change the excitability of the receptor. Adding a methyl group heavily biases the receptor toward the active state. If we compare the activity profiles of an unmethylated versus a methylated receptor, the addition of the methyl group shifts the response curve significantly to the right.

<figure>
  <img src="response2.svg" alt="Receptor activity vs. ligand concentration for unmethylated and methylated receptors">
  <figcaption>Adding methyl groups shifts the receptor's response curve to the right. At an intermediate ligand concentration, an unmethylated receptor is fully repressed while a methylated receptor remains active — methylation effectively re-tunes the receptor's operating range.</figcaption>
</figure>

Consequently, at an intermediate ligand concentration where an unmethylated receptor would be completely repressed (inactive), a heavily methylated receptor maintains a high level of activity, leading to more CheY-P production and more tumbling events. This dynamic chemical tagging is what physically stores the "memory" of the cell's recent environment.

### The Barkai-Leibler Model of Exact Adaptation

To understand how the dynamic addition and removal of methyl groups stores information and ensures a robust steady-state tumbling frequency, we can look to a famous mathematical model proposed by Naama Barkai and Stanislav Leibler in 1997.

The Barkai-Leibler model isolates the core components of the chemotaxis network into a simplified system. In this model, we start with an unmethylated receptor ($$T$$). For simplicity, the model assumes the unmethylated receptor cannot easily enter the active state.

The system is governed by two opposing enzymes and a stark separation of timescales:

- **Methylation (slow):** An enzyme called CheR constantly adds methyl groups to the unmethylated receptors, converting them into the methylated form ($$T_m$$).
- **Ligand binding (fast):** Once methylated, the receptor can rapidly fluctuate between an inactive state ($$T_m$$) and an active state ($$T_m^*$$). As established earlier, the active state ($$T_m^*$$) leads to CheY phosphorylation and subsequent tumbling. The binding of an attractant ligand ($$L$$) rapidly shifts this equilibrium, forcing the receptors into the inactive $$T_m$$ state. This switching occurs on the order of milliseconds.
- **Demethylation (slow):** A second enzyme, CheB, removes methyl groups from the receptors. However, in the Barkai-Leibler model, there is a strict rule: CheB only demethylates receptors that are currently in the active state ($$T_m^*$$). Both methylation and demethylation occur slowly, on the order of tens of seconds.

<figure>
  <img src="Barkai_Leibler.svg" alt="Schematic of the Barkai-Leibler model: methylation by CheR, ligand-driven switching between T_m and T_m*, and active-state-only demethylation by CheB">
  <figcaption>The Barkai-Leibler model. CheR methylates receptors at a constant, saturated rate. The methylated receptor switches rapidly between an inactive state \(T_m\) and an active state \(T_m^*\), with ligand binding driving it toward \(T_m\). CheB demethylates only receptors in the active state \(T_m^*\).</figcaption>
</figure>

#### The Mathematics of Memory

Because $$T_m^*$$ is the only state that triggers tumbling, the total number of $$T_m^*$$ receptors serves as a direct proxy for the cell's physical activity. To understand how the cell adapts, we evaluate how the total pool of methylated receptors ($$T_m + T_m^*$$) changes over time.

The change in methylated receptors per unit of time is equal to the rate of methylation minus the rate of demethylation. Assuming there are vastly more receptors than CheR molecules, CheR works at a constant, saturated rate ($$\rho \cdot \mathrm{CheR}$$). Demethylation by CheB relies on Michaelis-Menten kinetics, where the rate depends on the availability of its specific substrate, the active receptor ($$T_m^*$$).

We can write this as a differential equation:

$$
\frac{d(T_m + T_m^*)}{dt} = \rho \cdot \mathrm{CheR} - \frac{\beta \cdot \mathrm{CheB} \cdot T_m^*}{K + T_m^*}
$$

To find the baseline activity of the cell after it has fully adapted to a new environment, we must solve for the steady state. By definition, in a steady state, the number of methylated receptors is no longer changing, so we set the derivative to zero:

$$
0 = \rho \cdot \mathrm{CheR} - \frac{\beta \cdot \mathrm{CheB} \cdot T_{m,\mathrm{st}}^*}{K + T_{m,\mathrm{st}}^*}
$$

If we rearrange this equation to solve for the steady-state number of active receptors ($$T_{m,\mathrm{st}}^*$$), we get:

$$
T_{m,\mathrm{st}}^* = \frac{K \cdot \rho \cdot \mathrm{CheR}}{\beta \cdot \mathrm{CheB} - \rho \cdot \mathrm{CheR}}
$$

The brilliance of the Barkai-Leibler model is revealed in that final equation. Notice what variable is completely absent: the ligand concentration ($$L$$).

This works precisely because CheB is constrained to demethylate **only the active receptors $$T_m^*$$**. That asymmetry closes a negative feedback loop: $$T_m^*$$ — the very output we want to regulate — is also the substrate that sets the rate at which methyl groups are stripped, so any rise in activity automatically accelerates the process that returns it to baseline. Had CheB demethylated all methylated receptors indiscriminately, the demethylation rate would no longer track activity, and the steady state would once again depend on ligand concentration. The seemingly arbitrary substrate specificity of CheB is therefore the structural origin of exact adaptation.

The number of active receptors at steady state thus depends entirely on biochemical constants (the rate constants $$\rho$$ and $$\beta$$, the Michaelis constant $$K$$) and the total numbers of the CheR and CheB enzymes inside the cell. Because the steady-state activity is decoupled from $$L$$, the mathematical model perfectly mirrors the experimental observation: the cell's tumbling frequency will always return to the exact same set point, regardless of how much attractant is in the surrounding environment.
