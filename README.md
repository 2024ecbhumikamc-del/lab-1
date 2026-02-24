### Experiment-1-CS-amplifier-EC029


### DC analysis,AC analysis,Transfer characteristics and Transient Analysis of Common Source Amplifier
A common-source amplifier is a type of FET amplifier where the input signal is applied to the gate, and the output is taken from the drain. The source is typically grounded. It provides high voltage gain and **180-degree phase shift** (inversion) between the input and output. It’s widely used for amplifying weak signals in analog circuits, with the voltage gain determined by the load resistor and the transconductance of the FET.



### <u>Key Components and their roles</u>:
1. **Rd (Drain Resistor):** Provides the required voltage drop to amplify the signal.
2. **W (Transistor Width):** Affects the transconductance (gm), influencing gain and bandwidth.
3. **Vdd (Drain Supply Voltage):** Provides DC biasing for the NMOS transistor.
4. **AC Input (SINE source):** The test signal used to analyze circuit response.

   



**Circuit diagram:**
<img width="1321" height="593" alt="Screenshot 2026-02-24 171817" src="https://github.com/user-attachments/assets/11ec93cc-889f-432a-933a-01738c9226c4" />



## Given Parameters (From tsmc018.lib)
 
- Vth = 0.366 V  
- Tox = 4.1 × 10⁻⁹ m  
- μn (U0) = 273.809 cm²/V·s  
- εr (SiO₂) = 3.9  
- ε0 = 8.854 × 10⁻¹² F/m  
- Power constraint: P ≤ 1.2 mW  

Since the input DC bias at the gate is 0.9 V,

VGS = 0.9 V  

As VGS > Vth (0.9 V > 0.366 V),  
the NMOS operates in saturation region.






This report presents the DC analysis, AC analysis, Transient analysis of a common-source NMOS amplifier. The objective of this analysis is to determine the DC biasing conditions, gain and output impedence using Transient analysis, and to find frequency response using AC analysis.

## **Component Details:**
The circuit consists of a tsmc 180nm NMOS transistor (CMOSN), a drain resistor and two voltage sources. The drain resistor limits the current through the transistor and affects the small-signal gain. The NMOS transistor operates in saturation region, making it suitable for amplification.
**Model:** **CMOSN**

**Channel Length:** 180nm

**Channel Width:** 1.11um

**Threshold Voltage:** 0.366V

**Resistor:** 5 k ohm

**Supply Voltage:** 2V

**DC Voltage:** 0.9V

**Amplitude:** 10mV

**Frequency:** 1kHz


### THOERITICAL CALCULATION :

## Step 1: Calculate Drain Current Using Power Constraint

Using:

P = V × I  

0.4 × 10⁻³ = 2 × ID  

ID = (0.4 × 10⁻³) /2 

ID ≈ 2.00 × 10⁻⁴ A  

ID ≈ 0.200 mA  

## Step 2: Fix Q-Point

For maximum symmetrical swing:

VDS = VDD / 2  

VDS = 2 / 2  

VDS ≈ 1 V  

## Step 3: Calculate Drain Resistor (RD)

RD = (VDD − VDS) / ID  

RD = (2 − 1) / (2 × 10⁻⁴)  

RD ≈ 5 kΩ  

## Step 4: Calculate Oxide Capacitance (Cox)

First calculate oxide permittivity:

εox = εr × ε0  

εox = 3.9 × (8.854 × 10⁻¹²)  

εox ≈ 3.45 × 10⁻¹¹ F/m  

Now,

Cox = εox / Tox  

Cox = (3.45 × 10⁻¹¹) / (4.1 × 10⁻⁹)  

Cox ≈ 8.42 × 10⁻³ F/m²  

## Step 5: Calculate Process Transconductance Parameter (kn')

Convert mobility to SI units:

μn = 273.80 cm²/V·s  
= 0.02738 m²/V·s  

Now,

kn' = μn × Cox  

kn' = 0.02738 × (8.41 × 10⁻³)  

kn' ≈ 2.306 × 10⁻⁴ A/V²  

## Step 6: Calculate Required Transistor Width (W)

Using MOSFET saturation equation:

