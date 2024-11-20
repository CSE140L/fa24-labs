---
title: SR-FF to D-FF
grand_parent: Lab 5
parent: Part 1
layout: katex
nav_order: 1
---

# Making a D-FF with an SR-FF
{: .no_toc}

## Contents
{: .no_toc .text-delta}

1. TOC
{:toc}

---

## Implementation Guidelines

An SR flip-flop takes in the values of the two inputs, Set ($S$) and Reset ($R$), at a definite portion of the clock cycle (such as the rising edge of the clock).
Depending on the state of these inputs, the output ($Q$) either sets to high (if $S$ is high) or resets to low (if $R$ is high).
If both $S$ and $R$ are low, the output retains its previous state.
If both $S$ and $R$ inputs are high simultaneously, this is typically considered an invalid condition for traditional SR flip-flops and can lead to unpredictable behavior.
The characteristic table of the SR flip-flop is shown below:

### Table 1

{: .text-delta}
SR Flip-Flop Characteristic Table

| $\boldsymbol{S}$ | $\boldsymbol{R}$ | $\boldsymbol{Q}$ | $\boldsymbol{\overline{Q}}$ |
|:---:|:---:|:---:|:---:|
| $0$ | $0$ | $Q$ | $\overline{Q}$  |
| $0$ | $1$ | $0$ | $1$  |
| $1$ | $0$ | $1$ | $0$  |
| $1$ | $1$ | $\color{red}1$ | $\color{red}1$  |

A D flip-flop can be viewed as a memory cell.
It captures the value of the D-input at a definite portion of the clock cycle (such as the rising edge of the clock).
That captured value becomes the $Q$ output.
The characteristic table of the D flip-flop is shown below:

### Table 2

{: .text-delta}
D Flip-Flop Characteristic Table

| $\boldsymbol{D}$ | $\boldsymbol{Q}$ | $\boldsymbol{\overline{Q}}$ |
|:---:|:---:|:---:|
| $0$ | $0$ | $1$  |
| $1$ | $1$ | $0$  |

In order to implement a D flip-flop, you will take the SR signals, and create the appropriate glue logic to build it using an SR flip-flop.
The simple excitation table of the SR flip-flop is shown in [Table 3](#table-3).
In an excitation table, we describe the inputs that are necessary to generate the transition from $Q$ to $Q_{\text{next}}$ (i.e. to "excite" the flip-flop to the next state).

### Table 3

{: .text-delta}
SR Flip-Flop Excitation Table

|$\boldsymbol{Q}$ | $\boldsymbol{Q_{\text{next}}}$ | $\boldsymbol{S}$ | $\boldsymbol{R}$ | 
|:---:|:---:|:---:|:----:|
| $0$ | $0$ | $0$ |  X   |
| $0$ | $1$ | $1$ | $0$  |
| $1$ | $0$ | $0$ | $1$  |
| $1$ | $1$ |  X  | $0$  |

Now that we know the appropriate SR signals to transform between any combination of values of $Q$ and $Q_{\text{next}}$, we shall use this to implement a D flip-flop.

For example, if $D = 0$ and $Q = 0$, we know from [Table 2](#table-2) that $Q_{\text{next}}$ shall also be 0.
Using the excitation table for the SR flip-flop, we know that such a transition from 0 to 0 happens when $S$ is a 0 and $R$ is a 0 or a 1.
Please fill in the $Q_{\text{next}}$ and SR values for the remaining combinations of $D$ and $Q$.

### K-Map 1

$Q_{\text{next}}$ given $D$ and $Q$.

| $\boldsymbol{D}$ \ $\boldsymbol{Q}$ | 0 | 1 |
|:------:|:--:|:--:|
| **0**      | 0  |    |
| **1**      |    |    |

### K-Map 2

SR values given $D$ and $Q$.

| $\boldsymbol{D}$ \ $\boldsymbol{Q}$ | 0 | 1 |
|:------:|:--:|:--:|
| **0**      | 0X |    |
| **1**      |    |    |

Select the minimum covers for the SR K-maps.
The function with inputs D and Q will be fed into the SR input of an SR flip-flop to induce the functionality of a D flip-flop.

You should implement this DFF **using no AND/OR logic gates (NOT gates only)**.
Please use the `RS-Flip-Flop, clocked` component from *Digital* for the SR-FF.
Please **read the documentation** (relevant part included below with emphasis on the important part) regarding this component to better understand how it functions in the edge cases.

> **Digital Documentation**
> 
> A component to store a single bit.
> Provides the functions `set` and `reset` to set or reset the stored bit.
> *If both inputs (S, R) are set at the rising edge of the clock, the final state is random.*

## Deliverables

{: .highlight-title}
> Lab Report
>
> Include the completed K-maps from above in your lab report.

Please submit the schematic `DFF.dig` with the following pinout:

| Port Direction | Port Name  | Active | Port Width (bits) |
|:--------------:|------------|--------|------------------:|
|      INPUT     | `D`        |   -    |                 1 |
|      INPUT     | `CLK`      | High   |                 1 |
|     OUTPUT     | `Q`        |   -    |                 1 |
|     OUTPUT     | `QN`       |   -    |                 1 |
