---
epoch: 1794677358497
mode: agent
backendId: codex
sessionId: "01a1db1b-049e-7422-b0df-ac38a6527191"
agentLabel: "explain 6.11 from my notes. The energy gap"
tags:
  - copilot-conversation
usage: '{"usedTokens":28816,"contextWindow":828400,"updatedAt":1794677387313}'
---

**user**: explain 6.11 from my notes. The energy gap
[Timestamp: 2026/11/14 22:59:18]

**ai**: I’ll locate section 6.11 in your attached materials-science notes and explain it using the notation used there.In [[notes]], §6.11 explains why the free-electron $E$–$k$ parabola develops forbidden energy gaps in a crystal.

Electrons behave as waves. When their wavelength satisfies the Bragg condition for atom spacing $d$,

$$
\lambda = 2d,\ d,\ \frac{2d}{3},\ldots
$$

or equivalently,

$$
k=\pm\frac{n\pi}{d},
$$

the electron waves are strongly reflected by successive atoms. Forward and reflected waves combine into a standing wave, so the electron has zero net velocity along that direction.

Two standing waves are possible at the same $k$:

- A cosine wave has high electron probability at positive ion cores. Since an electron is attracted to the cores, this state has lower potential energy.
- A sine wave has high probability between ion cores, where the electron has higher potential energy.

In the free-electron model, these two waves would have the same energy. The crystal’s periodic potential splits them:

$$
\Delta E_{\text{gap}}=E_{\text{sine}}-E_{\text{cosine}}.
$$

This split is the **energy gap**. There are no allowed electron states in the energy interval between the lower cosine state and higher sine state. Thus, the original smooth $E$–$k$ curve breaks at $k=\pm n\pi/d$ into separate allowed bands.

The key causal chain is:

$$
\text{periodic ion arrangement}
\rightarrow
\text{Bragg reflection}
\rightarrow
\text{standing waves}
\rightarrow
\text{different localization relative to ions}
\rightarrow
\text{different potential energies}
\rightarrow
\text{energy gap}.
$$

A larger variation in potential energy from ion core to interstitial region produces a larger $E_g$. That is why a strongly bound covalent solid such as diamond has a large gap, while materials with weaker position-dependent binding can have smaller gaps or no gap.
[Timestamp: 2026/11/14 22:59:18]