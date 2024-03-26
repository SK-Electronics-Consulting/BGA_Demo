# BGA Demo

This project is a sandbox-type project with the intention of finding the limitations
and edges of using cheap PCB manufucturing for BGA chips.

Cheap PCB manufacturing in this case are the vendors who provide very inexpensive
PCB fabrication and assembly services, such as JLCPCB and PCBWay.  

The specific goals of this project are:

1. Determine what manufacturing capability is needed for each example BGA. This includes
trace width and spacing, using blind/buried vias, and so on.  
1. Document the costs and turn around times. This may or may not include using
alternates or already in-stock parts (JLC, I'm looking at you!).

## Assumptions

1. Through hole components will be not populated.
1. Only top layer will be populated. Placing components on both sides increases cost. The types of projects that would require BGAs and double sided placement, would also really require a deeper CM relationship than what JLC/PCBWay provide.

## Scope

Items that are out of scope for this project:

1. Unrelated costs and delays, such as delays due to Lunar New Year or parts that are exceptionally difficult to source.

## Versions

### [STM32L431CCY](https://www.st.com/resource/en/datasheet/stm32l431cc.pdf)

This is a WLCSP49 package, 3.1x3.1mm, 0.4mm pitch chip.

#### March 2024 order

* 4-layer board, non-HDI.
* Trace/Space: 0.076mm (0.003")
* Vias 0.25mm w/ 0.15mm hole
* Via in pad was needed
* Smallest Passive is 0402.
* Ordered from JLCPCB on 2024/03/19, delivered on 2024/03/28
* Cost: $255.01
* Mostly just a demo board for the chip. Included a CAN PHY as that's been needed for some projects recently.
* Omitted all through hole components.
* TODO: Actually make the board based on ST's recommendation.  (I rushed ordering it, so I might have missed something crucial and this board be a dud.)
* TODO: Add a Tag-Connect to avoid the 10-pin connector.
* TODO: (Not related to this experiment) Add a 24V to 3.3V SMPS.
* TODO: Try making this with 0.0035" traces, as that seems to be a cost-adder-threshold for JLC.
* Not all balls were able to be exposed in the fanout.  In this design 8 of 49 were left unconnected. A couple of those 8 could easily be brought out, but definitely not all 49 in this fab. See (#learnings) #1.

## Learnings

1. To get a 7x7 grid out completely, you would need blind vias at a minimum, if not a 2+N(+2) stackup. This is because if you look at the 4th (middle) row, you'd fan out this way: `[Top, Blind to In1, Through to In2 or Bottom, (TBD??), Through to In2 or Bottom, Blind to In1, Top]`
