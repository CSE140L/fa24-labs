---
title: Part 2
parent: Lab 5
layout: katex
nav_order: 3
---

# Booth's Multiplication with FSMs
{: .no_toc}

## Contents
{: .no_toc .text-delta}

1. TOC
{:toc}

---

## Introduction

Our Booth’s multiplier from Lab 2 had an obvious shortcoming.
Even though we could "skip" add operations during long strings of 1's or 0's in our multiplier, our circuit still performed the operation! (Though, the result of the operation was discarded on cycles where the add/sub wasn't needed.) 
The natural next step is to provide functionality to skip unnecessary add and subtract operations.
With your new expertise in finite state machines, it is now possible to design a new controller that can skip those operations! 

We ask that you implement the new controller twice: once as a Mealy machine and once as a Moore.

## Circuit Structure

{: .warning}
Failure to follow this structure can result in grading of the lab to be delayed or incorrect.

You will create two circuits for this part, `BoothsMultiplierMealy.dig` and `BoothsMultiplierMoore.dig` that follows the same pinout from Lab 2.

| Port Direction | Port Name       | Active | Port Width (bits) | Description                                                             |
|:--------------:|-----------------|:------:|------------------:|-------------------------------------------------------------------------|
|      INPUT     | `CLK`           | Rising |                 1 | Clock input used for controlling the multiplier                         |
|      INPUT     | `CLR`           |  High  |                 1 | Clears the multiplier to allow it for later reuse                       |
|      INPUT     | `MULTIPLIER`    |    -   |                13 | 13-bit signed decimal input as multiplier                               |
|      INPUT     | `MULTIPLICAND`  |    -   |                13 | 13-bit signal decimal input as multiplicand                             |
|     OUTPUT     | `RESULT`        |    -   |                26 | 26-bit signed decimal output as a result from your multiplication       |
|     OUTPUT     | `OP_DONE`       |    -   |                 2 | The operation you have performed (addition, subtraction, or no-op)      |
|     OUTPUT     | `DONE`          |  High  |                 1 | Set high when you have finished the multiplication                      |