ID = (kn'/2) × (W/L) × (VGS − Vth)²  

Given:

VGS = 0.9 V  
Vth = 0.366 V  

(VGS − Vth) = 0.534 V  

L = 180 nm = 180 × 10⁻⁹ m  

Substituting:

2.00 × 10⁻⁴ = (2.30 × 10⁻⁴ / 2) × (W / 180 × 10⁻⁹) × (0.534)²  

Solving,

W ≈ 1.1 µm  



## Procedure:

1.Create a new folder and name it as project file.Save the LT spice file in this folder.

2.Name the mosfet as CMOSN and the length as 500nm and width as 1.11um initially.

3.**DC Analysis**: Set up the circuit as per the circuit diagram with proper connections ensuring valid circuit for further analysis. Apply the DC voltage of Vdd=2V and Vgs = 0.9 V . Go to simulate option in the tab and edit simulation command, click on DC analysis and press ok.(.op) Click on Run in the tab menu to get the DC operating point ,Vout and Id. 

4.**Transfer characteristics**: Transfer characteristics depict how the drain current (Id) varies with the gate-to-source voltage (Vgs).It's ltspice command is ".dc V2 0 2" Common-Source NMOS Amplifier: DC Voltage Transfer Characteristic (VTC).Now Run to see the response of drain current.

5.**Transient Analysis:** Apply a sine wave input of Vgs=0.9V with an amplitude of 10mV and frequency of 1kHz by going to advanced menu in the voltage setting option.go to simulate option in tab ,edit simulation command , click on transient analysis and give the stop time as 5m and click ok. Now Run to visualise the response of the circuit to a time varying signal.

6.**AC Analysis:** Go to spice directive and give the library file path for the simulator to access the data through the path . Go to simulate option in the tab , edit simulation command , click on AC analysis and mention the time of sweep as decade , no of points as 10 and frequency as 1kHz to 100GHz and click on ok. Now Run to analyze the gain and frequency response of the circui







### DC analysis:
<img width="1321" height="593" alt="Screenshot 2026-02-24 171817" src="https://github.com/user-attachments/assets/752a1a79-fe6f-47e3-915f-2d396dcdb74b" />



If the Power dissipation is 0.4mW across the resistor, then the current through the resistor is given by:
**Id** = Power/Voltage =  0.4m / 2 = **200 µA**

**Vov = Vgs - Vth = 0.9 - 0.36 = 0.534 V**.
As 'L' is 180nm and 'W' is 1.11um the Id value will be 156 µA. Keeping the L constant and start varying the width to get the required current Id value from the simulation.
| Width     | Current(Id) |
|:---------|:---:|
| 1.11um   | 156 µA|
| 1.2um    | 167 µA|
| 1.3um    | 178 µA|
|1.4um     | 189 µA|
|1.515um   | 200 µA|



<img width="627" height="467" alt="Screenshot 2026-02-24 122519" src="https://github.com/user-attachments/assets/5d88ea58-dfa9-49a5-91ea-6847f1788dd3" />



From the simulation result we got the approximate current value of **200 µA ≈ Id** and **Vout = 0.995 ~ 1 V**

The output load line equation is given by


**Vout = Vdd - (Id * Rd)**


   Rd = (Vdd - Vout) / Id

   
    = (2 - 0.995)/200 µA

    
   = 5k Ω

Therefore **Rd = 5 kΩ**

The DC operating point analysis confirms that the NMOS transistor operates in the saturation region with Id ≈ 200μA.


**Vds = Vout =  0.995 V**


Vov = Vgs - Vth = 0.9 - 0.366 = 0.534V


i.e **Vds > ( Vgs - Vth)**

### Transfer characteristics :

We know the equation for output voltage:

Vout = VDD − ID*R1

For VGS < VTH, the MOSFET is OFF. Therefore, ID = 0 and Vout = VDD.

For VGS > VTH, the MOSFET turns ON and current ID flows. Hence, Vout = VDD − ID*R1.

As VGS increases, ID increases. This increases the voltage drop across R1, which decreases the output voltage Vout.



**Circuit diagram:**

<img width="1362" height="578" alt="Screenshot 2026-02-24 172016" src="https://github.com/user-attachments/assets/0fef0c87-ee96-43ba-9ceb-43970d8d31ba" />







### Transient Analysis:

Transient analysis in a common-source amplifier examines how the amplifier reacts to time-varying inputs, such as step or sinusoidal signals. It helps assess the time-domain response, including key parameters like rise time, settling time, and distortion from capacitive effects. The analysis shows how quickly the output responds and whether there are any delays, overshoot, or instability.

For this experiment, we will find the gain and output impedence of the circuit.
For the same circuit, we will perform the transient analysis keeping the sinusoidal voltage signal  **DC offset as 0.9V**, and **amplitude 10mV**, and **frequency = 1kHz**
And the **AC amplitude as 1V**.
In the configure analysis select  **stop time as 5ms**. There is **180 degree phase shift** between input and output and a DC level phase shift observed.



**Circuit Diagram:**

<img width="1363" height="578" alt="Screenshot 2026-02-24 172121" src="https://github.com/user-attachments/assets/ef1bd1cb-f7da-4367-93a8-47f69e06d574" />



## Gain Calculation (From Transient Analysis)

From the transient waveform:

**Voltage Gain (Av)** = Vout / Vin  

Peak-to-peak values were measured from the graph.

**Output voltage:**

Vout(max) = 1.032V  
Vout(min) = 0.973 V  

Vout(pp) =   1.032V -0.973 V
Vout(pp) = 0.059 V 

**Input voltage:**

Vin(max) = 0.91  V  
Vin(min) = 0.8903  V  

Vin(pp) = 0.91  V - 0.8903  V  
Vin(pp) = 0.0197  

Therefore,
Av = Vout(pp) / Vin(pp)  

Av =  0.059 V  / 0.0197V  
Av ≈ 3 

**Gain in dB:**

Av(dB) = 20 log(Av)  

Av(dB) = 20 log(3)  
Av(dB) ≈ 9.54 dB  



## Theoretical Gain Calculation

For a Common Source amplifier:

Av = gm × RD  
gm = 2ID / (VGS − Vth)

Given:

ID = 0.2 mA  
VGS = 0.9 V  
Vth = 0.366 V  
RD = 5 kΩ  

**Overdrive voltage:**

Vov = VGS − Vth = 0.9 − 0.366 = 0.534 V  

**Transconductance:**

gm = (2 × 0.2 × 10⁻³) / 0.534  
gm ≈ 0.75 mS  

Therefore,

Av = gm × RD  
Av = (0.75 × 10⁻³) × (5000)  
Av ≈ 3.7 

**Gain in dB:**

Av(dB) = 20 log(3.7)  
Av(dB) ≈ 11.36 DB 

The simulated gain (3 ) is lower than the theoretical(3.7) value due to channel length modulation, output resistance effects, and other non-ideal device characteristics.





### AC analysis:

In this experiment, we will conduct an AC analysis to evaluate the frequency response of the circuit, including parameters such as gain, output impedance, and phase shift. By applying a small-signal AC input, we can assess how the circuit amplifies signals and how it behaves under varying frequencies.

For the same circuit, in the configure analysis select decade as type of sweep, with starting frequenciy o.1Hz and stop frequency as 100GHz.

**Circuit diagram:**

## AC Response Without Load Capacitor

<img width="1321" height="593" alt="Screenshot 2026-02-24 171817" src="https://github.com/user-attachments/assets/5358be05-6354-49a2-8639-4c7f9337af9f" />



<img width="1361" height="574" alt="Screenshot 2026-02-24 173350" src="https://github.com/user-attachments/assets/e2290907-bf57-4b28-9278-b00f4d9da090" />





**Voltage gain = Vout / Vin**

= 0.06/ 0.02= 3V/V

 **in dB = 20log10(Vout / Vin)**

= 20log10(3)

**in dB = 9.54 dB**

**frequency @ 9.54 - 3 = 6.54

**frequency = 56 GHz



## AC Response With Load Capacitor (CL = 10 pF)

<img width="1311" height="596" alt="Screenshot 2026-02-24 230233" src="https://github.com/user-attachments/assets/6d2b2aec-a226-4625-9c7c-c9bfa44f1e7f" />




<img width="1360" height="582" alt="Screenshot 2026-02-24 231639" src="https://github.com/user-attachments/assets/107c9ba9-0d1c-4296-b619-f44c50aa4741" />


From AC plot (with CL = 10 pF):

- Midband gain ≈ 3
- Gain in dB ≈ 9.54 dB
- 3 dB bandwidth ≈ 56.4 GHz
- Unity Gain Bandwidth (UGB) ≈ 150.23 MHz
- GBP ≈ 3 × 56.4 GHz
     ≈ 187 MHz (approx)





## OVERALL COMPARISON TABLE :

| Parameter | Theoretical Value | Practical (Simulation) Value | Reason for Variation |
|------------|------------------|-----------------------------|----------------------|
| Drain Current (ID) | ≈ 0.2 mA | ≈ 0.2 mA | Minor rounding and model accuracy differences |
| VDS (Q-point) | 1 V | ≈ 1 V | Slight deviation due to transistor model non-idealities |
| Drain Resistor (RD) | 5 kΩ | 5 kΩ | Directly calculated from design equation |
| Transistor Width (W) | 1.1 µm (calculated) |1.515 µm (adjusted) | Width tuned in simulation to achieve exact Q-point |
| Voltage Gain (Av) | 3 | 3.7 | Channel length modulation and output resistance effects |
| Gain (dB) | 9.54 dB | 11.36 dB | Practical gain reduced due to non-ideal device behavior |
| 3 dB Bandwidth | — | 56  GHz | Limited by parasitic capacitances |
| Unity Gain Bandwidth (UGB) | — | 150 MHz | Determined by dominant pole and device capacitances |
| Gain Bandwidth Product (GBP) | — | ≈ 187 MHz | Product of midband gain and bandwidth |





### Inference:

 **DC Analysis:**
  The transistor is working correctly in the saturation region, which is needed for amplification. The current flowing through the circuit is 200 µA, and the resistor value 5kΩ is verified. The output voltage is around 1V, and the input voltage is 0.9V. The transistor is properly biased for amplification.

 
**Transfer characteristics:**
The transfer characteristic curve shows that the transistor operates in the proper saturation (active) region for amplification. The Q-point lies in the linear region, ensuring proportional output response to input variations. The slope of the curve confirms stable gain, and minimal distortion is observed within the operating range. Overall, the circuit is properly biased for effective amplification.


**AC Analysis:**
The circuit maintains a stable gain over different frequencies, proving it works well for amplification. The voltage gain is 3 (or 9.54 dB), and the -3 dB point (where gain drops) confirms its frequency limits. Simulation and theoretical results are in close agreement, with minor variations due to parasitic effects.


**Transient Analysis:**
The output signal is amplified and flipped by 180° (inverted), which is expected in a Common Source amplifier. The gain of the circuit is around 3. The circuit has an output resistance of 5kΩ, affecting how it drives the next stage in a system.

 


















