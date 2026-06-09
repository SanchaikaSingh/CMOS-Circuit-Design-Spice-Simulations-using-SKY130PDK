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
- SKY130 Open-Source PDK  
- ngspice (Circuit Simulation)  
- GitHub (Documentation)

# Day 1 [Basics of NMOS Drain Current (Id) vs Drain-to-source Voltage (Vds)]
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
An NMOS transistor consist of P-type substrate, heavily doped with n+ region. There is an isolated region which isolates the transistor from other transistors. The n+regions are Source and Drain. Above it there is an oxide layer, and top of it is metal deposition which is the Gate termianal.

<img width="779" height="324" alt="image" src="https://github.com/user-attachments/assets/fb09410d-695d-4664-aebe-028dda8b205c" />

At first we will keep the Vgs=0, means source and drain terminal both are grounded.
When  Vgs exceeds the threshold voltage Vth , an n-channel forms between the source and drain.
Increasing Vgs further attracts more electrons to the channel.
This strengthens the inversion layer and reduces channel resistance.
As a result, the drain current increases and the transistor conducts more effectively.

<img width="824" height="371" alt="image" src="https://github.com/user-attachments/assets/4a64fb67-e903-47ae-a98c-56201c23043f" />

## L3 Strong inversion and threshold voltage
Due to Accumulation of negative charges, there will be formation of Depletion Region, depleting of it's majority carriers i.e positive carriers here.

<img width="809" height="362" alt="image" src="https://github.com/user-attachments/assets/20bce8a0-20dd-4e92-9328-d7019c1e244f" />

Now we will increase the Gate voltage further, we will see that the positive charge carriers will be repelled and there will be increase of Depletion Width. On further increase of Gate voltage we will reach at a point where the surface gets inverted into an n-type material, this is called "Surface Inversion" or "Stronf Inversion". The gate voltage of Vgs voltage where Strong Inversion happens is called "Threshold Voltage".
with Vds=0 , no current flows despite the channel being present, so the transistor remains in the cutoff state.

<img width="758" height="312" alt="image" src="https://github.com/user-attachments/assets/23eadc10-f210-4e0c-86ed-cf07e9885c97" />

## L4 Threshold voltage with positive substrate potential
Due to the increased depletion region, surface inversion occurs more slowly when Vsb>0.
As a result, a higher gate voltage is required to form the inversion channel.
Therefore, the threshold voltage increases with increasing source-to-body voltage.

<img width="817" height="355" alt="image" src="https://github.com/user-attachments/assets/288c0393-4232-43d6-a3af-5a70e31b6235" />

Semiconductor surface inverts to n tye at Vgs = Vto + V1
Therefore: Threshold voltage increases This phenomenon is called the Body Effect.

<img width="824" height="396" alt="image" src="https://github.com/user-attachments/assets/bd94e79f-2c81-47b3-a21d-2bc1fb8f7bb7" />

The threshold voltage is no longer constant and becomes a function of VSB. The body effect equation quantifies the increase in threshold voltage caused by the applied source-to-body bias, with parameters such as body-effect coefficient (γ) and Fermi potential (ϕf) determined by the manufacturing process.

## NMOS resistive region and saturation region of operation
## L1 Resistive region of operation with small drain-source voltage
When Vgs>Vth, a continuous inversion channel forms between the source and drain.
Applying a small Vds creates a slight voltage drop along the channel.
The channel then provides a path for electron flow from source to drain.
At the source end, the gate-to-channel voltage is approximately equal to Vgs.

<img width="796" height="489" alt="image" src="https://github.com/user-attachments/assets/986cbd8e-5238-4f40-99da-eb8e8b70b8db" />

As the channel potential increases toward the drain, the effective gate voltage decreases slightly.
Since Vds is small, the channel remains inverted along its entire length.
The channel behaves like a gate-controlled resistor, and the drain current increases nearly linearly with Vds.
Hence, this mode of operation is called the Linear (Resistive) Region.

## L2 Drift current theory
The effective channel voltage will vary w.r.t x.

for example at x=0, Vgs=1V and V(x)=0, So the Vgs-Vx=1V.

At x=Vds=0.05V, Vgs-Vx=0.95V. Now if we see the induced chagre equation, it is proportional to the effective channel voltage.

As we know there are two types of currents; Dift and Diffusion current, Here there is Drift current due to potential difference across the channel.

<img width="826" height="400" alt="image" src="https://github.com/user-attachments/assets/60a19efe-184f-4ef1-9103-85157c4e21bb" />

<img width="822" height="375" alt="image" src="https://github.com/user-attachments/assets/18f886b1-bb1e-4a1f-af7f-46b5e4cc0aa7" />

To get the drain current, the top view of transistor is required.

<img width="809" height="397" alt="image" src="https://github.com/user-attachments/assets/91372c69-7702-49cf-9765-7df0ec8ce1c4" />

## L3 Drain current model for linear region of operation
As there is change of voltage across the channel length, this will result in change of velocity which is a function of mobility and electrci field.

## L4 SPICE conclusion to resistive operation
After deriving the linear-region drain current equation, SPICE simulations are performed to validate the theoretical model. By sweeping Vds from 0 to (Vgs-Vth) for different values of (Vgs), the variation of drain current is observed while maintaining linear-region operation. The simulation verifies the drain current equation, demonstrates the effect of gate voltage on channel conductivity, and provides accurate I–V characteristics without lengthy manual calculations.

## L5 Pinch-off region condition
There is also a Region of operation when Drain-source voltage exceeds the value (Vgs-Vt), the region of operation is called "Saturation Region". We know the channel voltage is Vgs-Vds. Now, we will increase the Vds.

When Vgs-Vds is greater than Vt, there will be a conducting channel. When Vgs-Vds is equal to Vt, we will see at drain side, just Inversion has happened as it is equal to Vt, so channel will start disappearing at drain side.

