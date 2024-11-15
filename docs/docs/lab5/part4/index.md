---
title: Part 4
parent: Lab 5
layout: katex
nav_order: 5
---

# Sequence Detectors Galore
{: .no_toc}

## Contents
{: .no_toc .text-delta}

1. TOC
{:toc}

---

## Introduction

The first time you saw your new boss, you knew your stars were not aligned.
Yet confident of your long seniority in what used to be the shining start-up of Wall Street a decade ago, you knew that your job was secure.
Shielded off from the real world, apparently your naiveté had no bounds.
Soon you realize that your boss, who for some inexplicable reason has an axe to grind, is set on giving you impossible assignments, trying to generate a paper trail against you in preparation for firing you.

Your first assignment consists of giving you a 5 state Finite State Machine (FSM) with two outputs $Z_1$ and $Z_2$.
Each of these outputs generates 1 upon seeing a 3-bit input.
Immediately, you realize your boss's devious strategy upon being told that you will not be given the 3-bit sequences activating $Z_1$ and $Z_2$.
No worries, you say, since you are a budding expert in setting up recognizer FSMs.
Not only do you know how to set them up, but you can also by now decode them and figure out the detected sequences. 

The magnitude of your task becomes clearer when you are told that the input sequences that activate the transitions will not be given to you either.
Only the output behavior and the FSM!
In desperation you steal a furtive glance at the notes of your new boss' right-hand man, who seems to have the complete information, and manage to see a single input condition on one of the transitions ($S_1 \rightarrow S_1$) on this Mealy machine, which you annotate onto the specification given by your boss in [Figure 4.1](#figure-4.1).
Your spirits are a bit lifted when you notice that thankfully there is only a single input variable. 

### Figure 4.1

{: .text-delta}
Original Mealy State Machine to detect $Z_1$ and $Z_2$

{: .note}
**State Transition Format**: Input / $Z_1$,$Z_2$

![](https://lucid.app/publicSegments/view/f07ecdd3-ad51-467e-bb0c-7ffb2d5a4e4a/image.png)

{: .warning}
Update this!

While you are *busy* contemplating your fate, trying to figure out how to implement this FSM with unknown inputs on transitions, trying to act like a team player while ruing the fact that you should have invested more time reading murder mysteries, you’re awakened out of your deep reverie by hearing that your task has increased in complexity.
The FSM you designed (that recognizes $Z_1$ and $Z_2$) should be modified so as to transition to an FSM that only recognizes $Z_2$ once a $Z_2$ has been recognized in the original FSM.
Thereupon, a single recognition of $Z_2$ will revert the machine back to recognizing both $Z_1$ and $Z_2$.
The behavioral description of the FSM is given in [Figure 4.2](#figure-4.2). 

### Figure 4.2

{: .text-delta}
Behavioral description of the FSM

![](https://lucid.app/publicSegments/view/57136f40-6e69-4f2f-970c-a2aeae8696f9/image.png)

In an emotional state laden with anger, denial, and grief mixed in with technical arrogance (and once you are past the stage of reading murder mysteries) you decide to invest in a rereading of your lecture notes.
You soon realize that the analogous example in your notes is a classic example of **FSM composition** that your professor outlined, wherein once $Z_2$ has been detected in the full FSM (that recognizes $Z_1$ and $Z_2$), the reduced FSM will be transitioned into.
You do have the FSM that recognizes $Z_1$ and $Z_2$, but you are at your wits' end as to how to construct the reduced FSM (the one that recognizes $Z_2$ only).

Being the top student that you were in your long-gone days of youth when you were taking CSE 140L at your alma mater and remembering your prowess at coming up with creative solutions to challenging logic design problems, you set yourself down to study your technical predicament.
A bit of reflection informs you that the second reduced FSM can be simply obtained by using the first FSM and setting the $Z_2$ output to 0 in the cases when it was 1 in the original FSM.
So, duplicating the FSM with a small change in the $Z_2$ output has resulted in the desired FSM.
The connecting transition between the two FSMs is effected by having the $Z_1$ or $Z_2$ recognizing transitions in the original FSM go to their counterpart states in the reduced FSM.
The transition from the $Z_1$ only recognizing FSM back to the original FSM can be similarly constructed.

Your pride at your technical prowess is unbounded and hope glimmers that you will be able, perhaps, to not only fulfill the task but one-up your boss as well.
Yet your dreams take a break when you realize the next task that needs to be accomplished.
How do you minimize the states in this composite FSM whose transition inputs are unknown!? You are staring at a ten-state machine and you know that unless you reduce the number of states to eight or below, your efforts will not make the cut.

You quickly realize that to implement the FSM, you need to crack the puzzle of what the input transitions are.
For this, you go back to the well-worn pages of your lecture notes and realize that pattern recognizer FSM structures may provide insights into the transition inputs.
You manage to fully uncover all the transition inputs on your composite FSM.
With all the transitions visible, you are able to induce the equivalence of two states in the initial FSM (that detects only $Z_1$), thus saving you one.
After the first minimization, you notice that there is another pair of equivalent states that can be merged, reducing your states from the original ten down to eight and effectively saving you a flip-flop (and even more importantly reducing the size of your K-maps)! 

{: .warning}
Need to update these gate counts!

Once you have evened the playing field, you set on making your boss come up short by shaking up her throne and getting her fired while getting your long-deserved promotion in the process.
You remember overhearing her saying that the next state logic is composed of **about 18 two-input gates** when using the **Sum-of-Products form** in a **`RS flip-flop, clocked` implementation**, and **about 16 two-input gates** when using the **Sum-of-Products form** in a **`JK flip-flop` implementation**.
You decide to two-up her and use your great skills at prioritized adjacency coding you learned in 140L.
Seeing that you seem to have done the impossible, your long-time colleagues that had hurried over to your boss’s side, sensing that you are history, are now slowly coming back to your side.
Buoyed by your technical prowess, sensing the battlefield shifting in your direction, you set out to find a leaner next state logic that beats that of your boss.

{: .highlight-title}
> Lab Report
>
> In your lab report, please outline:
1. The original Mealy state machine [Figure 4.1](#figure-4.1) with transition inputs deciphered.
2. The composite FSM with 10 states. 
3. The composite, state-minimized FSM of 8 states; show your state minimization approach. 
4. The priority 1 and priority 2 groups for your prioritized adjacency technique.
5. Describe the approach you took for resolving these groups and how you arrived at a solution that satisfies primarily priority 1 groups and secondarily priority 2 groups.
6. Provide a table of your symbolic states and corresponding encodings.
7. Show your next-state and output K-maps for the FSM implemented with SR flip-flops. Show your logic in SOP form. Tell us the total number of 2-input AND/OR gates your design represents. 
8. Show your next-state and output K-maps for the FSM implemented with JK flip-flops. Show your logic in SOP form. Tell us the total number of 2-input AND/OR gates your design represents. 
9. Please explain how the constructed Karnaugh maps and logic expressions for two implemented FSMs with the SR and JK flip-flops differ.

{: .warning}
Need to check out what the circuit would look like, and do the K-maps

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
