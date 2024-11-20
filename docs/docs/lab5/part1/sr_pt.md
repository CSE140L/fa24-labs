---
title: PT-FF to SR-FF
grand_parent: Lab 5
parent: Part 1
layout: katex
nav_order: 3
---

# Making a SR-FF with a PT-FF
{: .no_toc}

## Contents
{: .no_toc .text-delta}

1. TOC
{:toc}

---

## Implementation Guidelines

Now that you have created a PT flip-flop using a JK flip-flop which was essentially created from an SR flip-flop, let us circle back and use the PT flip-flop to create an SR flip-flop.

Even though the PT flip-flop is complete, it doesn’t have the desirable property of generating the excitation table that captures all the transitions through the simple and convenient mechanism of don’t cares, similar to a JK flip-flop.
For example, for the transition from $Q = 1$ to $Q_{\text{next}} = 1$ to be excited, the condition is either {$P=0$ and $T=0$} or {$P=1$ and $T=1$}, which cannot be captured by one designation in the excitation table.
Please fill in the remaining excitation table.
If the condition cannot be captured by one designation, use "/" to separate the cases.

### Table 1

{: .text-delta}
PT Flip-Flop Excitation Table

|$\boldsymbol{Q}$ | $\boldsymbol{Q_{\text{next}}}$ | $\boldsymbol{P}$ | $\boldsymbol{T}$ | 
|:---:|:---:|:---:|:---:|
| $0$ | $0$ |     |     |
| $0$ | $1$ |     |     |
| $1$ | $0$ |     |     |
| $1$ | $1$ | 0/1 | 0/1 |

If such a transition occurs for only one $S$ and $R$ input combination, the identification of the optimal solution would necessitate two pairs of K-maps for $P$ and $T$: one where we choose the first excitation condition (such as $P=0$ and $T=0$) and one where we choose the second (such as $P=1$ and $T=1$).

As such situations could in all likelihood proliferate for multiple $J$ and $K$ input combinations, one can see that the problem of the identification of minimality ends up turning into an exponentially growing quest.

You should be able to implement this using **no more than one additional AND/OR gate**.
Use the PT-FF you created from the previous part here.

## Deliverables

{: .highlight-title}
> Lab Report
>
> Please include a filled in [table 1](#table-1) in the lab report.
> Please include the K-maps for $P$ and $T$ that can be implemented (not provided) with the minimum number of AND/OR gates.

Please submit the schematic `SRFF.dig` with the following pinout:

| Port Direction | Port Name  | Active | Port Width (bits) |
|:--------------:|------------|--------|------------------:|
|      INPUT     | `S`        |   -    |                 1 |
|      INPUT     | `R`        |   -    |                 1 |
|      INPUT     | `CLK`      | High   |                 1 |
|     OUTPUT     | `Q`        |   -    |                 1 |
|     OUTPUT     | `QN`       |   -    |                 1 |
