# CMOS-Circuit-Design-Spice-Simulations-using-SKY130PDK
From transistors to simulations: learning CMOS design with Sky130 and ngspice.
This repository contains the work completed during a 10-day CMOS circuit design workshop based on the SKY130 PDK. It includes transistor-level simulations, device characterization, timing analysis, and digital design flow integration using open-source EDA tools.
## Table of Contents

### Day 1
- [Basics of NMOS Drain Current (Id) vs Drain-to-source Voltage (Vds)](#ngspicesky130---day-1---basics-of-nmos-drain-current-id-vs-drain-to-source-voltage-vds)
  - [NgspiceSky130_D1SK1 - Introduction to Circuit Design and SPICE simulations](#ngspicesky130_d1sk1---introduction-to-circuit-design-and-spice-simulations)
  - [NgspiceSky130_D1SK2 - NMOS resistive region and saturation region of operation](#ngspicesky130_d1sk2---nmos-resistive-region-and-saturation-region-of-operation)
  - [NgspiceSky130_D1SK3 - Introduction to SPICE](#ngspicesky130_d1sk3---introduction-to-spice)

### Day 2
- [Velocity saturation and basics of CMOS inverter VTC](#ngspicesky130---day-2---velocity-saturation-and-basics-of-cmos-inverter-vtc)
  - [NgspiceSky130_D2SK1 - SPICE simulation for lower nodes and velocity saturation effect](#ngspicesky130_d2sk1---spice-simulation-for-lower-nodes-and-velocity-saturation-effect)
  - [NgspiceSky130_D2SK2 - CMOS voltage transfer characteristics (VTC)](#ngspicesky130_d2sk2---cmos-voltage-transfer-characteristics-vtc)

### Day 3
- [CMOS Switching threshold and dynamic simulations](#ngspicesky130---day-3---cmos-switching-threshold-and-dynamic-simulations)
  - [NgspiceSky130_D3SK1 - Voltage transfer characteristics – SPICE simulations](#ngspicesky130_d3sk1---voltage-transfer-characteristics--spice-simulations)
  - [NgspiceSky130_D3SK2 - Static behavior evaluation – CMOS inverter robustness – Switching Threshold](#ngspicesky130_d3sk2---static-behavior-evaluation--cmos-inverter-robustness--switching-threshold)

### Day 4
- [CMOS Noise Margin robustness evaluation](#ngspicesky130---day-4---cmos-noise-margin-robustness-evaluation)
  - [NgspiceSky130_D4SK1 - Static behavior evaluation – CMOS inverter robustness – Noise margin](#ngspicesky130_d4sk1---static-behavior-evaluation--cmos-inverter-robustness--noise-margin)

### Day 5
- [CMOS power supply and device variation robustness evaluation](#ngspicesky130---day-5---cmos-power-supply-and-device-variation-robustness-evaluation)
  - [NgspiceSky130_D5SK1 - Static behavior evaluation – CMOS inverter robustness – Power supply variation](#ngspicesky130_d5sk1---static-behavior-evaluation--cmos-inverter-robustness--power-supply-variation)
  - [NgspiceSky130_D5SK2 - Static behavior evaluation – CMOS inverter robustness – Device variation](#ngspicesky130_d5sk2---static-behavior-evaluation--cmos-inverter-robustness--device-variation)
 
## Tools Used
SKY130 Open-Source PDK
ngspice (Circuit Simulation)
GitHub(Documentation)

# Day1 [Basics of NMOS Drain Current (Id) vs Drain-to-source Voltage (Vds)]
## Introduction to Circuit Design and SPICE simulations
## L1 Why do we need SPICE simulations?
SPICE (Simulation Program with Integrated Circuit Emphasis) simulations are used to analyze and verify the behavior of electronic circuits before fabrication.
#### Circuit Design