<img width="816" height="364" alt="image" src="https://github.com/user-attachments/assets/f0923872-800b-4255-8605-dfe9e7d85848" />

When Vgs-Vds is equal to Vt, we will see at drain side, just Inversion has happened as it is equal to Vt, so channel will start disappearing at drain side.

Pinch off Voltage When the channel starts to disappear, is termed as "Pinch off region"

<img width="807" height="361" alt="image" src="https://github.com/user-attachments/assets/aa41ba5e-a7ca-4d06-bc28-37c24700a823" />

<img width="371" height="86" alt="image" src="https://github.com/user-attachments/assets/eb96af7c-e094-4649-8aa7-74f514012278" />

## L6 Drain current model for saturation region of operation
In saturation region, the channel voltage will remain constant as 'Vgs-Vt', and the drain current will not depend on Vds. To get drain current equation in saturation region we will replace Vds as Vgs-Vt.

<img width="413" height="325" alt="image" src="https://github.com/user-attachments/assets/42e31cf7-9535-497b-876f-a86d76e51654" />

According to the equation, the mosfet acts as perfect current source. But this is not true, when we increase Vds we will that Depletion region at drain increases and so channel length further reduces.Therefore, we see a slight dependency of Vds over Id. This is called "Channel Length Modulation".

<img width="809" height="354" alt="image" src="https://github.com/user-attachments/assets/fbf2548e-ebd9-4499-82e6-0400ca5db852" />

<img width="794" height="146" alt="image" src="https://github.com/user-attachments/assets/0d63ec9f-bd9d-4728-b9ee-84068928c037" />

## Introduction to SPICE
## L1 Basic SPICE setup
The encircled parameters arwe called spice model parameters. These may or may not be constants.
These are directly coming from the foundary, we don't need to derive them.

<img width="816" height="463" alt="image" src="https://github.com/user-attachments/assets/b99b882c-9659-43e6-b00b-124461536952" />

<img width="233" height="438" alt="image" src="https://github.com/user-attachments/assets/487c1cc0-90c3-4a23-b931-2e1513240031" />

## L2 Circuit description in SPICE syntax
To define a spice netlist :
firstly nodes are identified

<img width="554" height="357" alt="image" src="https://github.com/user-attachments/assets/4a3264ac-b191-4e89-aa9f-deb160636d35" />

Then,nodes are named and code is written.

SPICE Netlist

Then,nodes are named and code is written.

<img width="800" height="349" alt="image" src="https://github.com/user-attachments/assets/ac1713dd-a16d-49f3-9df8-87470fd186a5" />

## L3 Define technology parameters

<img width="586" height="327" alt="image" src="https://github.com/user-attachments/assets/bf4fb32b-b6b2-432a-8b54-91243691582d" />

Now we will look for model of this particular NMOS. For this we have model paramters, and it becomes easy to model from the parameters. That is where the technology file comes into picture. The models for the name NMOs will be found in file which has the attribute of the similar name.

Inside the brackets, technology paramteters will exist. Similarly for pmos also.

<img width="473" height="57" alt="image" src="https://github.com/user-attachments/assets/c254db26-d3a8-4aae-b34f-54d56f5a0f69" />

Now, we just plug in this packaged file in .mod file and call this file in top level SPICE netlist.

<img width="480" height="454" alt="image" src="https://github.com/user-attachments/assets/4ef1073e-1f6d-4fef-974a-46ead1fd832b" />

<img width="554" height="142" alt="image" src="https://github.com/user-attachments/assets/0dc577b7-5567-4db9-a9bf-648385ee76f6" />

## L4 First SPICE simulation

<img width="960" height="762" alt="Screenshot 2026-06-08 173027" src="https://github.com/user-attachments/assets/9f96a140-6628-485c-902e-31597c3c0693" />

<img width="1366" height="768" alt="Screenshot (1)" src="https://github.com/user-attachments/assets/79913813-53de-456f-ba73-c88128f1f7d6" />

To check the value of Id for corresponding Vds and Vgs, just left click and see.

<img width="263" height="26" alt="image" src="https://github.com/user-attachments/assets/3d63d8d9-cec3-4566-b6a4-d65205a6c457" />

#  Day 2 [Velocity saturation and basics of CMOS inverter VTC]
## SPICE simulation for lower nodes and velocity saturation effect
## L1 SPICE simulation for lower nodes
This curve is from previous SPICE simulation in which Id is at y-axis and Vds is at x-axis

<img width="827" height="497" alt="image" src="https://github.com/user-attachments/assets/db7bfd6f-f405-4fd3-864b-57d2bd18a091" />

the above graph the area left of curve; Vds=Vgs-Vt is Linear region as current is increasing linearly, the area right is Saturation region with slight increase in current due to velocity saturation and below is the Cut off region.Also this case is when the channel length is large.

Now we are taking different W and L, but the ration of W/L is same as previous, so the Id should not change. But this is not the case practically.

Below is the spice deck, where only the values of W and L is changed, rest everything remains same.

<img width="782" height="451" alt="image" src="https://github.com/user-attachments/assets/3b3a7a92-f09f-4837-ad30-adba16f7994f" />

## L2 Drain current vs gate voltage for long and short channel device
Now we are comparing between Long and Short channel device

Some of the observations are:

1. If we see Id values for different Vgs and for Vds=2.5V, there is a quadratic dependency of Id on Vgs. Whereas for short channel device, at Vds=2.5V, the current is increasing linearly due to velocity saturation.

<img width="833" height="448" alt="image" src="https://github.com/user-attachments/assets/e0ccbef5-e24b-4674-bc2e-26a7c3b9c804" />

Now we will plot graph of Id vs Vgs and sweeping Vds or keeping Vds constant = 2.5V.

