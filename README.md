# Two-stage-miller-compensated-OPAMP-design

## Basic theory about two stage miller compensated opamp


A two-stage Miller compensated operational amplifier (op-amp) is a common architecture used in analog integrated circuits to amplify analog signals. It provides high gain, stability,
and a wide bandwidth. The Miller compensation technique is employed to enhance the stability of the op-amp, especially when dealing with capacitive loads. Here's a brief overview of the design:

![image](https://github.com/user-attachments/assets/95553e43-708d-4e16-abb0-261348774c19)

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
2. calculating the DC parameter using DC analysis of nmos and pmos (μpCox and μnCox).
3. calculating the min and max threshold value of m1 and m3 mos
4. designing full circuit and make proper wire connection
5. check all mosfet working region through DC analysis
6. ploting bode plot through ac analysis
7. checking all other parameter ( CMRR , slew rate , Noise , PSRR , Power dissipation )

# (A) NMOS Differential Input Two-Stage OPAMP
## 1. Declaring design specifications.
We are required to design an OPAMP having load capacitor CL = 4pF with the 1.1 volts power supply. I used the TSMC 40nm node technology for this project. An OPAMP was designed to best meet the following specificatons:

- 𝗗𝗶𝗳𝗳𝗲𝗿𝗲𝗻𝘁𝗶𝗮𝗹 𝘃𝗼𝗹𝘁𝗮𝗴𝗲 𝗴𝗮𝗶𝗻: 𝗔𝘃𝗱 ≥ 𝟱𝟬𝗱𝗕.
- 𝗼𝗽𝗲𝗿𝗮𝘁𝗶𝗻𝗴 𝘃𝗼𝗹𝘁𝗮𝗴𝗲 𝘃𝗱𝗱 = 𝟭.𝟭 𝘃
- 𝗦𝗹𝗲𝘄 𝗿𝗮𝘁𝗲: 𝗦𝗥 ≥ 𝟮𝟬 𝗩/μ𝗦.
- 𝗜𝗻𝗽𝘂𝘁 𝗰𝗼𝗺𝗺𝗼𝗻 𝗺𝗼𝗱𝗲 𝗿𝗮𝗻𝗴𝗲: 𝗜𝗖𝗠𝗥 (𝟲𝟱𝟬𝗺 𝟵𝟬𝟬𝗺)
- 𝗨𝗻𝗶𝘁𝘆 𝗚𝗮𝗶𝗻-𝗯𝗮𝗻𝗱𝘄𝗶𝗱𝘁𝗵: 𝗚𝗕 ≥ 𝟯𝟬𝗠𝗛𝘇 𝘄𝗶𝘁𝗵 𝗮 𝟰𝗽𝗙 𝗹𝗼𝗮𝗱 𝗰𝗮𝗽𝗮𝗰𝗶𝘁𝗮𝗻𝗰𝗲.
- 𝗣𝗵𝗮𝘀𝗲 𝗠𝗮𝗿𝗴𝗶𝗻: 𝗳(𝗚𝗕) ≥ 𝟲𝟬° 𝘄𝗶𝘁𝗵 𝗮 𝟰𝗽𝗙 𝗹𝗼𝗮𝗱 𝗰𝗮𝗽𝗮𝗰𝗶𝘁𝗮𝗻𝗰𝗲.
- 𝗣𝗼𝘄𝗲𝗿 𝗱𝗶𝘀𝘀𝗶𝗽𝗮𝘁𝗶𝗼𝗻: 𝗣𝗱𝗶𝘀𝘀 ≤ 𝟭𝗺𝗪.

## 2. calculating the DC parameter using Dc analysis of nmos and pmos (μpCox and μnCox)
upcox = 115u
uncox = 285u
 ![Virtuoso® Analog Design Environment L Editing_ RAHULP opampDC schematic@mirage 24-08-2023 14_12_36](https://github.com/Rahulprakash77/Two-stage-miller-compensated-OPAMP-design-/assets/130161648/9883e799-c44b-44f6-ab52-1aed1944b992)

## 3. calculating the min and max threshold value of m1 and m3 mos
Vtp = 485mV
Vtn = 460mV

![Virtuoso® Analog Design Environment L Editing_ RAHULP opampDC schematic@mirage 24-08-2023 15_07_26](https://github.com/Rahulprakash77/Two-stage-miller-compensated-OPAMP-design-/assets/130161648/5a0d3ce9-809a-4976-b80d-b86564ddff07)

## 4. Designing full circuit and make proper wire connection
![twoStage_nmos2](https://github.com/user-attachments/assets/e499fde2-d6f2-47b9-ae0f-744d8ab46b1f)

## 5. Ac analysis ( Bode plot) 
**DCGain=52dB , GBW = 28.24MHz and Phase Margin = 63.52 , Bandwidth=119kHz**
![Virtuoso (R) Visualization   Analysis XL@mirage 24-08-2023 17_07_28](https://github.com/Rahulprakash77/Two-stage-miller-compensated-OPAMP-design-/assets/130161648/922b4a52-288a-4c4a-81ac-d18e887e0699)

## 6. Calculation of Slew Rate.
We know that according to target specifications the slew rate should be 20V/μsec. Lets see how much we are actually getting. Below is the setup for calculation of SR. I connected inverting terminal to output in unity gain closed loop form and provided pulse input at the non-inverting terminal and observed the transient reponse.

![pmos2stage_trans](https://github.com/user-attachments/assets/0556170e-afb1-442c-a483-7634acc8f67e)

from the wave output we get SR = 26.17 v/usec

## 7. CMRR Plot

![pmos2stage_cmrr](https://github.com/user-attachments/assets/958e63b6-099f-41cb-994f-03875ab1c4fc)


## 8. PSRR Plot
![pmos2stage_psrr2](https://github.com/user-attachments/assets/b7f85af2-b525-433d-aeff-f90810a1ac32)


## 9. Noise Plot

![pmos2stage_noise2](https://github.com/user-attachments/assets/3df16002-7372-4619-b7b2-88776d8ddf7f)


# (B) PMOS Differential Input Two-Stage OPAMP
## 1. Declaring design specifications.
We are required to design an OPAMP having load capacitor CL = 2pF with the 1.1 volts power supply. I used the TSMC 40nm node technology for this project. An OPAMP was designed to best meet the following specificatons:

- 𝗗𝗶𝗳𝗳𝗲𝗿𝗲𝗻𝘁𝗶𝗮𝗹 𝘃𝗼𝗹𝘁𝗮𝗴𝗲 𝗴𝗮𝗶𝗻: 𝗔𝘃𝗱 ≥ 𝟱𝟬𝗱𝗕.
- 𝗼𝗽𝗲𝗿𝗮𝘁𝗶𝗻𝗴 𝘃𝗼𝗹𝘁𝗮𝗴𝗲 𝘃𝗱𝗱 = 𝟭.𝟭 𝘃
- 𝗦𝗹𝗲𝘄 𝗿𝗮𝘁𝗲: 𝗦𝗥 ≥ 𝟱 𝗩/μ𝗦.
- 𝗜𝗻𝗽𝘂𝘁 𝗰𝗼𝗺𝗺𝗼𝗻 𝗺𝗼𝗱𝗲 𝗿𝗮𝗻𝗴𝗲: 𝗜𝗖𝗠𝗥 (𝟮𝟬𝟬𝗺 , 𝟵𝟬𝟬𝗺)
- 𝗨𝗻𝗶𝘁𝘆 𝗚𝗮𝗶𝗻-𝗯𝗮𝗻𝗱𝘄𝗶𝗱𝘁𝗵: 𝗚𝗕 ≥ 𝟯𝟬𝗠𝗛𝘇 𝘄𝗶𝘁𝗵 𝗮 𝟮𝗽𝗙 𝗹𝗼𝗮𝗱 𝗰𝗮𝗽𝗮𝗰𝗶𝘁𝗮𝗻𝗰𝗲.
- 𝗣𝗵𝗮𝘀𝗲 𝗠𝗮𝗿𝗴𝗶𝗻: 𝗳(𝗚𝗕) ≥ 𝟲𝟬° 𝘄𝗶𝘁𝗵 𝗮 𝟮𝗽𝗙 𝗹𝗼𝗮𝗱 𝗰𝗮𝗽𝗮𝗰𝗶𝘁𝗮𝗻𝗰𝗲.
- 𝗣𝗼𝘄𝗲𝗿 𝗱𝗶𝘀𝘀𝗶𝗽𝗮𝘁𝗶𝗼𝗻: 𝗣𝗱𝗶𝘀𝘀 ≤ 𝟭𝗺𝗪.

## 2. calculating the DC parameter using Dc analysis of nmos and pmos (μpCox and μnCox)
upcox = 115u
uncox = 285u
 ![Virtuoso® Analog Design Environment L Editing_ RAHULP opampDC schematic@mirage 24-08-2023 14_12_36](https://github.com/Rahulprakash77/Two-stage-miller-compensated-OPAMP-design-/assets/130161648/9883e799-c44b-44f6-ab52-1aed1944b992)

## 3. calculating the min and max threshold value of m1 and m3 mos
Vtp = 485mV
Vtn = 460mV

![Virtuoso® Analog Design Environment L Editing_ RAHULP opampDC schematic@mirage 24-08-2023 15_07_26](https://github.com/Rahulprakash77/Two-stage-miller-compensated-OPAMP-design-/assets/130161648/5a0d3ce9-809a-4976-b80d-b86564ddff07)

## 4. Designing full circuit and make proper wire connection
![twoStage_pmos2](https://github.com/user-attachments/assets/1c0a62a8-f02c-4287-9317-129029bc161a)

## 5. Ac analysis ( Bode plot) 
**DCGain=49dB , GBW = 28.22MHz and Phase Margin = 64.32 , Bandwidth=128.5kHz**
![pmos2stage_gainphase](https://github.com/user-attachments/assets/a1816e62-3edf-4830-b2db-857926f866a3)


## 6. Calculation of Slew Rate.
We know that according to target specifications the slew rate should be 20V/μsec. Lets see how much we are actually getting. Below is the setup for calculation of SR. I connected inverting terminal to output in unity gain closed loop form and provided pulse input at the non-inverting terminal and observed the transient reponse.

![pmos2stage_transt](https://github.com/user-attachments/assets/8b351a5e-2eb5-4603-8516-d455b9f62e41)


from the wave output we get SR = 6.63 v/usec

## 7. CMRR Plot
![pmos2stage_cmrr](https://github.com/user-attachments/assets/050d5b9e-20da-434c-b652-8d34ed28526a)



## 8. PSRR Plot
![pmos2stage_psrr](https://github.com/user-attachments/assets/07121371-33d8-4c0a-bab5-aab70bfa897b)



## 9. Noise Plot
![pmos2stage_noise](https://github.com/user-attachments/assets/75991193-64c5-435a-ac39-08c9ed7567eb)


