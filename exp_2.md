### Experiment-2___029



## Experiment 2A: To design and analyze a Common Source (CS) amplifier with PMOS active load using 180nm CMOS technology and evaluate its DC, Transient and AC performance.
## GIVEN SPECIFICATIONS

| Parameter | Value |
|------------|--------|
| VDD | 2 V |
| Power Constraint | ≤ 1.2 mW |
| Load Capacitor (CL) | 1 pF |
| Channel Length (L) | 180 nm |
| Assumed Overdrive Voltage (Vov) | 0.25 V |
| Source Voltage Drop (VRS) | 0.2 V |
---

# CIRCUIT - 1  
## Common Source Amplifier with PMOS Active Load
### Circuit Diagram

<img width="1366" height="768" alt="Screenshot 2026-03-17 235515" src="https://github.com/user-attachments/assets/1ca018b8-f7c5-4922-a5e8-8a930c39d355" />



### Circuit Description

This circuit is a **Common Source (CS) amplifier with PMOS active load**.

- **M1 (NMOS)** acts as the amplifying transistor.
- **M2 (PMOS)** acts as an active load to increase gain.
- **RS** provides source degeneration for bias stabilization.
- **VB1** biases the PMOS transistor.
- Input signal is applied at the gate of M1.
- Output is taken at the drain node (Vout).

The circuit is designed to operate all transistors in the **saturation region** to ensure proper amplification.

## DC Analysis and Design Calculations

### Step 1: Drain Current from Power Constraint

Given:
VDD = 2 V  
P ≤ 1.2 mW  

P = VDD × ID  

ID = 0.4 mW / 2 
ID = 0.2 mA  

---

### Step 2: NMOS (M1) Width Calculation

Saturation current equation:

ID = (1/2) kn' (W/L) (Vov)²  

Rearranging for W:

W = (2 ID L) / (kn' (Vov)²)

Substituting values:

kn' = 2.30 × 10⁻⁴ A/V²  
L = 180 nm  
Vov = 0.25 V  
ID = 0.2 mA  

Wn ≈ 4.99 µm  

---

### Step 3: PMOS (M2) Width Calculation

ID = (1/2) kp' (W/L) (Vov)²  

W = (2 ID L) / (kp' (Vov)²)

kp' = 9.73 × 10⁻⁵ A/V²  

Wp ≈ 11.89 µm  

---

### Step 4: Source Resistor (RS)

Given VRS = 0.2 V  

RS = VRS / ID  
RS = 0.2 / 0.2mA  

RS ≈ 1 kΩ  

---

### Final Designed Values

| Parameter | Value |
|------------|--------|
| ID | 0.2 mA |
| Wn | 4.99 µm |
| Wp | 11.89 µm |
| RS | 1000 Ω |

The above calculations ensure proper DC biasing and saturation region operation.
## DC Simulation Result

<img width="638" height="515" alt="Screenshot 2026-03-17 234915" src="https://github.com/user-attachments/assets/75d2a668-13b1-4d79-93d9-78d70212d316" />


### Observations
- ID(M1) ≈ 0.2 mA  
- ID(M2) ≈ - 0.2 mA  
- Vout ≈ 1.2 V  
- Source voltage ≈ 0.20 V  

The simulated drain current matches the calculated value (0.2 mA), confirming correct DC biasing.
### Width Tuning and Validation

| Parameter | Calculated | Final (Simulated) |
|------------|------------|------------------|
| Wn | 4.99 µm | 25 µm |
| Wp | 11.89 µm | 36 µm |

**Reason for Increase in Width:**

- Hand calculation assumes ideal square-law MOSFET model.
- 180nm model includes mobility degradation and short channel effects.
- Effective transconductance is lower in practical model.
- Larger W is required to maintain ID ≈ 0.2 mA.
- Width adjustment ensures proper Q-point and saturation region operation.

  ---

## Transient Analysis

A sinusoidal input signal was applied at the gate terminal:

Vin = SINE (0.81 10m 1k)

Transient command used:

.tran 5m

### Input and Output Waveforms

<img width="1366" height="768" alt="Screenshot 2026-03-17 235045" src="https://github.com/user-attachments/assets/695e10dc-0d39-4a58-9864-191d3511dfa2" />

---

## Gain Analysis

### 1️ Practical Gain (From Transient Analysis)

Measured from waveform:

Vout(max) = 1.36 V  
Vout(min) = 1.11 V  

Vin(max) = 0.82 V  
Vin(min) = 0.80 V  

Vout(pp) = 0.25 V  
Vin(pp) = 0.02 V  

Av (practical) = 0.25 / 0.02  
Av = 12.5  

Gain (dB):

Av(dB) = 20 log(12.5)  
Av(dB) = 21.9 dB  

---

##  Theoretical Gain Calculation

For CS amplifier with PMOS active load and source degeneration:

Av = − gm (ro1 || ro2) / (1 + gm Rs)

#### Transconductance (gm)

gm = 2ID / VOV  

gm = 2 × (0.2 × 10⁻³) / 0.25  

gm = 1.6 × 10⁻³ S  

gm ≈ 1.6 mS  

#### Output Resistance (ro)

ro = 1 / (λ ID)

Assuming λ = 0.1 V⁻¹ (180 nm technology)

ro1 = 1 / (0.1 × 0.2 × 10⁻³)

ro1 ≈ 50 kΩ  

Since ro1 ≈ ro2,

ro(eq) = ro1 || ro2  

ro(eq) ≈ 25 kΩ  

#### Voltage Gain

Av = − (1.6 × 10⁻³ × 25 × 10³) / (1 + 1.6 × 10⁻³ × 1000)

Av ≈ −15 V/V  

Gain (dB):

Av(dB) = 20 log(15)

Av(dB) ≈ 23.52 dB

**Theoretical Gain (Linear)** = −15 V/V  
  
**Theoretical Gain (dB)** = 23.52 dB

**Practical Gain (Transient)** = 12.5 V/V  
**Practical Gain (dB)** = 21.9 dB

##  Reason for Variation Between Theoretical and Practical Gain

The theoretical gain assumes ideal device operation with constant output resistance and neglects higher-order effects.

However, in LTspice simulation:

• Channel length modulation affects output resistance.  
• Parasitic capacitances influence small-signal behavior.  
• Bias-dependent variation in gm occurs.  
• Source degeneration reduces effective gain.  

Hence, practical gain (19.75 dB) is lower than theoretical gain (23.74 dB).

## AC Analysis

AC simulation command used:

.ac dec 10 0.1 100G

The frequency response was obtained to extract midband gain, 3dB bandwidth, and high-frequency cutoff.
### AC Frequency Response

<img width="1366" height="768" alt="Screenshot 2026-03-17 235120" src="https://github.com/user-attachments/assets/876b1d35-f24d-43da-a142-8b4192790d82" />


### Extracted Parameters

| Parameter | Value |
|-----------|-------|
| Midband Gain | 21.9 dB |
| 3dB Gain | 18.6 dB |
| Bandwidth (fH) | 91.73 GHz |

Bandwidth is determined at the frequency where gain drops by 3 dB from midband value.


### Observation
- Amplifier shows flat midband gain region.
- Gain decreases at high frequency due to parasitic capacitances.
- Bandwidth ≈ 91.73 GHz.







# Experiment 2B:  Design CS amplifier with PMOS active load and NMOS current source degeneration in LTSPICE.


# Circuit - 2

<img width="1366" height="720" alt="Screenshot 2026-03-18 011637" src="https://github.com/user-attachments/assets/af106025-dc04-47d3-9f7d-28257f0f0221" />

---

# Given Design Parameters

| Parameter              | Symbol | Value    |
| ---------------------- | ------ | -------- |
| Supply Voltage         | VDD    | 2 V      |
| Desired Drain Current  | ID     | 200 µA   |
| Maximum Power          | Pcons  | ≤ 1.2 mW |
| Overdrive Voltage      | VOV    | 0.25 V   |
| Load Capacitance       | CL     | 1 pF     |
| Channel Length         | L      | 180 nm   |
| NMOS Threshold Voltage | Vthn   | 0.36 V   |
| PMOS Threshold Voltage | Vthp   | 0.39 V   |

---

# Circuit Operation

The cascode amplifier consists of three major devices:

*M1 – Input NMOS (Common Source Stage)*
This transistor converts the small input voltage variations into a corresponding drain current.

*M3 – Bias Current Source*
This device provides a constant bias current and replaces the need for a degeneration resistor.

*M2 – PMOS Active Load*
The PMOS transistor acts as a high-resistance load, improving voltage gain and increasing output swing.

---

# Advantage of Cascode Configuration

In a simple common source amplifier, the output resistance is approximately

ro1 || ro2

However, the cascode arrangement significantly increases the effective output resistance.

Approximate output resistance:

gm1 · ro1 · ro3

Since voltage gain is proportional to

Av ≈ gm × Rout

an increase in output resistance results in a *larger voltage gain without increasing device dimensions*.

---

# DC Analysis

## Power Consumption Check

Assuming the designed drain current:

ID = 200 µA

Power consumption:

P = VDD × ID
P = 2 × 200 µA
P = 0.4 mW

Since

0.4 mW ≤ 1.2 mW

the design satisfies the power constraint.

---

## Output Bias Point

For symmetrical signal swing,

Vout ≈ VDD / 2

Vout = 2 / 2 = 1 V

---

# NMOS Bias Calculations

## Transistor M3

Gate-source voltage:

VGS3 = VOV + VTH

VGS3 = 0.25 + 0.36
VGS3 = 0.61 V

Assume source node voltage

VS1 = 0.3 V

Drain-source voltage:

VDS3 = VS1 = 0.3 V

### Saturation Check

Condition 1:

VGS ≥ VTH
0.61 ≥ 0.36 

Condition 2:

VDS ≥ VOV
0.3 ≥ 0.25 

Therefore *M3 operates in saturation*.

---

## Transistor M1

Gate-source voltage:

VGS1 = VOV + VTH
VGS1 = 0.61 V

Gate voltage:

VG1 = VS1 + VGS1
VG1 = 0.3 + 0.61
VG1 = 0.91 V

Drain-source voltage:

VDS1 = VOUT − VS1
VDS1 = 1 − 0.3
VDS1 = 0.7 V

### Saturation Verification

0.61 ≥ 0.36 
0.7 ≥ 0.25 

Thus *M1 also remains in saturation*.

---

# PMOS Load Transistor (M2)

For PMOS:

VSG2 = VOV + |VTH|

VSG2 = 0.25 + 0.39
VSG2 = 0.64 V

Gate voltage:

VSG2 = VS2 − VG2

0.64 = 2 − VG2

VG2 = 1.36 V

Drain-source voltage:

VSD2 = VDD − VOUT
VSD2 = 2 − 1
VSD2 = 1 V

### Saturation Condition

0.64 ≥ 0.39 
1 ≥ 0.25 

Hence *M2 operates in saturation*.

---

# Transistor Width Calculation

For NMOS devices:

ID = (1/2) μn Cox (W/L) (VOV)²

Using process parameters:

Kn′ = μnCox ≈ 230 × 10⁻⁶ A/V²

After substituting ID = 200 µA:

Calculated width

Wn ≈ 5 µm

---

For PMOS:

ID = (1/2) μp Cox (W/L) (VOV)²

Resulting width

Wp ≈ 11.8 µm

---

# Initial Simulation Result

<img width="1860" height="851" alt="initial result" src="https://github.com/user-attachments/assets/4a56d35e-2242-4ca8-a475-c8b9abb1e88c" />

Simulation output:

ID = 63.5 µA
Vout = 1.46 V

Current scaling factor:

200 / 63.5 = 3.14

Thus transistor widths were scaled accordingly.

---

# Final Device Dimensions

| Device    | Width   |
| --------- | ------- |
| M1        | 18.5 µm |
| M3        | 16.6 µm |
| PMOS Load | 34.6 µm |

# Final Simulation Result

<img width="638" height="515" alt="Screenshot 2026-03-18 012419" src="https://github.com/user-attachments/assets/9c05719e-06ab-43aa-94cc-3cbc76e57ab8" />



After tuning the widths, the circuit achieved:

ID = 200 µA
VOUT = 1 V

---

# DC Sweep (Transfer Characteristic)

<img width="1366" height="720" alt="Screenshot 2026-03-18 012608" src="https://github.com/user-attachments/assets/8bc12058-14a7-4cf4-8238-a1fe4a426c08" />

The voltage transfer characteristic shows three operating regions:

### Cut-off Region

For input voltage below threshold, transistor M1 is OFF.
The output node remains near VDD.

### Active Region

When the input exceeds threshold, the transistors operate in saturation.
Small variations in Vin produce large changes in Vout, giving maximum gain.

### Linear Region

For higher Vin values, the output drops significantly and the NMOS devices enter the triode region, limiting the output swing.

---

# Transient Analysis

## Input Signal and Output waveform

<img width="1366" height="720" alt="Screenshot 2026-03-18 012801" src="https://github.com/user-attachments/assets/5e7820df-e1fe-4845-825a-a8f7ad3dce29" />


---

## Measured Results

| Parameter           | Value    |
| ------------------- | -------- |
| Input Peak-to-Peak  | 19.33 mV |
| Output Peak-to-Peak | 0.066 V  |
| Voltage Gain        | 3.41 V/V |
| Gain (dB)           | 10.65 dB |
| Frequency           | 1 kHz    |
| Phase Shift         | 180°     |

Since the circuit is based on a common source stage, the output signal is *inverted relative to the input*.

---

# Small Signal Gain Calculation

Transconductance:

gm = 2ID / VOV

gm = (2 × 200µA) / 0.25
gm = 1.6 mS

Output resistances:

ro1 = 1/(λn ID) ≈ 50 kΩ
ro2 = 50 kΩ

PMOS:

ro3 ≈ 41.6 kΩ

Effective resistance:

ro_eff ≈ 22.7 kΩ

Voltage gain:

Av ≈ −0.448 V/V

Gain in dB:

Av ≈ 6.97 dB

---

# Gain Comparison

| Metric     | Theoretical | Simulated |
| ---------- | ----------- | --------- |
| Gain (V/V) | 0.448       | 3.41      |
| Gain (dB)  | 6.97        | 10.65     |

The simulated gain is larger because the practical transistor parameters produce higher output resistance than assumed in theoretical calculations.

---

# AC Analysis

## Frequency Response

<img width="1366" height="720" alt="Screenshot 2026-03-18 013007" src="https://github.com/user-attachments/assets/ca87e2c2-fb6d-4384-8d6c-c9b276b264a1" />

Measured values:

Lower cutoff frequency ≈ 0 Hz
Upper cutoff frequency ≈ 145.41 MHz

Bandwidth:

BW ≈ 145.41 MHz

---



# Conclusion

The cascode amplifier was successfully designed using 180 nm CMOS technology.
All transistors operate in the saturation region, ensuring proper biasing and stable operation.

Key observations:

* The cascode structure significantly increases output resistance and voltage gain.
* Simulation results confirm the expected gain-bandwidth relationship.
* The amplifier achieves a wide bandwidth suitable for high-speed analog applications.

Overall, the circuit demonstrates the effectiveness of the cascode topology for achieving *high gain with good bandwidth performance* in modern CMOS analog designs.





# Experiment 2C: Common Source Amplifier with Diode-Connected NMOS Current Source and PMOS Active Load

# Circuit - 3 

<img width="885" height="621" alt="Image" src="https://github.com/user-attachments/assets/7e35739d-3ef4-4dcf-8cdc-452e369256a4" />

# Design Calculation:

Given Specifications:
### Design Parameters:

| Parameter | Symbol | Value |
|-----------|--------|-------|
| Supply Voltage | VDD | 2 V |
| Drain Current | ID | 200 µA |
| Overdrive Voltage | VOV | 0.25 V |
| Power Constraint | P | ≤ 1.2 mW |
| Relative Permittivity | εr | 3.9 |
| Permittivity of Free Space | ε0 | 8.854 × 10⁻¹² F/m |
| Oxide Thickness | tox | 4.1 × 10⁻⁹ m |
| Electron Mobility | μn | 273.809 cm²/Vs |
| Hole Mobility | μp | 115.689 cm²/Vs |

- M3 MOSFET(Always in saturation region):
  
 VGS3=VOV+VTH
 
   =0.25+0.36=0.61V
     
  VGS3=VG3-VS3
  
   =VG3=0.61V=VS1
      
- M1(nmos):
  
  VGS1=VOV+VTH
  
   =0.25+0.36=0.61V
  
  VGS1=VG1-VS1
  
   =VG1-0.61V
  
  VG1=1.22=**VIN**
  
- M2(PMOS Active load)
  
  VGS3=VOV+VTH

   0.25+0.39=0.64V
  
  VB1=VDD-VSG3
  
     =2-0.64=1.36V
  
- Width Calculation :
  
  Current equation is given as :
  
  ID = (1/2) kn' (W/L) (VOV)^2
  
  For M1 and M3 on substitution width comes to be 5 µm anD for M2 is  11.82 µm

# DC Operating Point:
To obtain desired operating point width of mosfet is varied 

### Transistor Dimensions

| Transistor | Type | Width (W) | Length (L) |
|-----------|------|-----------|-----------|
| M1 | NMOS | 14.3 µm | 0.18 µm |
| M2 | PMOS | 35 µm | 0.18 µm |
| M3 | NMOS | 14.3 µm | 0.18 µm |


<img width="851" height="486" alt="Image" src="https://github.com/user-attachments/assets/4424d991-990d-4942-bdcf-aa955b826268" />

The DC operating point (Q-point) defines the steady-state voltages and currents of the circuit when no input signal is applied. It ensures that all MOSFETs operate in the saturation region, which is necessary for proper amplification.

In this circuit, the biasing is adjusted by selecting appropriate transistor dimensions so that the drain current remains close to the specified 200 µA, while maintaining sufficient overdrive voltage. This guarantees stable operation and allows the amplifier to produce a linear output without distortion.



## DC Sweep Analysis:  

<img width="1917" height="605" alt="Image" src="https://github.com/user-attachments/assets/00fc67b6-376b-44d1-98c5-3e2601e79467" />

DC sweep analysis is used to study how the output voltage varies with respect to the input voltage (VIN). By sweeping VIN over a range, the transfer characteristics of the amplifier are obtained.

From the curve, the region where the output varies linearly with input indicates proper amplification. This also helps verify that the transistor remains in saturation over the operating range and confirms the correctness of the chosen biasing conditions.



## Transient Analysis:
<img width="1917" height="872" alt="Image" src="https://github.com/user-attachments/assets/0ac84d80-0c75-40c7-8cd4-8cb2de174067" />

<img width="1917" height="878" alt="Image" src="https://github.com/user-attachments/assets/3b4512e5-af0c-47b9-a002-6847755114f9" />

### Gain Calculation: 
Gain(Av)=vout(p-p)/vin(p-p)

       =355.506mV/19.709mV
       
        =18.03V/V
Gain (dB)=20*log(Av)

         = 25.12dB
### Theoritical gain:

Av = - gm1 × ro2/(1+gm1/gm3)
   = - (2mS × 50kΩ)/2
Av = -50 V/V

Gain in dB: Av(dB) = 20 log(50)
Av(dB) = 33.97 dB

## AC Analysis :

<img width="1912" height="690" alt="Image" src="https://github.com/user-attachments/assets/7506a113-d023-4374-9d5b-dc28e06b3542" />

 1. Midband Voltage Gain:
- midband gain=25.33dB
- |Av|dB = 20 log10(|Av|)
  |Av| = 10^(25.33/20)
  |Av| ≈ 18.47 V/V

3. −3 dB Cutoff Frequency (Bandwidth):
 - The bandwidth is determined by the frequency at which the gain drops by 3 dB from its maximum midband value.  
 - that is frequency at (25.33-3)dB which is **343.332MHz**
4. Unity Gain Frequency (fT):
   - This is the frequency at which the amplifier stops amplifying and the gain drops to 0 dB (a linear gain of 1 V/V).
   - frequency at 45dB is **490MHz**




# Inferance:
Circuit 1: 
- Resistive Source Degeneration Element: A standard passive resistor ($R_1 = 1\text{k}\Omega$).
- Characteristics: This is the classical approach. The resistor provides linear feedback, stabilizing the DC operating point and increasing the input range. However, in integrated circuit (IC) design, passive resistors like this can consume a significant amount of silicon area.

Circuit 2:
- Current Source Degeneration Element: An NMOS transistor ($M_3$) biased with a constant DC voltage ($V_3 = 0.61\text{V}$) at its gate.
- Characteristics: As long as $M_3$ is biased in the saturation region, it acts as a constant DC current source. This provides a very high incremental (AC) resistance while allowing you to control the exact DC tail current flowing through the amplifier.

Circuit 3: Diode-Connected Source Degeneration
- Degeneration Element: An NMOS transistor ($M_3$) configured as a "diode-connected" device (its gate is tied directly to its drain).
- Characteristics: A diode-connected transistor is always in saturation and acts as an active resistor. Its small-signal resistance is approximately $1/g_{m3}$. This is highly preferred in CMOS IC design because it replaces the bulky passive resistor from Circuit 1 with a much smaller MOSFET that scales well with the rest of the circuit.




#  Overall Comparison of CS Amplifier Configurations (Experiment 2A, 2B, 2C)

| Parameter | Circuit 1: CS + PMOS Load + RS | Circuit 2: CS + PMOS Load + NMOS Current Source | Circuit 3: CS + PMOS Load + Diode NMOS |
|----------|--------------------------------|-----------------------------------------------|----------------------------------------|
| Technology | 180 nm CMOS | 180 nm CMOS | 180 nm CMOS |
| Supply Voltage (VDD) | 2 V | 2 V | 2 V |
| Drain Current (ID) | 0.2 mA | 0.2 mA | 0.2 mA |
| Power Consumption | 0.4 mW | 0.4 mW | ≤ 1.2 mW |
| Degeneration Type | Resistor (1 kΩ) | NMOS Current Source | Diode-connected NMOS |
| Design Complexity | Simple | Moderate | Moderate |
| Area Efficiency | Low (bulky resistor) | High | High |
| Bias Stability | Good | Very Good | Moderate |
| Output Voltage (Vout) | ≈ 1.2 V | ≈ 1 V | ≈ 1 V |
| NMOS Width (Wn) | 25 µm | 18.5 µm | 14.3 µm |
| PMOS Width (Wp) | 36 µm | 34.6 µm | 35 µm |
| Extra Transistor | No | Yes (M3: 16.6 µm) | Yes (M3: 14.3 µm) |
| Theoretical Gain (V/V) | −15 | −0.448 | −50 |
| Theoretical Gain (dB) | 23.52 dB | 6.97 dB | 33.97 dB |
| Practical Gain (V/V) | 12.5 | 3.41 | 18.03 |
| Practical Gain (dB) | 21.9 dB | 10.65 dB | 25.12 dB |
| Midband Gain | 21.9 dB | ~10.65 dB | 25.33 dB |
| Bandwidth | 91.73 GHz | 145.41 MHz | 343.33 MHz |
| Frequency Performance | Excellent | Moderate | Good |
| Best Feature | High Bandwidth | Best Stability | Highest Gain |
| IC Suitability | Low | High | High |