<img width="779" height="480" alt="image" src="https://github.com/user-attachments/assets/07b56f1c-8423-4085-86a8-c2c35e19bacc" />

syntax explains that what will be there on left hand side will be sweeped at every value on right hand side. For example here for every value of Vdd, Vin will be sweeped. The plot we get is quadratic, it is only when Vds=2.5V

<img width="543" height="441" alt="image" src="https://github.com/user-attachments/assets/5e1e9b92-dcba-44d7-8e71-a9c2db228bce" />

velocity saturation: is a phenomenon that occurs in short-channel MOSFETs when the electric field in the channel becomes very high.

<img width="832" height="414" alt="image" src="https://github.com/user-attachments/assets/245b3554-1f39-42f9-ab64-1bb0ea023ac6" />

## L3 Velocity saturation at lower and higher electric fields
For short channel we will see more of a linear behaviour as the Vgs increases. This is due to velocity saturation effect.

<img width="797" height="401" alt="image" src="https://github.com/user-attachments/assets/6630130e-75e7-451b-9a63-c2212f494422" />

We know velocity and electric field are related to each other with equation v=uE, where v is velocity, E is electric field and u is mobility. Velocity increases linearly with electric field over certain electric field value after which it gets saturated. This is due to scattering at higher fields and mobility decreases.

<img width="816" height="431" alt="image" src="https://github.com/user-attachments/assets/e8c51cdf-8cc7-4fb6-892f-e97eed381f41" />

Velocity saturation happens for higher gate-source voltages.

<img width="825" height="386" alt="image" src="https://github.com/user-attachments/assets/3b858f0a-772a-45c2-be03-b68ea00c0ac3" />

<img width="818" height="341" alt="image" src="https://github.com/user-attachments/assets/753419f6-fd9d-462b-9a0a-bdae7cadc521" />

## L4 Velocity saturation drain current model
Let us take Vgs-Vt=Vgt because we will be taking Vgs as large values. Current equation we will be using as shown above, For lower values of Vds we will neglect the 'lambda' term.

There is one more technology paramter which is "Vdsat", it is the velocity of gate when the device just enters the Velocity saturation region.

<img width="788" height="187" alt="image" src="https://github.com/user-attachments/assets/6bab366f-86a5-41de-8f3d-34c8a27ac9f1" />

Saturation region:

<img width="822" height="514" alt="image" src="https://github.com/user-attachments/assets/828bba5d-6d45-4584-8c3b-0ee77a4c6ae8" />

Resistive region:

<img width="822" height="415" alt="image" src="https://github.com/user-attachments/assets/fda00468-a28d-44f0-b93d-8cd684910d5d" />

Velocity Saturation region:

<img width="814" height="400" alt="image" src="https://github.com/user-attachments/assets/957a5ae9-0424-48f0-8ef8-360df32cbadb" />

In the above equation, it seems when W is constant and L is lowered then Id should increase, But it is not so practically.

Observation 2 - The saturation current for lower nodes is low instead of being high. This is because Velocity saturation tends to saturate the device early so the peak current we see for lower nodes is much lesser than for higher nodes.

<img width="832" height="364" alt="image" src="https://github.com/user-attachments/assets/c5eca2b4-92d8-4677-ba77-a51ec3690852" />

## L5 Labs Sky130 Id-Vgs
We will now do simulation for lower nodes. Inside day2 design file.

<img width="955" height="759" alt="Screenshot 2026-06-08 173654" src="https://github.com/user-attachments/assets/ff2ce721-f50f-4851-b204-25bfc0e7a702" />

<img width="1058" height="752" alt="Screenshot 2026-06-08 174356" src="https://github.com/user-attachments/assets/cc30cd5c-4f3f-4e91-8184-abfd211774d0" />

The above plot is Id vs Vds for different values of Vgs. We can see for lower values of Vgs it is showing quadratic behaviour and for higher values of Vgs it is showing Linear behaviour. 

## L6 Labs Sky130 Vt
Now we will calculate Threshold Voltage Vt for Id vs Vgs curve.

<img width="1071" height="765" alt="Screenshot 2026-06-08 175013" src="https://github.com/user-attachments/assets/a0f1906c-4d60-4875-b95e-77b2d396c1c8" />

<img width="960" height="763" alt="Screenshot 2026-06-08 175101" src="https://github.com/user-attachments/assets/3f0abd42-66a0-44bf-845e-44b59fe2654c" />

In the curve we can see that Vt is the value when current increases drastically for small change in Vgs. To calculate we will draw tangent on the curve and see where it touches.

It comes at around 0.76V.

## CMOS voltage transfer characteristics (VTC)
## L1 MOSFET as a switch
We will now look at the device parameters from the switch point of view.

<img width="877" height="360" alt="Screenshot 2026-06-05 094159" src="https://github.com/user-attachments/assets/29bfcea8-0d15-41ea-bc35-ea7afa029b56" />

When |Vgs|<Vt, device is OFF and it acts as open switch
When |Vgs|>Vt, device is ON and it acts as closed switch

<img width="1082" height="591" alt="image" src="https://github.com/user-attachments/assets/4ab676ad-bf29-42e3-bddd-438e51d3ed40" />

## L2 Introduction to standard MOS voltage current parameters

We are trying to get the equivalent circuit of CMOS when Vin is 'high' and 'low', so that we can get the Voltage Transfer Characteristics (VTC) and therefore calculate the delay of the cell.
 
1. When we take Vin as 'high' and equal to Vdd, PMOS will be OFF and NMOS will be ON.
2. When we take Vin as 'low' or equal to '0', PMOS will be ON and NMOS will be OFF. 

<img width="1157" height="610" alt="image" src="https://github.com/user-attachments/assets/65ac88ef-2cde-4d30-9a6b-bd3bad8a93e7" />

