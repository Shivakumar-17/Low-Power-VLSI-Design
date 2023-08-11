
# Design & Implementation of Low Power VLSI Circuits

This includes what is Low Power VLSI Design is and what are the Challenges that araises while Designing and what are the Techniques and Methodologies used for Low Power VLSI Circuit Design. 

## Low Power Design


  Low power design is a collection of techniques and methodologies aimed at reducing the overall dynamic and static power consumption of an integrated circuit (IC).


# Components of Power
![image](https://github.com/Shivakumar-17/Low-Power-VLSI-Design/assets/136796176/3ba8a49e-6d3c-439e-bca0-d5de86dafaa6)


#### Activity: 
The level of activity or the number of active components in a circuit affects power 
consumption. Active components, such as logic gates or transistors, consume more power when 
they are switching or performing computations compared to when they are idle.
#### Frequency:
 The operating frequency of a circuit also impacts power consumption. Higher 
frequencies generally result in higher power consumption due to increased switching activity 
and faster transitions.
#### Transition time: 
The time it takes for a signal to transition from one logic level to another 
affects power consumption. Shorter transition times generally result in higher power 
consumption due to increased switching activity.
#### Capacitive load:
 The capacitive load of a circuit, which is the amount of charge it can store, 
affects power consumption. Charging and discharging capacitive loads require energy, so 
circuits with larger capacitive loads tend to consume more power.
#### Voltage: 
The voltage level at which a circuit operates affects power consumption. Power 
consumption is proportional to the square of the voltage, so higher voltages result in higher 
power consumption.
#### Leakage current: 
Leakage current refers to the small amount of current that flows through a 
transistor even when it is supposed to be off. Leakage current can contribute to static power 
consumption and is influenced by factors such as temperature and transistor characteristics.
#### Peak current: 
The peak current drawn by a circuit during certain operations or events can 
impact power consumption. Higher peak currents generally result in higher power 
consumption, especially if sustained for longer durations.

## Challenges


```bash
  Power Dissipation
```
```bash
  Performance Trade-offs
```
```bash
  Design Complexity
```
```bash
  Design Verification
```
```bash
  Design for Manufacturability

```
```bash
  Design Tools and Methodologies
```
```bash
  System-Level Optimization
```
```bash
  Power Delivery
```


## Low Power Design Techniques
There are many low power design techniques available, some of which are very simple to use 
while others are more involved and complex
 
#### Clock Gating
![image](https://github.com/Shivakumar-17/Low-Power-VLSI-Design/assets/136796176/3d5996b9-b114-40e5-99d2-ff6dc6dd070d)

This technique is typically performed during logic synthesis where enable flops are optimized 
into a clock gating structure, thereby saving mux area and reducing the overall switching 
activity of the clock net (refer to Figure ). With respect to the power equation, the goal is to 
reduce capacitive load (via area reduction) and activity factors which reduces the switching power component of dynamic power. This is a very simple and readily available technique to 
reduce power and area. However, it does rely on the logic synthesis tool to perform this 
optimization. Fortunately, this technique is well-known and well supported in most tools and 
flows.

#### Multi Voltage Design
![multivoltage](https://github.com/Shivakumar-17/Low-Power-VLSI-Design/assets/136796176/fbd851b5-9d24-45b0-944e-8d7f4585e6f3)

This is a technique where functions of a chip are partitioned via performance characteristics –
perhaps one block is high performance, while the rest of the chip is lower performance as 
shown in Figure . To achieve the goals for the high-performance block, a higher voltage is 
typically required; while to save power on the lower performance blocks, a lower voltage can 
be used. This is in lieu of designing the entire block at the higher voltage, which is simpler but 
more power intensive. In the power equation, voltage is reduced which decreases every static 
and dynamic power component. With multi voltage designs, there is the complication of 
designing in separate voltage islands where voltage crossings between islands may require 
“Level Shifter” (LS) cells with the need to implement and analyze the blocks at their different 
voltage characteristics.
#### Power Gating
![Power gating](https://github.com/Shivakumar-17/Low-Power-VLSI-Design/assets/136796176/93a3c6e3-95ca-4d0e-8803-2413f2a5f59d)

This is a technique where functions on an IC are also partitioned, much like multi voltage, but 
this time the power supplies for the power domains are connected to power switches as shown 
in Figure 4.4 . Power gating effectively shuts off the power completely for a block. In the power 
equation, this zeros out the voltage and shuts off power, resulting in both static and dynamic 
savings for the time that the block is turned off. Power gating typically offers the most 
aggressive power savings, and thus it’s an ideal goal to shut off as many domains as possible, 
as often as possible, while maintaining functionality. In order to achieve this power savings 
with power gating, power switches must be implemented in the design, which requires Isolation 
gates that clamp the boundaries of the power domain to known values when off. The power 
states of the design and what combination of ON/OFF states for given voltages must be 
considered. Lastly, a power management unit (PMU) that controls the power switch and 
isolation enable signals must be implemented. It is essential that the order of these signals are 
correct during power down and power up, such that the values during shutdown are clamped 
to the right values at the right time.
#### Retention with Power Gating
![Retention with power gating](https://github.com/Shivakumar-17/Low-Power-VLSI-Design/assets/136796176/47661146-80fc-477f-ae67-d0b0ca26ba36)

Retention (or register retention) is a technique used along with power gating. Here in each 
shutdown block, when the block is OFF, either a subset of the flops or all the flops in the block 
have their previous values saved. When the block powers on, then the previously saved values 
will be restored. It is important to save the state of the block at the time it is powered off so 
that the block can quickly restore its previous state instead having to cycle through from an 
INIT state to the current state. This saves power by reducing the time and steps necessary to 
get the saved state, as well as improves the overall ramp up time to restore the previous 
functionality of the block. In addition to everything needed for power gating, retention flops 
must exist in the library that can map to the desired registers in the RTL. SAVE/RESTORE 
signals will need to be added to the PMU along with the control the sequence of these signals 
in addition to those done for power gating (refer to Figure ).
#### Advanced Techniques
There are many more advanced techniques for low power design, including the combination of 
the techniques previously mentioned. Blocks that use a lower voltage with power gating and
have isolation, retention, and level shifters are commonly seen in many modern-day chips. Well 
biasing, zero-pin retention flops, specialized low power library cells, dynamic voltage and 
frequency scaling (DVFS), adaptive voltage and frequency scaling (AVFS), and custom design 
are just some of the other advanced low power techniques also used in the industry. 
Dynamic Voltage and Frequency Scaling (DVFS): DVFS adjusts the operating voltage and 
frequency of a circuit dynamically based on workload, optimizing power consumption while 
meeting performance requirements.
 
##  Low Power Design Methodology
Assuming an example where the system has been specified, system simulations have been 
performed, microarchitecture is completed, low power choices for technology node, IP, etc., have been made, and coding of RTL and UPF are done. Given this, there are five main phases 
for low power design and verification methodology to be used to design the IC.

#### Static Power Verification and Exploration
In static verification, the first step is to ensure the inputs to the design flow (RTL, UPF, and 
SDC) are structurally and syntactically correct. By definition, static verification doesn’t use 
test vectors, so this is a very efficient way to review inputs before going into simulation or 
implementation flows. Lint and CDC checks are important in general to ensure your RTL is 
clean. UPF checks can be done either independently or with the corresponding RTL to ensure 
they are clean and SDC can also be statically checked along with RTL as well. In power 
exploration, early estimates for power for the RTL can be driven, either with estimated 
switching or actual waveforms from simulation. Choices can be made early on to improve the 
overall architecture of the design by performing early RTL power analysis.
#### Dynamic Power Verification and Analysis
In dynamic power verification, there are several important aspects to check. First off, does the 
sequence for the PMU control signals work correctly to shut down, clamp for isolation, save, 
restore, remove isolation clamp, and power up. This is an extremely important check with the 
design RTL and UPF together to make sure the design is functioning properly. Next, what type 
of waveforms and toggle activity are seen in the design? This will determine the dynamic power 
used since it depends on activity factor. The higher the activity factor, the more power is being 
used. Hence, the waveforms produced are very important to accurately estimate power both 
early and late in the process.
#### Software Driven Power Analysis
For emulation-based low power flows, it’s important to be able to capture the right peak 
windows for the design’s power profile. Emulation allows review of a much wider set of 
data, enabling one to choose
the windows that would be most valuable to generate waveforms to estimate power.
#### Power Implementation
RTL-based predictive power estimation, logical synthesis, DFT insertion and physical 
implementation all have important low power specific roles to play. RTL-based predictive 
power estimation allows, very early on, to make RTL modifications with early power estimates. 
In logic synthesis, the RTL, SDC, and UPF, now fully verified both statically and dynamically, are mapped to technology gates. Power-specific isolation, level shifter, and retention cells are 
mapped to gates as well, where timing, area and power are all part of the cost function for 
generating a Netlist and associated UPF’. DFT insertion occurs as well, often simultaneously 
during this time. Once the Netlist and UPF’ are complete, another round of checks is done 
statically and dynamically at this level – once clean, the results are input to physical 
Implementation. In physical implementation, floorplanning is done with macro placement and 
power routing in mind. Then placement is performed where power switches are physically 
inserted and placed; and iterations of placement, routing estimation, logical optimizations, and 
clock tree synthesis are performed to once again trade off for timing, area, and power. Finally, 
the routing step occurs, where pre-route of the priority signals (clock, power enables, switch 
connections) is done followed by detailed routing of the rest of the design – all with emphasis 
on reducing power more granularly, while still trying to meet the timing and area targets.
#### Signoff
UPF consistency should once again be checked during signoff. However, this time with the 
Netlist and UPF’ from logic synthesis and PGNetlist and UPF” from physical implementation. 
This will ensure that the connections and changes made to the netlist and UPF are consistent 
and clean, and the power intent is preserved. Logical equivalence checks comparing RTL and 
UPF vs. Gates and UPF’ vs. PGNetlist and UPF” ensures the logical functionality is preserved. 
Finally, static timing analysis should be performed with UPF to ensure the design meets timing; 
and power analysis with detailed waveform behaviors to give accurate power estimation 
results.
## RESULTS AND DISCUSSION
After performing simulation on various cmos logic circuits inverter, NAND, NOR, XOR and 
XNOR on 130nm Technologies in Mentor Graphics Tool and gets the following results. We 
take pulse for input and the input parameter for simulation in Eldo software (MENTOR 
GRAPHICS TOOL) are as follow: 
##### Input A 
Initial value (V/A):0, pulsed value (V/A):1, delay (s):1n, rise time (s):1n, fall time (s):1n, pulse 
width (s):20n, period (s): 50n 
##### Input B
Initial value (V/A):0, pulsed value (V/A):1, delay (s):1n, risetime (s):1n, fall time (s):1n, pulse 
width (s):30n, period (s):60n

![image](https://github.com/Shivakumar-17/Low-Power-VLSI-Design/assets/136796176/b7bf9c6d-3bb2-4902-9216-1b9a60095516)
#### Table 1 shows the simulated result of CMOS logic circuits on scale: 130nm.
![image](https://github.com/Shivakumar-17/Low-Power-VLSI-Design/assets/136796176/95f37ed8-bae4-4fb5-ad6c-3075ca3a6340)

####  Graph for above tabular data of Power Dissipation on scale 130nm
![image](https://github.com/Shivakumar-17/Low-Power-VLSI-Design/assets/136796176/829bebaf-2612-42c4-aa90-0f8192b28b93)
#### Graph for above tabular data of Delay on scale 130nm



## CONCLUSION AND FUTURE SCOPE
### CONCLUSION
Low power design techniques play a crucial role in reducing power consumption and 
improving the efficiency of VLSI circuits. Clock gating is a simple yet effective technique that 
optimizes enable flops, reducing switching activity and power consumption. Multi-voltage 
design partitions the chip into blocks with different performance characteristics, allowing for 
the use of higher voltage in high-performance blocks and lower voltage in low-performance 
blocks. Power gating shuts off power to specific blocks, effectively reducing power 
consumption when those blocks are not in use. Retention with power gating saves the previous 
values of flops in shutdown blocks, improving power-up time and preserving functionality. 
These techniques can be combined and further enhanced with advanced techniques such as 
well biasing, zero-pin retention flops, dynamic voltage and frequency scaling (DVFS), and 
custom design. Dynamic power verification and analysis are essential to ensure the correct 
functioning of power management unit (PMU) control signals and accurate power estimation 
results.

Overall, the use of these low power design techniques enables the development of energy efficient VLSI circuits, reducing power consumption and extending battery life in portable 
devices. These techniques are widely supported in design tools and flows, making them 
accessible for implementation in various projects. Continuous research and development in low 
power design techniques are essential to further improve power efficiency and meet the 
increasing demand for energy-efficient electronic devices.
### FUTURE SCOPE
The design and implementation of low-power VLSI circuits is an active area of research, and 
there are several future trends that are being explored to further improve the power efficiency 
of VLSI circuits. Here are some of the key trends:
#### Energy Harvesting: 
Energy harvesting techniques involve capturing and utilizing ambient 
energy sources, such as solar, thermal, or vibration energy, to power VLSI circuits. Researchers 
are exploring ways to integrate energy harvesting modules directly into VLSI circuits, enabling 
them to operate with minimal or no external power supply.
#### Approximate Computing: 
Approximate computing is a technique that allows for trading off 
accuracy for power savings. By relaxing the requirement for precise computation, approximate 
computing techniques can significantly reduce power consumption in VLSI circuits. This 
approach is particularly useful for applications where a small loss in accuracy is acceptable, 
such as image and signal processing.
#### Emerging Technologies: 
Emerging technologies, such as spintronics, memristors, and tunnel 
field-effect transistors (TFETs), are being investigated for their potential to reduce power 
consumption in VLSI circuits. These technologies offer new device structures and operating 
principles that can enable lower power operation compared to traditional CMOS technology.
#### Power Management Techniques: 
Power management techniques, such as dynamic voltage 
scaling (DVS) and adaptive power gating, are being further refined to optimize power 
consumption in VLSI circuits. These techniques involve dynamically adjusting the supply 
voltage and selectively powering down unused circuit blocks to minimize power consumption 
during different operating conditions.
#### Machine Learning and AI-based Optimization: 
Machine learning and AI techniques are being 
applied to optimize the design and implementation of low-power VLSI circuits. These 
techniques can analyze large design spaces, identify power optimization opportunities, and 
generate optimized circuit architectures and configurations.
#### System-level Power Optimization: 
Power optimization is not limited to individual circuits but 
also extends to system-level design considerations. Future trends involve exploring power aware system architectures, interconnect optimization, and workload scheduling techniques to 
minimize power consumption across the entire system.
#### Advanced Power Management Units: 
Power management units (PMUs) play a crucial role in 
controlling and optimizing power consumption in VLSI circuits. Future trends involve the 
development of advanced PMUs with enhanced power monitoring, adaptive power 
management, and intelligent power allocation capabilities.

It's important to note that these trends are based on current research and development efforts, 
and the field of low-power VLSI circuits is continuously evolving. As new technologies and 
techniques emerge, the focus on power efficiency will likely remain a key consideration in the 
design and implementation of VLSI circuits.


