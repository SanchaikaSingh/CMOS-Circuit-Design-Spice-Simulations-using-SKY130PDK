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
A circuit design includes PMOS and NMOS tied together in such a fashion that they result into logic gates such as NAND, NOR, OR, AND etc. 
given below is an inverter circuit using NMOS and PMOS

<img width="484" height="471" alt="image" src="https://github.com/user-attachments/assets/1b59621f-19e3-425f-93c6-76714357735a" />

#### Delays
Without SPICE there won't be delays and if there are no delays physical design flow, crosstalk won't make any sense.
Now,let us consider Delay tables for both level 1 and level 2 buffers have been shown. This is calculated by circuit design and simulation

<img width="819" height="394" alt="image" src="https://github.com/user-attachments/assets/d9b57b00-b12e-4335-adab-c96b0c321681" />

## L2 Introduction to basic element in circuit design-NMOS