1. when Vin=Vdd there is a direct path that exists between Vss and Vout, the capacitor CL discharges through the resistor.
2. when Vin=0 there is a direct path between Vdd and Vout, CL charges.

Let us give the naming convention of the CMOS:
<img width="477" height="591" alt="image" src="https://github.com/user-attachments/assets/ad029fdb-9ee6-4e73-871d-e271b2b72273" />

 current in both the condition is Idsn(drain to source for NMOS) and Idsp(Drain to source for PMOS) And Idsp = -Idsn, both are opposite in direction to each other.

 ## L3 PMOS/NMOS drain current vs drain voltage

 <img width="378" height="591" alt="image" src="https://github.com/user-attachments/assets/9e3e1b01-f900-4f1a-8b4e-afbf3c1ecc10" />

 The curve between Idsn Vs Vdsn and Idsp Vs Vdsp, it is as shown below.

 <img width="838" height="423" alt="image" src="https://github.com/user-attachments/assets/f4e784ed-f881-437e-92a6-9812decaabba" />

## L4 Step1- Convert PMOS gate-source-voltage to Vin

We have seen various internal voltages, but actually in terms of user's perspective we can't see the internal voltages and only see the external Vin and Vout. From these we calculate the VTC and eventually we get to know the delay.

Now we will see the steps to obtain Voltage Transfer Characteristics(VTC) for static CMOS inverter: Assumption: Let us assume that it is a long channel device with Vdd=2V

<img width="351" height="229" alt="image" src="https://github.com/user-attachments/assets/186d48ed-baf2-42f2-aa93-3095041d3490" />

We will fix the Vgs values as shown below 
We know that Vgsp= Vin-Vdd, So we get the above values.So we get Vin = Vgsp+Vdd, we are trying to convert all the voltages as function of Vin and Vout.
We will try to plot the graph of PMOS in terms of Idsn, the plot will be as shown below. We can see that the corresponding Vin value of Vgsp is being plotted as shown in the above table.

<img width="821" height="423" alt="image" src="https://github.com/user-attachments/assets/d295a218-6464-4298-aeec-e807037d1664" />

## L5 Step2 & Step3- Convert PMOS and NMOS drain-source-voltage to Vout
Now we will be converting the Vdsp and function of output voltage Vin. We know Vdsp = Vout-Vdd.
Let us convert Vdsp into Vout. So to get Vout there is a shift of Vdd towards left hand side.

<img width="1320" height="385" alt="image" src="https://github.com/user-attachments/assets/ae4dd0d4-12e9-4aa4-9d7f-92fa7e5014b4" />

We can see that whenever Vout=2V that means Vdsp=0V and Vdd=2V (given), then The current is zero and capacitor at the output is discharged. This is true only when PMOS is in combination with NMOS and forms a CMOS inverter.

Let us take another example, when Vout=0V, that means -Vdsp=2V and Vdd=2V, so at every gate voltage of Vin we will see a finite current whenever Vout=0V. As Vout=0V, the capacitor is completely discharged and we need to charge that, so that is the charging current required. 
So, here we get the load curve for PMOS

<img width="499" height="386" alt="image" src="https://github.com/user-attachments/assets/c074b5bf-1069-4c1b-a9b0-a9fa4ce9a29e" />

Now we will try to get the "load curve" for NMOS transistor from this equations.

<img width="220" height="65" alt="image" src="https://github.com/user-attachments/assets/87150da9-8436-4e7d-a012-f4cd6baf490a" />

It is actually simple as Vgsn = Vin and Vdsn = Vout, directly we can get the graphs.

<img width="401" height="283" alt="image" src="https://github.com/user-attachments/assets/920c0822-7bb1-433f-aa13-0e1eb6f7b657" />

<img width="875" height="369" alt="image" src="https://github.com/user-attachments/assets/19e4b690-dbfe-4244-b268-a03f38ccdcb5" />

## L6 Step4- Merge PMOS-NMOS load curves and plot VTC
Now,merge the above two curves and obtain the voltage transfer characteristics(VTC) for CMOS inverter.

<img width="964" height="288" alt="image" src="https://github.com/user-attachments/assets/7eabf5f5-ae93-4c64-bd35-0f8dbe32016c" />

find out the common point between Vin and Vout of both NMOS and PMOS.

<img width="425" height="272" alt="image" src="https://github.com/user-attachments/assets/1f0b96b1-df76-4fa4-b71c-3555350d4341" />

So the range of Vin and Vout is 0V-2V.

When Vin = 0V, Vout = 2V; NMOS is Cut Off and PMOS is in Linear region.
When Vin = 0.5V, 1.5V<Vout<2V; NMOS is in Saturation region and PMOS is in Linear region.
When Vin = 1V, 0.5V<Vout<1.5V; NMOS and PMOS are in Saturation region.
When Vin = 1.5V, 0<Vout<0.5V; NMOS is Linear region and PMOS is in Saturation region.
When Vin = 2V, Vout = 0V; NMOS is in linear region and PMOS is Cut Off.

<img width="1091" height="508" alt="image" src="https://github.com/user-attachments/assets/06cf38f2-b4bf-44c7-a1f8-c92c266eb17f" />

# Day 3 [CMOS Switching threshold and dynamic simulations]
## Voltage transfer characteristics-SPICE simulations
## L1 SPICE deck creation for CMOS inverter
SPICE Deck
component connectivity

component values

nodes identification

<img width="769" height="591" alt="image" src="https://github.com/user-attachments/assets/bab3f079-6bb8-46bc-9993-c7d2077e52cd" />

name nodes

<img width="554" height="543" alt="image" src="https://github.com/user-attachments/assets/56fbe28a-9d63-486c-8298-ede7c85dd043" />

Now to write SPICE deck:

