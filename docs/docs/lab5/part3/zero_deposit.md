---
title: Zero Deposit
grand_parent: Lab 5
parent: Part 3
layout: default
nav_order: 3
---

# Zero Deposit
{: .no_toc}

## Contents
{: .no_toc .text-delta}

1. TOC
{:toc}

---

## Description of Changes to `VendingMachine`

Seeing that getting some venture capital in this recession-driven economy is difficult, you decide not to load the machine with any bills when you refill it with chocolates.
However, you soon realize that this frugal approach imposes some additional constraints on your vending machine.
For example, if a customer inserts a 5 B$ bill, the machine should dispense a bar of chocolate and a refund of 1 B$.
Yet if there are no 1 B$ bills in the till, the machine would not be able to process this refund request leaving the customer shortchanged.
Obviously we want to  preclude any sequences of events that may lead to unhappy customers not getting their change.
Perhaps you may find the preceding brief case study involving the absence of a 1 B$ motivational of the need for your vending machine to now do some checking and bookkeeping at the start of an exchange with a customer.
As we dig in further, you will see that more than just checking at the very beginning is necessary if our vending machine is successfully able to thwart the possibility of finding itself unable to make change.


As you dig in a bit deeper, you realize that there are two fundamental questions to address.
One is the question of shutting some of the bill intakes as in the case of the lock on the 5 B$ bill intake.
You soon realize that while the case discussed can be implemented at initialization time for each customer exchange, there might be a need to shut other bill intakes during the exchange after the customer has deposited some amount of money.
The second question concerns whether the locks, once asserted, should be effective throughout or whether they can be released during a customer exchange depending on the intervening deposits.
You realize that while the lock for the 5 B$ bill cannot be lifted if the customer inserts  a single 1 B$ bill (or even two 1 B$ bills), the lock can be lifted once the deposited amount has reached 3 B$s as a 5 B$ bill insertion at that point will result in two chocolates being dispensed with no need for returning any change.
But nothing is that simple in the world of the vending machines you soon observe; can you still release the lock on the 5 B$ bill intake if you are down to your last chocolate in the vending machine?
**You decide to persevere and identify all the relevant cases so that a correctly working lock system is in effect to ensure no customers are being shortchanged while not depriving you of the opportunity to make a possible sale.**


You decide to handle these kinds of situations by installing locks on the input bill slots (to preclude the deposit of this kind of bill in case it will result in a situation where correct change cannot be given) with the help of two new outputs, as shown in the figure below:

![](https://lucid.app/publicSegments/view/0745f3c9-4368-4686-a9a2-7d77abddd018/image.png)

The two new additional outputs are `lock_3` and `lock_5`, which, when 1, indicate that the machine cannot accept at this moment a 3 B$ bill and 5 B$ bill, respectively.
As we already discussed, no bills of 5 B$ should be possible to deposit if there are no 1 B$ bills present in the till to start with.
This `lock_5` can be turned on,  if applicable, right at the onset of the VendingMachine4 before an individual transaction is started (together with possibly cleaning any other locks at that point).
You soon realize that in this world of no 1 B$ bills, the `lock_3` may need to be additionally raised based on a particular current balance and state of bills in the till.
Additionally, another denomination of the current balance (and number of chocolates) may conversely result in making it possible to accept 5 B$ bills, resulting in the release of the `lock_5`.

With all these cases identified, you quickly realize that you have to take the current bill counters into account when designing logic to lock the bills.
Dreading how this will completely blow up your K-maps, you try to find a better solution.
Luckily, you quickly realize that there are at most 4 major compound actions that you have to carry out and decide to have your states output an encoding for each of these actions based on the inputs it is already using, leaving the actual job of the turning on and off the locks indicated by the encoding to the datapath.
One of these actions as we have seen before is the case where we set `lock_5` when we have 1 B$ already deposited and don’t have an extra 1 B$ to return to the user.
However, you realize that due to the initial absence of a 1 B$ , `lock_5` will have already been set, and when you reach this state, you don’t have to do anything more.
Thus, one of the first actions seems to be "Do Nothing" (always a welcome action 🙂).
You quickly scribble down the rest of the major compound actions in an encoding table.
When your FSM generates one of these encoded values, it passes this out to the top level circuit, where you then use combinational logic (possibly together with count indicators for some bills) to implement the (un)locking of  the corresponding bill intake slot.

| Enoding    | Compound Action     |
|--------------- | --------------- |
| 00   | Do Nothing    |
| 01   | Release `lock_5`   |
| 10   |    |
| 11   |    |


{: .highlight-title}
> Lab Report
>
> What are all of the cases where you might have to lock or unlock a bill slot? 
> Please describe them in the report and make the appropriate changes to your FSM logic to generate a `VendingMachine` that locks bill entry only when absolutely necessary.
> Additionally, please include a filled in encoding table in your lab report.

*Hint*: You may need to use additional flip flops for implementing these locks.
