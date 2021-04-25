# PCB Design Overview
The PCB Design team consisted of Eli Kopendahka and Jack Hayes.

## Design Process
We folowed a pretty simple design process
```
┌───────────────────────┐
│                       │
│    Research Problem   │
│                       │
└───────────┬───────────┘
            │
            ▼
┌───────────────────────┐
│                       │
│  Define Requirements  │
│                       │
└───────────┬───────────┘
            │
            ▼
┌───────────────────────┐
│                       │
│     Create Models     │
│                       │
└───────────┬───────────┘
            │
            ▼
┌───────────────────────┐
│                       │
│     Select a model    │
│                       │
└───────────┬───────────┘
            │
            ▼
┌───────────────────────┐
│                       │
│  Design and prototype │◄─────────────────────┐
│                       │                      │
└───────────┬───────────┘                      │
            │                         ┌────────┴─────────┐
            ▼                         │                  │
┌───────────────────────┐             │                  │
│                       │◄────────────┤                  │
│          Test         │             │   Make changes   │
│                       ├────────────►│                  │
└───────────┬───────────┘             │                  │
            │                         │                  │
            ▼                         └──────────────────┘
┌───────────────────────┐                      ▲
│                       │                      │
│    Evaluate Design    ├──────────────────────┘
│                       │
└───────────┬───────────┘
            │
            ▼
┌───────────────────────┐
│                       │
│    Design complete    │
│                       │
└───────────────────────┘

```
Tools we used in our design process:
- [KiCad](https://kicad.org/) : for schematic and PCB design
- [GNU Octave](https://www.gnu.org/software/octave/index) : for helping create the spectral model
- [Engauge Digitizer](https://markummitchell.github.io/engauge-digitizer/) : for digitizing the spectral graphs of each LED
- Microsoft Excel : for creating a pretty graph of the spectrum

### Research
The research phase of this project took the largest chunk of our time, as we initially had trouble finding suitable LEDs for our project. This, coupled with the design complexity each different kind of LED would bring, made it very hard initially to get this off the ground. We decided to take the relative spectral power graphs from each LED we were interested in and digitize the data so we could model how different combinations of each LED would change the total output spectrum. Using this we were able to get a relatively close spectral match with just 5 different types of LEDs.

| LED Manufacturer | Model                   | LED Count |
|------------------|-------------------------|-----------|
| Cree             | MHBBWT-0000-000C0BE240E | 20        |
| Cree             | MHBBWT-0000-000C0BD430E | 20        |
| Lumileds         | L1CU-CYN1000000000      | 60        |
| Lumileds         | LXM3-PD01               | 40        |
| Lumileds         | LXML-PF01               | 100       |

### Component Selection
After deciding on how many different kinds of LEDs and how many of each kind we'd need, we decided to calculate voltage and current requirements for our board. Initially, given the variety of voltages that each kind of LED operated at, we had thought it a good idea to look into designing a custom DC-DC power supply to power our project. It quickly became obvious that the best solution in our case would be to buy an off-the-shelf DC power supply and use resistors to drop any extra voltage. When it came to selecting what kind of transistor we would use, we arrived at a cheap MOSFET that fit our voltage and current requirements. Finally, for resistors, we decided to run a lot of resistors in parallel such that the equivalent resistance matched our calculations, and that each resistor only had to be able to handle 0.25-0.5W.
### Initial Schematic Creation
We consulted with a few professors to aid in the schematic part of the process, which ultimately resulted in a few different iterations of the schematic being created over the weeks that we worked on it. We decided to order small amounts of each component to verify that the function of each component on a small scale would agree with how we designed the schematic. Once we verified that each component would work as intended, we got to work on scaling up our small-scale schematic to the final number of LEDs required by our design.
### Place and Route
The software we used offered netlist export, which generated a very useful ratsnest which draws lines between pads that need to be connected together. The netlist import within the PCB creation tool also automatically places the correct number of components, given that the component has a linked footprint in the schematic and that the netlist you exported is current with the schematic. We met with the team that would be working on focusing the light that comes out of the board, and they requested that we make the board reasonably small, and that each type of LED be evenly distributed around the board. Using those two bits of information as a starting point, we decided the board would be 5"x5", and we would lay out the LEDs in a roughly circular pattern. Given those constraints, and the fact that we have a pretty high current requirement, we quickly learned that a two layer board was not an option. The manufacturer that we decided to go with, JLCPCB, offers boards with layers in multiples of two, with inside layers having half as much copper as outside layers. With this in mind, we calculated the minimum trace widths we'd need for each trace to carry the amount of current we needed, and proceeded with routing.