<img width="1188" height="468" alt="image" src="https://github.com/user-attachments/assets/cc915119-9604-42de-b76d-c0ba8c07cbba" />

## L2 SPICE simulation for CMOS inverter

Simulation Commands

The gate input voltage sweeps from 0 to 2.5V with steps of 0.05. We need to find the VTC, for this we will be sweeping the input voltage and measuring the output voltage.
Final step is to describe the Model files, all the information about the technological parameteres is given inside the model files.

<img width="1242" height="501" alt="image" src="https://github.com/user-attachments/assets/6b345e40-b79a-4eb6-9d8e-5b55be96c9bf" />

Now, SPICE waveform : Wn=Wp=0.375u, Ln=Lp=0.25u, Wn/ln=Wp/Lp=1.5

<img width="660" height="529" alt="image" src="https://github.com/user-attachments/assets/8316d8cd-91c8-41d3-8f18-6de4f0dd1f5b" />

And, SPICE waveform :  Wn= 0.375u, Wp= 0.9375u, Ln,p=0.25u; Wn/Ln=1.5, Wp/Lp=2.5 (PMOS width is 2.5 times more than NMOS)

<img width="747" height="569" alt="image" src="https://github.com/user-attachments/assets/2d2600b3-35d6-4bcc-b0af-0f1c290cbb7d" />

Observation :  the previous graph is left shifted slightly. This happens because NMOS is more stronger than PMOS in previous graph.

## L3 Labs Sky130 SPICE simulation for CMOS
We now get the VTC characteristics are using both pfet and nfet for CMOS inverter. We can see that W/L ratio of pmos is 2.33 times greater than that of nmos. And we will be sweeping Vin from 0 to 1.8V with step isze of 0.01V and plotting the Vout.

<img width="1060" height="761" alt="Screenshot 2026-06-08 175639" src="https://github.com/user-attachments/assets/b3bd4381-07f1-49c6-9b7b-c5aad4ea291a" />

get the plot type ngspice and plot out vs in.

<img width="1070" height="763" alt="Screenshot 2026-06-08 175800" src="https://github.com/user-attachments/assets/69ecb000-d93b-409d-8c78-2bc0a583aae2" />

<img width="1070" height="761" alt="Screenshot 2026-06-08 175842" src="https://github.com/user-attachments/assets/a9962939-0b33-4c30-86f9-eca31527a219" />

So switching threshold for W/L=2.3 is around 0.876V

<img width="270" height="27" alt="image" src="https://github.com/user-attachments/assets/b4e4e864-3f98-4160-9de4-d1e2f5d39ed5" />

We will now see the transient analysis:
For that we will go inside the tansient SPICE file for day3

<img width="1043" height="767" alt="Screenshot 2026-06-08 175954" src="https://github.com/user-attachments/assets/4631f2db-3e56-4f33-8991-f7c53fc3f7b9" />

We can see that it is for typical corner as before and the W/L is also same. But now we taking transient pulse from 0v to 1V with shift of 0 with rise time and fall time being 0.1ns and 0.1ns respectively, pulse width of 2ns and total time period of 4ns. Let us run this.

<img width="1053" height="761" alt="Screenshot 2026-06-08 180058" src="https://github.com/user-attachments/assets/2559c3b8-60a7-43d5-b059-d072355f0a79" />

<img width="1061" height="767" alt="Screenshot 2026-06-08 180125" src="https://github.com/user-attachments/assets/85840c7f-8f1f-4d21-bafb-0fce54fccf91" />

So for rise delay and fall delay, we need to consider 50% of output curve i.e. at 0.9V; out-in.

<img width="290" height="65" alt="image" src="https://github.com/user-attachments/assets/946ea47d-1c1d-4509-b09d-6f203d0e56cc" />

Therefore, Rise delay = 2.482ns-2.15ns = 0.333ns
For fall delay, consider while falling.

<img width="306" height="61" alt="image" src="https://github.com/user-attachments/assets/ce30edcf-4a7f-46f6-8282-b05f336f76fa" />

Therefore, Fall Delay = 4.334ns-4.050ns = 0.285ns

## Static behavior evaluation – CMOS inverter robustness – Switching Threshold
## L1 Switching Threshold, Vm
<img width="1174" height="579" alt="image" src="https://github.com/user-attachments/assets/49611c40-1e8a-4727-9823-1e876fb0c071" />

To find out the Switching threshold, Vm in both the cases by drawing a 45 degree line.
So, in first case Vm comes out to be somewhere around 0.9V and in second case Vm=1.2V.

<img width="1146" height="434" alt="image" src="https://github.com/user-attachments/assets/291353a5-3071-49a2-82ea-d3a4a7a3c867" />

here PMOS and NMOS both are in saturation region.
Current flows from both pmos and nmos

<img width="1100" height="512" alt="image" src="https://github.com/user-attachments/assets/47082040-5cf1-4e14-8f29-c2b137ecad15" />

### L2 Analytical expression of Vm as a function of (W/L)p and (W/L)n

<img width="512" height="253" alt="image" src="https://github.com/user-attachments/assets/517e1180-bc00-4930-9695-e8f5bb7a669e" />

<img width="546" height="211" alt="image" src="https://github.com/user-attachments/assets/d28f524e-e4a5-4037-baf6-72793a5b3388" />

<img width="796" height="225" alt="image" src="https://github.com/user-attachments/assets/c4932e26-8af9-4ecc-9a1a-18b4be1d1eda" />

## L3 Analytical expression of (W/L)p and (W/L)n as a function of Vm

For calculating the value of W/L for PMOS and NMOS when Vm is given.

 letting Switching threshold is exatly half of the power supply Vdd = 2.5V, therefore required Vm = 1.25V.
