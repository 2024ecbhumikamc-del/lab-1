# Experiment-1-EC029-CS-amplifier
# DC analysis,AC analysis,Transfer characteristics and Transient Analysis of Common Source Amplifier
A common-source amplifier is a type of FET amplifier where the input signal is applied to the gate, and the output is taken from the drain. The source is typically grounded. It provides high voltage gain and **180-degree phase shift** (inversion) between the input and output. It’s widely used for amplifying weak signals in analog circuits, with the voltage gain determined by the load resistor and the transconductance of the FET.

### <u>Key Components and their roles</u>:
1. **Rd (Drain Resistor):** Provides the required voltage drop to amplify the signal.
2. **W (Transistor Width):** Affects the transconductance (gm), influencing gain and bandwidth.
3. **Vdd (Drain Supply Voltage):** Provides DC biasing for the NMOS transistor.
4. **AC Input (SINE source):** The test signal used to analyze circuit response.

**Circuit diagram:**
<img width="1321" height="593" alt="Screenshot 2026-02-24 171817" src="https://github.com/user-attachments/assets/11ec93cc-889f-432a-933a-01738c9226c4" />


This report presents the DC analysis, AC analysis, Transient analysis of a common-source NMOS amplifier. The objective of this analysis is to determine the DC biasing conditions, gain and output impedence using Transient analysis, and to find frequency response using AC analysis.

## **Component Details:**
The circuit consists of a TSMC 180nm NMOS transistor (CMOSN), a drain resistor and two voltage sources. The drain resistor limits the current through the transistor and affects the small-signal gain. The NMOS transistor operates in saturation region, making it suitable for amplification.
**Model:** **CMOSN**

**Channel Length:** 180nm

**Channel Width:** 1.11um

**Threshold Voltage:** 0.366V

**Resistor:** 5000 ohm

**Supply Voltage:** 2V

**DC Voltage:** 0.9V

**Amplitude:** 10mV

**Frequency:** 1kHz

# Procedure:

1.Create a new folder and name it as project file.Save the LT spice file in this folder.

2.Name the mosfet as CMOSN and the length as 500nm and width as 1.11um initially.

3.**DC Analysis**: Set up the circuit as per the circuit diagram with proper connections ensuring valid circuit for further analysis. Apply the DC voltage of Vdd=2V and Vgs = 0.9 V . Go to simulate option in the tab and edit simulation command, click on DC analysis and press ok.(.op) Click on Run in the tab menu to get the DC operating point ,Vout and Id.

4.**Transient Analysis:** Apply a sine wave input of Vgs=0.9V with an amplitude of 10mV and frequency of 1kHz by going to advanced menu in the voltage setting option.go to simulate option in tab ,edit simulation command , click on transient analysis and give the stop time as 5m and click ok. Now Run to visualise the response of the circuit to a time varying signal.

5.**AC Analysis:** Go to spice directive and give the library file path for the simulator to access the data through the path . Go to simulate option in the tab , edit simulation command , click on AC analysis and mention the time of sweep as decade , no of points as 10 and frequency as 1kHz to 100GHz and click on ok. Now Run to analyze the gain and frequency response of the circuit


# DC analysis:
<img width="1321" height="593" alt="Screenshot 2026-02-24 171817" src="https://github.com/user-attachments/assets/752a1a79-fe6f-47e3-915f-2d396dcdb74b" />



If the Power dissipation is 0.4mW across the resistor, then the current through the resistor is given by:
**Id** = Power/Voltage =  0.4m/ 2 = **200 µA**

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

   
    = (2 - 1)/200 µA

    
   = 5000 Ω

Therefore **Rd = 5000 Ω**

The DC operating point analysis confirms that the NMOS transistor operates in the saturation region with Id ≈ 200μA.


**Vds = Vout =  1 V**


Vov = Vgs - Vth = 0.9 - 0.366 = 0.534V


i.e **Vds > ( Vgs - Vth)**


# AC analysis:

In this experiment, we will conduct an AC analysis to evaluate the frequency response of the circuit, including parameters such as gain, output impedance, and phase shift. By applying a small-signal AC input, we can assess how the circuit amplifies signals and how it behaves under varying frequencies.

For the same circuit, in the configure analysis select decade as type of sweep, with starting frequenciy o.1Hz and stop frequency as 100GHz.

**Circuit diagram:**
<img width="1361" height="574" alt="Screenshot 2026-02-24 173350" src="https://github.com/user-attachments/assets/8eea301b-8994-4002-a2fc-57981ba05afe" />


**Voltage gain = Vout / Vin**

= 0.06/ 0.02= 3V/V

 **in dB = 20log10(Vout / Vin)**


     = 20log10(3)

  

**in dB = 9.54 dB**


# Transient Analysis:

Transient analysis in a common-source amplifier examines how the amplifier reacts to time-varying inputs, such as step or sinusoidal signals. It helps assess the time-domain response, including key parameters like rise time, settling time, and distortion from capacitive effects. The analysis shows how quickly the output responds and whether there are any delays, overshoot, or instability.

For this experiment, we will find the gain and output impedence of the circuit.
For the same circuit, we will perform the transient analysis keeping the sinusoidal voltage signal  **DC offset as 0.9V**, and **amplitude 10mV**, and **frequency = 1kHz**
And the **AC amplitude as 1V**.
In the configure analysis select  **stop time as 5ms**. There is **180 degree phase shift** between input and output and a DC level phase shift observed.

**Circuit Diagram:**
<img width="1363" height="578" alt="Screenshot 2026-02-24 172121" src="https://github.com/user-attachments/assets/ef1bd1cb-f7da-4367-93a8-47f69e06d574" />


Overall gain (Av) = Vout / Vin
      = 3

From calculations:

**gm = 2(Id)/(Vov)**

i.e Vov = Vgs - Vth


   = 2(200μ) / ( 0.534)

   
**gm = 749 μA/V**

Rout = Rd = 5000 Ω


Overall gain :

**Av = gm * Rout**
             
    =  749 μ * 5000
    
   **Av = 3.745**


   # Results:
   
Id = 200μA

Vov = 0.534 V

Vout = 1 V

Voltage gain = 3 V/V (in dB = 9.54 dB)

gm = 749 μA/V

Overall gain =  3.745V/V

# Inference:

 **DC Analysis:**
  The transistor is working correctly in the saturation region, which is needed for amplification. The current flowing through the circuit is 200 µA, and the resistor value 5kΩ is verified. The output voltage is around 1V, and the input voltage is 0.9V. The transistor is properly biased for amplification.


**AC Analysis:**
The circuit maintains a stable gain over different frequencies, proving it works well for amplification. The voltage gain is 3 (or 9.54 dB), and the -3 dB point (where gain drops) confirms its frequency limits. Simulation and theoretical results are in close agreement, with minor variations due to parasitic effects.


**Transient Analysis:**
The output signal is amplified and flipped by 180° (inverted), which is expected in a Common Source amplifier. The gain of the circuit is around 3. The circuit has an output resistance of 5kΩ, affecting how it drives the next stage in a system.











