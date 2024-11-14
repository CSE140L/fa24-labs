---
title: Part 3
parent: Lab 5
layout: katex
nav_order: 4
---

# Vending Machine FSM Design
{: .no_toc}

## Contents
{: .no_toc .text-delta}

1. TOC
{:toc}

---
## Introduction

The quarter is finally over.
You are basking in the glory of having received a well-deserved A in this course, but most importantly, in the tremendous amount of knowledge and insights you have built in hardware design throughout the quarter.
With the software job market tanking, you realize you are on the way to being one of the very few UCSD CSE graduates who has a chance at the job market.
Your parents are utterly pleased with this turn of events, and you manage to convince them to bankroll your summer adventure exploring the Caribbean right after your exams.

The allure of the Bahamas is irresistible—pristine beaches, turquoise waters, and a vibrant culture await you.
After a short flight to Nassau, you find yourself wandering through bustling straw markets, soaking in the lively rhythms of [Junkanoo music](https://youtu.be/2iry2vI0-To?si=bEG-TfmB6SWEXcvh).
The warmth of the locals, combined with the aroma of Bahamian cuisine, makes you feel like you've stepped into paradise.

One evening, a quaint little shop catches your eye.
Its highlight? 
A vending machine stocked with tropical fruit-flavored chocolate bars.
Intrigued, you try one, and it’s a revelation—the rich, creamy texture with a hint of passionfruit is unlike anything you've ever tasted.
A few days later, on a ferry to the Exumas, another vending machine beckons, this time with Bahamian guava-flavored chocolates.
You’re sold.

These chocolates are incredible, and an idea starts to take shape.
You realize this is a great entrepreneurial opportunity: designing a vending machine specifically for distributing Caribbean-inspired chocolates in tourist hotspots.
With your hardware design expertise, entrepreneurial spirit, and global perspective, you recognize the potential for success.
The booming tourism industry in the Bahamas ensures a steady stream of customers, especially during the peak travel season.

As you sit on the deck of the ferry, with the sun setting over the sparkling ocean, you begin sketching out your ideas for a state machine to control the vending mechanism.
This trip may have started as a break from your studies, but it’s quickly becoming the launchpad for your next big adventure.

## Implementation Details

You will implement four different versions of the `VendingMachine` part in this section.
You will notice that some inputs and states are unused in the FSMs.
These unused input/state combinations are represented as don't cares in the Karnaugh maps and can be used to simplify the next state and output logic.
You will notice that the Mealy-based `VendingMachine` FSM can be constructed with 3 states.
The `VendingMachine` FSMs in this section should be implemented with the state encoding following the input bill encoding using DFFs.
Similarly, the `RefundSerializer` should use for its state encoding the refund encoding and it should also be implemented with DFFs.
Please use a 4-bit counter to keep track of the number of chocolates in subparts 2 to 4 and 8-bit counters for bill counters in parts 3 to 4, except for the bonus part where you can set these parameters as you deem appropriate.
You need to set the chocolate counter and all the bill counters to 15 for subparts 2 to 4 during the reset process.
Initialise the bill counters to 31 for subpart 3 and to zero in subpart 4 during the same reset process.
The chocolate counter is initialized throughout to 15.
The `empty` signal should be asserted as 1 if the chocolate counter reaches the value 0.

{: .highlight-title}
> Lab Report
>
> In your report, please explain how you have designed the next state and output logic in the constructed FSMs by including **ALL** of the Karnaugh maps.
> In addition, please explain how you tested the `VendingMachine` in all different scenarios.
> Please describe how you implemented the logic for the locks and which cases they correspond to.
> Please also describe for the bonus part, in case you undertake it, what the minimal initial deposits and the sizes of the counters should be (and turn in the appropriate `VendingMachine` design).

## Deliverables

Please submit the following files to Gradescope **individually** (i.e. not in a folder):

- All `.dig` files you have created 
- PDF of your [lab report](#lab-report)

## Circuit Structure

For each subpart in this part, you will create a new `VendingMachineTop#.dig` file **where # is the subpart number**.

{: .note}
Your `VendingMachineTop#.dig` is not the same as `VendingMachine#.dig` for all parts, as there is some external glue logic required for the `VendingMachine` interacting with the `RefundSerializer`.
If you don't need some outputs for a given part, tie them to 0 (we will not be testing them, but we need to ensure that they exist).

| Port Direction | Port Name       | Active | Port Width (bits) | Description                                                             |
|:--------------:|-----------------|:------:|------------------:|-------------------------------------------------------------------------|
|      INPUT     | `CLK`           | Rising |                 1 | Clock input used for controlling the vending machine                    |
|      INPUT     | `RST`           |  High  |                 1 | Resets the vending machine                                              |
|      INPUT     | `BILL`          |    -   |                 2 | 2-bit encoding detailed in [Table C1](https://cse140l.github.io/fa24-labs/docs/lab5/part3/basic_design#table-1) |
|     OUTPUT     | `CHOCOLATE`     |    -   |                 2 | 2-bit encoding detailed in [Table C2](https://cse140l.github.io/fa24-labs/docs/lab5/part3/basic_design#table-1)                                    |
|     OUTPUT     | `BILL_OUT`      |    -   |                 2 | 2-bit encoding detailed in [Table C3](https://cse140l.github.io/fa24-labs/docs/lab5/part3/basic_design#table-2) for subparts 1 and 2, else it is connected to the output of the `RefundSerializer` |
|     OUTPUT     | `EMPTY`         |  High  |                 1 | Set high when the vending machine is out of chocolates                  |
|     OUTPUT     | `BUSY`          |  High  |                 1 | Set high when the vending machine is busy                               |
|     OUTPUT     | `LOCK_3`        |  High  |                 1 | Set high when the vending machine should not accept 3 B$ bills          |
|     OUTPUT     | `LOCK_5`        |  High  |                 1 | Set high when the vending machine should not accept 5 B$ bills          |