<img width="900" height="131" alt="image" src="https://github.com/user-attachments/assets/5f5e0153-8ae7-4bd9-8aa3-43fb759f5eb5" />

<img width="837" height="118" alt="image" src="https://github.com/user-attachments/assets/90d8b51f-f8d4-4265-8d93-040fc84c3998" />

<img width="477" height="89" alt="image" src="https://github.com/user-attachments/assets/0123bbb6-4760-452d-87fe-3ad1777aa9ab" />

<img width="760" height="85" alt="image" src="https://github.com/user-attachments/assets/a8b6eb79-0e73-49d3-b66b-e28314cbcd31" />

<img width="503" height="117" alt="image" src="https://github.com/user-attachments/assets/adcc711c-2c5e-42f9-98fa-e9af80a932c1" />

<img width="531" height="139" alt="image" src="https://github.com/user-attachments/assets/1a667d8a-3717-423c-a456-c25c63fb0493" />

As RHS all are constants. So , If we know Vm then we can get the W/L ratios.

<img width="297" height="225" alt="image" src="https://github.com/user-attachments/assets/3509753f-4ecf-4d6b-b5e4-2ff6762125bf" />

## L4 Static and dynamic simulation of CMOS inverter

When Wn/Ln = Wp/Lp = 1.5

<img width="1115" height="554" alt="image" src="https://github.com/user-attachments/assets/e8dcb91a-9e15-426e-89ec-348c60bd9cd1" />

To find Rise time and Fall time => We do transient analysis

<img width="1283" height="482" alt="image" src="https://github.com/user-attachments/assets/5f608a46-9043-4c61-8b1a-2899ce08ab4a" />

## L5 Static and dynamic simulation of CMOS inverter with increased PMOS width

   Now when Wp/Lp = 2 Wn/Ln
   
   <img width="746" height="603" alt="image" src="https://github.com/user-attachments/assets/dc5ca89c-750d-4cf1-b742-836ddf77e867" />

   When Wp/Lp = 3 Wn/Ln
   
   <img width="694" height="494" alt="image" src="https://github.com/user-attachments/assets/fedd5773-9c80-4e35-b1e9-485275a22b80" />

   When Wp/Lp = 4 Wn/Ln
  
  <img width="686" height="494" alt="image" src="https://github.com/user-attachments/assets/14f9d4d0-266b-4307-bd62-d004d82a6ad3" />

   And when Wp/Lp = 5 Wn/Ln
  
   <img width="886" height="508" alt="image" src="https://github.com/user-attachments/assets/5b7f16df-9837-45a8-9b2e-3d48e33b2f5f" />

   Vm is increasing for the increasing value of width of PMOS transistors as the PMOS has become more stronger and it needs more current to charge the output load    capacitor.
   
<img width="678" height="227" alt="image" src="https://github.com/user-attachments/assets/ea52289b-4a74-47ce-bc10-fffee8ffb6b6" />

Rise delay decreases with increase in PMOS width, this shows the time required to charge the output capacitor decreases significantly this is because we have a bigger area.

 ## L6 Applications of CMOS inverter in clock network and STA

 <img width="1125" height="278" alt="image" src="https://github.com/user-attachments/assets/809717a9-f28a-4322-b833-ad95ba9127de" />

 Key obseravations of the L5 experiments :
 
 -During fabrication, there can be slight variation in sizes of PMOS and NMOS from the required one, but the robustness of CMOS inverter is such that, there is not much difference in the Vm with change in sizes.

-RISE-FALL delay being approximately equal for Wp/Lp = 2 Wn/Ln, shows "Symmetry" of CMOS inverter. This is a typical characteristic of Clock Inverter/buffer where we want the rise delay and fall delay to be equal.

  <img width="1257" height="680" alt="image" src="https://github.com/user-attachments/assets/47e623e1-7e40-4827-9a4e-34b718741935" />

 <img width="1059" height="287" alt="image" src="https://github.com/user-attachments/assets/8fdbd4a8-c86e-43e3-93f4-9e13b8ea35d3" />

<img width="1244" height="667" alt="image" src="https://github.com/user-attachments/assets/c0d1d632-3ac9-45bd-9d65-8f6585d44f3d" />

# Day 4 [CMOS Noise Margin robustness evaluation]
## Static behaviour evaluation-CMOS inverter robustness-Noise Margin
## L1 Introduction to Noise Margin
Now we will learn CMOS inverter's robustness towards the Noise Margin. Also we see the Noise margin evaluation for CMOS inverter. 

Noise Margin: It is a measure of how much unwanted electrical noise a logic circuit can tolerate on its input without producing an incorrect output. 
For example if we consider an ideal Inverter, for inputs 0/1 it gives output as 1/0. The slope of switch is infinite. 
But practically the slope won't be infinite, due to presence of resistances and capacitances there will be delay. Therefore we will get a finite slope 

<img width="911" height="571" alt="Screenshot 2026-06-05 115433" src="https://github.com/user-attachments/assets/463695c4-ea83-489a-8003-45a1704a281d" />

whenever the input is between 0 to VIL(input low voltage); the output will be VOH(output high). 
And whenever the input is between VIH(input high voltage) and Vdd; output will be VOL(output low voltage). 

<img width="799" height="624" alt="Screenshot 2026-06-05 115556" src="https://github.com/user-attachments/assets/3a103fc7-12e7-48f7-be79-b141cc6304b3" />

## L2 Noise Margin voltage paramters
Considering the more practical scenarios and non idealities of an inverter, the curve we get is as shown below. So here the when the 0 output is VOH output is 0VOL as VOH will be output high for the next inverter which will be connected and 0 as it will be the output low for the next inverter. 
Also, the slope is approximately -1, as for increase in input, output is reducing. 

<img width="964" height="628" alt="Screenshot 2026-06-05 120022" src="https://github.com/user-attachments/assets/6d6b3d8d-7497-4c38-b422-62eda7c04c6f" />

