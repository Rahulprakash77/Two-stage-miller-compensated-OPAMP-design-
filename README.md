# Two-stage-miller-compensated-OPAMP-design-

## basic theory about two stage miller compensated opamp


A two-stage Miller compensated operational amplifier (op-amp) is a common architecture used in analog integrated circuits to amplify analog signals. It provides high gain, stability,
and a wide bandwidth. The Miller compensation technique is employed to enhance the stability of the op-amp, especially when dealing with capacitive loads. Here's a brief overview of the design:

**1. First Stage (Input Differential Pair):**
The first stage consists of a differential pair amplifier. This stage amplifies the input voltage difference (differential voltage) and provides a relatively high input impedance. The differential pair consists of two transistors (usually NMOS or PMOS) with their sources connected together. The drain currents of these transistors create a differential voltage at their common node.

**2. Second Stage (Gain Stage):**
The second stage amplifies the output of the first stage to provide high voltage gain. It typically consists of a common-source (for NMOS) or common-gate (for PMOS) amplifier. This stage can have additional current sources to enhance the gain and improve linearity.

**3. Miller Compensation:**
The Miller compensation technique is used to stabilize the op-amp against capacitive loads, which can otherwise lead to oscillations. Capacitive loads create a pole that can reduce the phase margin of the op-amp, making it prone to instability. The Miller compensation technique adds a capacitor between the output and the input of the first stage. This capacitor effectively reduces the gain at high frequencies, introducing a zero and improving the phase margin.

**4. Frequency Compensation:**
The choice of the compensation capacitor and other components in the circuit determines the frequency response of the op-amp. The goal is to achieve a balance between gain and bandwidth while maintaining stability. The Miller compensation capacitor, along with other external components like resistors, set the dominant pole and zero of the op-amp's transfer function.

**5. Biasing and Current Sources:**
Proper biasing of the transistors is essential for the op-amp's linear operation. A biasing network ensures that the transistors operate in their active region. Current sources are often included to provide a stable bias current for consistent operation.

**6. Output Stage:**
In some designs, an output stage is added to provide additional current drive capability. This stage can be a common-source amplifier with a current source load or other configurations based on the application requirements.

**7. Noise Considerations:**
Op-amps can be sensitive to noise, so design considerations include minimizing noise sources and optimizing the signal-to-noise ratio. This involves selecting appropriate transistor sizes, biasing currents, and using noise-reducing techniques.

**8. Simulation and Testing:**
After designing the op-amp circuit, it's crucial to simulate its behavior using tools like SPICE. Simulation helps in verifying its performance, frequency response, stability, and other characteristics. Iterative adjustments might be necessary to achieve the desired specifications.

Designing a two-stage Miller compensated op-amp involves a combination of analog circuit design principles, understanding of transistor behavior, compensation techniques, and practical considerations to ensure a stable, high-gain, and well-behaved amplifier suitable for specific applications.


The project flow goes as follows:
1. Declaring design specifications.
2. calculating the DC parameter using Dc analysis of nmos and pmos (μpCox and μnCox).
3. calculating the min and max threshold value of m1 and m3 mos
4. designing full circuit and make proper wire connection
5. check all mosfet working region through Dc analysis
6. ploting bode plot through ac analysis
7. checking all other parameter ( CMRR , slew rate , ICMR , power dissipation )


## 1. Declaring design specifications.
We are required to design an OPAMP having load capacitor CL = 10pF with the 3.3 volts power supply. I used the TSMC CMOS 0.35-μm technology for this project. An OPAMP was designed to best meet the following specificatons:
- Differential voltage gain: Avd ≥ 50dB.
- operating voltage vdd = 1.8 v
- Slew rate: SR ≥ 20 V/μS.
- Input common mode range: ICMR ≥ 1.8V.
- Unity Gain-bandwidth: GB ≥ 50MHz with a 4pF load capacitance.
- Phase Margin: f(GB) ≥ 60° with a 4pF load capacitance.
- Power dissipation: Pdiss ≤ 1mW.

- ## 2. calculating the DC parameter using Dc analysis of nmos and pmos (μpCox and μnCox)
- upcox = 295u
- uncox = 370u
- ![Virtuoso® Analog Design Environment L Editing_ RAHULP opampDC schematic@mirage 24-08-2023 14_12_36](https://github.com/Rahulprakash77/Two-stage-miller-compensated-OPAMP-design-/assets/130161648/9883e799-c44b-44f6-ab52-1aed1944b992)

## 3. calculating the min and max threshold value of m1 and m3 mos
vt3(max) = -417.717mV
vt1(min) = 512.57mV
vt3(max) = 597.31mV

![Virtuoso® Analog Design Environment L Editing_ RAHULP opampDC schematic@mirage 24-08-2023 15_07_26](https://github.com/Rahulprakash77/Two-stage-miller-compensated-OPAMP-design-/assets/130161648/5a0d3ce9-809a-4976-b80d-b86564ddff07)

## 4. designing full circuit and make proper wire connection
![Virtuoso® Analog Design Environment L Editing_ RAHULP opamp1 schematic@mirage 23-08-2023 12_14_21](https://github.com/Rahulprakash77/Two-stage-miller-compensated-OPAMP-design-/assets/130161648/74432448-5893-4169-9f71-6e4819a2cf09)

## Ac analysis ( bode plot) 
![Virtuoso (R) Visualization   Analysis XL@mirage 24-08-2023 17_07_28](https://github.com/Rahulprakash77/Two-stage-miller-compensated-OPAMP-design-/assets/130161648/922b4a52-288a-4c4a-81ac-d18e887e0699)

##  Calculation of Slew Rate.
We know that according to target specifications the slew rate should be 20V/μsec. Lets see how much we are actually getting. Below is the setup for calculation of SR. I connected inverting terminal to output in unity gain closed loop form and provided pulse input at the non-inverting terminal and observed the transient reponse.

from the wave output we get SR = 23.17 v/usec

## Calculation of Input Common Mode Range (ICMR)
To calculate the ICMR, I gave a random AC signal and I varied the Input common mode signal from 0 voltss to 3.3 volts. I observed the point with highest gain and 3db below point of it and noted the corresponding X co-ordinate values. 
calculated value from plot is 0.95v < ICMR <1.8v
## . Calculation of power dissipation
calculated value from analysis of power dissipation is 1.023mW



