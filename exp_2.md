# Experiment-2___029

### Circuit - 1
Design and comparative analysis of three amplifier configurations using 180nm CMOS in LTspice.
## AIM

## To design and analyze a Common Source (CS) amplifier with PMOS active load using 180nm CMOS technology and evaluate its DC, Transient and AC performance.
## GIVEN SPECIFICATIONS

| Parameter | Value |
|------------|--------|
| VDD | 2 V |
| Power Constraint | ≤ 0.4 mW |
| Load Capacitor (CL) | 10 pF |
| Channel Length (L) | 180 nm |
| Assumed Overdrive Voltage (Vov) | 0.25 V |
| Source Voltage Drop (VRS) | 0.2 V |
---

# CIRCUIT 1  
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
P ≤ 0.4 mW  

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

### 1️⃣ Practical Gain (From Transient Analysis)

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







### Circuit - 2


---

# Circuit Diagram

<img width="1366" height="720" alt="Screenshot 2026-03-18 011637" src="https://github.com/user-attachments/assets/af106025-dc04-47d3-9f7d-28257f0f0221" />

---

# Given Design Parameters

| Parameter              | Symbol | Value    |
| ---------------------- | ------ | -------- |
| Supply Voltage         | VDD    | 2 V      |
| Desired Drain Current  | ID     | 200 µA   |
| Maximum Power          | Pcons  | ≤ 1.2 mW |
| Overdrive Voltage      | VOV    | 0.25 V   |
| Load Capacitance       | CL     | 10 pF     |
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

After tuning the widths, the circuit achieved:

ID = 200 µA
VOUT = 1 V

---

# DC Sweep (Transfer Characteristic)

<img width="1918" height="855" alt="transfer curve" src="https://github.com/user-attachments/assets/e99cc4d4-4abc-46cd-91f1-633cdb31bac2" />

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

## Input Signal

<img width="1917" height="851" src="https://github.com/user-attachments/assets/53b720da-3642-4794-9b44-c4139ef3b32f" />

## Output Signal

<img width="1918" height="852" src="https://github.com/user-attachments/assets/99d4468c-4c52-4ee9-b35b-3fe7ec09a49a" />

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

<img width="1918" height="851" src="https://github.com/user-attachments/assets/deb7b771-90da-4c60-ae43-4cfffbe11d20" />

Measured values:

Lower cutoff frequency ≈ 0 Hz
Upper cutoff frequency ≈ 145.41 MHz

Bandwidth:

BW ≈ 145.41 MHz

---

# Unity Gain Bandwidth

<img width="1911" height="881" src="https://github.com/user-attachments/assets/d063dda5-be25-4ab3-a797-ff54c4b69674" />

From simulation:

UGB ≈ 469.31 MHz

From gain-bandwidth product:

UGB ≈ 494.39 MHz

Both values are close, confirming the validity of the design.

---

# Conclusion

The cascode amplifier was successfully designed using 180 nm CMOS technology.
All transistors operate in the saturation region, ensuring proper biasing and stable operation.

Key observations:

* The cascode structure significantly increases output resistance and voltage gain.
* Simulation results confirm the expected gain-bandwidth relationship.
* The amplifier achieves a wide bandwidth suitable for high-speed analog applications.

Overall, the circuit demonstrates the effectiveness of the cascode topology for achieving *high gain with good bandwidth performance* in modern CMOS analog designs.