## L3 Noise margin equation and summary
Now we will calculate the noise margin equation, for that we will plot the voltages on the same scale.

<img width="700" height="404" alt="image" src="https://github.com/user-attachments/assets/f6e45cf0-689f-4804-9071-a90bedb4ff9c" />

Noise margin High NH - value between VIH and VOH. 
Noise Margin Low NL - value between VIL and VOL. 

Any value which lies in between noise margins is considered either 1/0 and considered to be tolerable. Apart from this region the value is "Undefined" and the logic level can swing between 'high' and 'low'.

<img width="841" height="521" alt="Screenshot 2026-06-05 120252" src="https://github.com/user-attachments/assets/04c18e50-b0c3-457e-b2c2-8e2348dd77a1" />

<img width="888" height="548" alt="Screenshot 2026-06-05 120752" src="https://github.com/user-attachments/assets/f6105724-b4d2-4528-b4dc-decc920a4065" />

## L4 Noise margin variation with respect to PMOS width
We will evaluate the noise margin depending upon the PMOS width and ultimately prove that how CMOS inverter is robust to the noise margins.
First, we will find the points where the slope = -1 and extend the lines towards x-y axis.

<img width="1307" height="712" alt="Screenshot 2026-06-05 121139" src="https://github.com/user-attachments/assets/ed1716ee-9e30-46b9-8a22-0004ff17197c" />

<img width="1326" height="587" alt="Screenshot 2026-06-05 133257" src="https://github.com/user-attachments/assets/6cb14026-fe48-4390-813d-fd181451ba9e" />

<img width="1328" height="575" alt="Screenshot 2026-06-05 133324" src="https://github.com/user-attachments/assets/352be46a-f199-4de7-9084-35d43a69471e" />

<img width="1314" height="601" alt="Screenshot 2026-06-05 133356" src="https://github.com/user-attachments/assets/a4a4e7f7-61c3-4dac-806e-7e808ae4d732" />

<img width="1307" height="587" alt="Screenshot 2026-06-05 133417" src="https://github.com/user-attachments/assets/02bf165f-6b52-43f0-85e1-6d2a01d95700" />

For (W/L)p=4(W/L)p and (W/L)p=5(W/L)p noise margins are same, so even if we increase the widths further noise margin will be static. 

<img width="761" height="289" alt="Screenshot 2026-06-05 121227" src="https://github.com/user-attachments/assets/68735092-c2a3-4ed0-bd26-bb8933d0efea" />

Here also we can verify the robustness of CMOS inverter. 
Also we come to know the ranges for "Digital design" and "Analog design" in the CMOS inverter.

<img width="1201" height="634" alt="Screenshot 2026-06-05 133755" src="https://github.com/user-attachments/assets/d255c8f6-46e7-4425-8f0e-46c6f503b5cf" />

<img width="1193" height="621" alt="image" src="https://github.com/user-attachments/assets/952e5e9a-72f2-4d2c-95d8-e0eda183a8fd" />

## L5 Sky130 Noise margin labs
We will now plot Noise margins

<img width="1061" height="765" alt="Screenshot 2026-06-08 180227" src="https://github.com/user-attachments/assets/fa497c1e-e912-46b6-b77f-dcba63f7771c" />

<img width="1068" height="763" alt="Screenshot 2026-06-08 180340" src="https://github.com/user-attachments/assets/0617ae17-e50c-4535-8205-afe1054c9e99" />

<img width="1075" height="759" alt="Screenshot 2026-06-08 180419" src="https://github.com/user-attachments/assets/22064c0e-38ed-4bed-a363-7fce437b7af9" />

<img width="270" height="49" alt="image" src="https://github.com/user-attachments/assets/57aba85c-aec9-4043-97eb-21a8bc01d47c" />

We will take the point where the slope is -1 ; x axis will give VIL and VIH, whereas y axis will give VOH and VOL. Noise margin NH = VOH - VIH = 1.70952-0.98778 = 0.72 Noise margin NL = VIL - VOL = 0.7733-0.09523 = 0.67807

# DAY 5 [CMOS power supply and device variation robustness evaluation]
## Static behavior evaluation – CMOS inverter robustness – Power supply variation
## L1 Smart SPICE simulation for power supply variations
As technology scales, the supply voltage is reduced to lower power consumption.

 To study the robustness of the CMOS inverter, the supply voltage was varied from 1.8 V to lower values while observing the Voltage Transfer Characteristics (VTC). Ideally, reducing the supply voltage should not significantly alter the inverter's switching behavior.
 
 <img width="1123" height="685" alt="image" src="https://github.com/user-attachments/assets/7e63fe80-ab67-4325-b88a-a9734fec652c" />


 <img width="808" height="449" alt="image" src="https://github.com/user-attachments/assets/4f862ac7-e3e7-4465-be17-032b5c9d0c7d" /> 
 
 Here we will do some scripting under ".control" and ".endc" . All the other commands will remain same as they were previously.

 <img width="738" height="563" alt="image" src="https://github.com/user-attachments/assets/031eafef-bc6d-4655-8195-8560f5225971" />
 
 The above plot shows the changes in CMOS curves as we chnage the supply voltages while the width of the channel is kept constant.

 ## L2 Advantages and disadvantages using low supply voltage
  <img width="876" height="543" alt="image" src="https://github.com/user-attachments/assets/0f4eab6a-1791-4b56-ab0b-18d3e522ddd8" />
  <img width="907" height="553" alt="image" src="https://github.com/user-attachments/assets/ddc4de95-459c-4ca8-964b-993b8b6d22f5" />

  <img width="623" height="183" alt="image" src="https://github.com/user-attachments/assets/48546de0-3a46-47fe-b082-4ee30d3b441f" />

  Along with the advantages of operation at 0.5v over 2.5, there are also certain disadvantages. that's why it 0.5V is not commmonly used in operating devices.

  <img width="958" height="547" alt="image" src="https://github.com/user-attachments/assets/28f44eb1-e720-4f2d-bbcc-d4b350e7110e" />

 The main disadvantage is the rise and fall delay due to which load capacitance doesn't even get enough time for charging and dischanging.
 Ths causes major performance impact.
