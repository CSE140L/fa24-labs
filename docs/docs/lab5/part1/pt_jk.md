---
title: JK-FF to PT-FF
grand_parent: Lab 5
parent: Part 1
layout: katex
nav_order: 2
---

# Making a PT-FF with a JK-FF
{: .no_toc}

## Contents
{: .no_toc .text-delta}

1. TOC
{:toc}

---

## Implementation Guidelines

JK flip-flops are *complete* flip-flops where each of the 4 possible functions, namely set (1), reset (0), hold ($Q$), and toggle ($\overline{Q}$), appears once in its characteristic table.
When these four functions exist in the characteristic table of a flip-flop, each transition can be excited by exactly two of them, leading hopefully to don’t cares in its excitation table.

Now that you crafted a D-FF from an SR-FF you quickly realize that one can create many other complete flip-flops by simply shuffling the assignment of operations to rows of the characteristic table.
For example, let’s call the flip-flop below a PT flip-flop.


### Table 1

{: .text-delta}
PT Flip-Flop Characteristic Table

| $\boldsymbol{P}$ | $\boldsymbol{T}$ | $\boldsymbol{Q}$ | $\boldsymbol{\overline{Q}}$ | Function |
|:---:|:---:|:---:|:---:|---|
| $0$ | $0$ | $Q$ | $\overline{Q}$  | |
| $0$ | $1$ | $0$ | $1$  | |
| $1$ | $0$ | $\overline{Q}$ | $Q$  | |
| $1$ | $1$ | $1$ | $0$  | |

You can see that the PT flip-flop is complete.
In order to implement a PT flip-flop, you will take the $P$ and $T$ signals, and create the appropriate glue logic to build it using a JK flip-flop.
For your convenience, the excitation table of the JK flip-flop is shown in [Table 2](#table-2).

### Table 2

{: .text-delta}
JK Flip-Flop Excitation Table

|$\boldsymbol{Q}$ | $\boldsymbol{Q_{\text{next}}}$ | $\boldsymbol{J}$ | $\boldsymbol{K}$ | 
|:---:|:---:|:---:|:----:|
| $0$ | $0$ | $0$ |  X   |
| $0$ | $1$ | $1$ |  X   |
| $1$ | $0$ |  X  | $1$  |
| $1$ | $1$ |  X  | $0$  |

You should be able to implement this with **one logic gate**.

## Deliverables

{: .highlight-title}
> Lab Report
>
> Please fill in the function field of [table 1](#table-1) with the 4 possible functions (set, reset, hold, or toggle).

Please submit the schematic `PTFF.dig` with the following pinout:

| Port Direction | Port Name  | Active | Port Width (bits) |
|:--------------:|------------|--------|------------------:|
|      INPUT     | `P`        |   -    |                 1 |
|      INPUT     | `T`        |   -    |                 1 |
|      INPUT     | `CLK`      | High   |                 1 |
|     OUTPUT     | `Q`        |   -    |                 1 |
|     OUTPUT     | `QN`       |   -    |                 1 |
