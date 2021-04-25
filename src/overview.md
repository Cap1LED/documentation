# Design Overview

## Project outline
Current solar simulators that are used in solar power research utilize xenon arc lamps. They are used due to the relatively close spectral match to daylight, their small size, and commercial availability in powers of upwards of 12kW. The main drawbacks of this technology is their rather low luminous efficacy, which means that only about 5-7% of the power drawn by the lamp is converted to usable light. This is contrasted with the efficacy of LEDs, which can convert 25-30% of power drawn into usable light. Thus the goal of this project is to have the good spectral match of xenon arc lamps while retaining the efficiency advantage of modern LEDs.
## Project objectives
* Use only off-the-shelf components
* Create a system that is modular, for expansion later
* Have a reasonably accurate spectral match
* Total radiative output of at least 200 watts
* Ability to dim
* Ability to log data
## Our Solution
The approach we took split us up into three teams that each tackled one part of the project:
* [PCB Design](./pcb/overview.md)
* [GUI Development](./gui/overview.md)
* [Microcontroller software development](./uc/overview.md)