## L3 Sky130 Supply Variation Labs
<img width="1078" height="767" alt="Screenshot 2026-06-08 180907" src="https://github.com/user-attachments/assets/13ee2643-0b2a-492c-a64b-7ab0f5ac66cd" />

The initial supply voltage is 1.8V and we are reducing it with the step of 0.2V, so there will be 6 iterations.

<img width="1066" height="761" alt="Screenshot 2026-06-08 181008" src="https://github.com/user-attachments/assets/197c1500-be8d-4bd2-9374-85326f639613" />

<img width="1065" height="763" alt="Screenshot 2026-06-08 181211" src="https://github.com/user-attachments/assets/43d5d6b7-5988-458a-9709-5814330bdf57" />

We will calculte the Gain:
Vdd=1.8V
|gain|=10.64

<img width="255" height="67" alt="image" src="https://github.com/user-attachments/assets/d8869aad-1454-4e8e-ac03-31f4da1eef01" />

## Static behavior evaluation – CMOS inverter robustness – Device variation
## L1 Sources of variation – Etching process
During fabrication, the gate dimensions may change. Etching is one of the sources of variation.

<img width="1147" height="619" alt="image" src="https://github.com/user-attachments/assets/37cb71a9-e050-495c-a263-009a93182a9c" />

For a single inverter layout, we see the length of gate, the width(common area between polysilicon and diffusion). Due to etching process there can be a variation in length and width of CMOS.

<img width="1269" height="648" alt="image" src="https://github.com/user-attachments/assets/b55b6457-d26b-4cd3-8ea7-09bc3ae0c729" />



<img width="1253" height="671" alt="image" src="https://github.com/user-attachments/assets/35733311-c5f3-47d9-9e94-a9164f27246e" />

We will get a very different kind of distorted structure at the leftmost side to the rightmost side of the chain imverters.
While the middle portion structure remains the same.

The variation in L and W can change the drain current of CMOS inverter.

<img width="912" height="604" alt="image" src="https://github.com/user-attachments/assets/551d4356-121a-4146-8944-3f020c583a30" />

## L2 Sources of variation – oxide thickness

Oxide thickness is another source of variation.
Here is the cross sectional view of the mosfet:
<img width="967" height="544" alt="image" src="https://github.com/user-attachments/assets/dd9df165-c4d9-4256-b8c1-132879d9d0c5" />

 The oxide under polysilicon gate, while fabricating the thickness can vary. There is a difference between ideal thickness and actual thickness.
Similar to the previous case, the variation in structure at the left and right most side is more. While the middle portion structure remains the same.

<img width="1293" height="625" alt="image" src="https://github.com/user-attachments/assets/65c43d3f-57cc-44f9-b6c7-e3bd0652fc33" />

<img width="766" height="106" alt="image" src="https://github.com/user-attachments/assets/028a1c7c-1bf0-49c3-83a3-2f7ef36bd845" />

## L3 Smart SPICE simulation for device variations
nNow we have to see how does the change in drain current affects the behaviour of the CMOS.
Ideally it should be least responsive towards the device variations.
We will experimentally see the dc curve variations with respect to the device variations.

<img width="1128" height="503" alt="image" src="https://github.com/user-attachments/assets/9373674b-a1ed-482d-a1da-3a193bc42226" />

Strong PMOS means it has the least resistance value 
Weak NMOS means it has the highest resistance value.
And vice versa.

<img width="521" height="453" alt="image" src="https://github.com/user-attachments/assets/203972a5-fd2f-4d47-ad4b-d83624be1c5d" />
<img width="701" height="433" alt="image" src="https://github.com/user-attachments/assets/8f439d9e-8b7a-4687-9ea0-5c56cb7268ca" />



<img width="737" height="573" alt= "image" src="https://github.com/user-attachments/assets/895b9014-d52d-4fc1-b93c-cd85e5974e8a" />

 ## L4 Conclusion
 
Here, we will be looking for two parameters to study the robustness of CMOS inverter :
-Noise margin
-Switching threshold

<img width="1088" height="537" alt="image" src="https://github.com/user-attachments/assets/3f818b33-ea80-44e8-8821-f219416d1c0a" />

The Switching threshold 'Vm' is shifted right in case of strong PMOS and shifted left in case of Strong NMOS.

<img width="950" height="532" alt="image" src="https://github.com/user-attachments/assets/15de20c8-d5a0-499d-ae17-5c23f81caf1b" />

As we see there is not much variation in Noise Margins in both the extreme cases, that means it behaves as a robust inverter in both the cases.

## L5 Sky130 Device Variation Labs
We will now do the SPICE simulations for the device variations

<img width="1072" height="757" alt="Screenshot 2026-06-08 180509" src="https://github.com/user-attachments/assets/5511b9d1-5442-4bb7-99d3-e4d8b26ad39c" />

We can see that the width of PMOS is quite large than that of NMOS. SO it is clearly strong PMOS and weak NMOS case. The Vm will be right shifted.

<img width="1086" height="767" alt="Screenshot 2026-06-08 180644" src="https://github.com/user-attachments/assets/fa1619b2-211c-44c1-82f8-005a12ba2dbb" />

<img width="1086" height="756" alt="Screenshot 2026-06-08 180815" src="https://github.com/user-attachments/assets/5a50c218-343f-4cf0-b14f-a1d695c3a906" />
