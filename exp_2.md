# LIC_Amplifier_Configurations_Experiment-2
Design and comparative analysis of three amplifier configurations using 180nm CMOS in LTspice.
## AIM

To design and analyze a Common Source (CS) amplifier with PMOS active load using 180nm CMOS technology and evaluate its DC, Transient and AC performance.
## GIVEN SPECIFICATIONS

| Parameter | Value |
|------------|--------|
| VDD | 2 V |
| Power Constraint | ≤ 0.4 mW |
| Load Capacitor (CL) | 1 pF |
| Channel Length (L) | 180 nm |
| Assumed Overdrive Voltage (Vov) | 0.25 V |
| Source Voltage Drop (VRS) | 0.2 V |
---

# CIRCUIT 1  
## Common Source Amplifier with PMOS Active Load
### Circuit Diagram

![Circuit2](https://raw.githubusercontent.com/Sinchanak181/LIC_Amplifier_Configurations_Exp2/main/circuit2.png)


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

![Circuit2_DC](https://raw.githubusercontent.com/Sinchanak181/LIC_Amplifier_Configurations_Exp2/main/circuit2_dc.png)

### Observations
- ID(M1) ≈ 0.335 mA  
- ID(M2) ≈ 0.335 mA  
- Vout ≈ 0.946 V  
- Source voltage ≈ 0.20 V  

The simulated drain current matches the calculated value (0.334 mA), confirming correct DC biasing.
### Width Tuning and Validation

| Parameter | Calculated | Final (Simulated) |
|------------|------------|------------------|
| Wn | 8.36 µm | 48.32 µm |
| Wp | 19.7 µm | 62.286 µm |

**Reason for Increase in Width:**

- Hand calculation assumes ideal square-law MOSFET model.
- 180nm model includes mobility degradation and short channel effects.
- Effective transconductance is lower in practical model.
- Larger W is required to maintain ID ≈ 0.334 mA.
- Width adjustment ensures proper Q-point and saturation region operation.

  ---

## Transient Analysis

A sinusoidal input signal was applied at the gate terminal:

Vin = SINE (0.9 10m 1k)

Transient command used:

.tran 5m
### Input Waveform (Vin)

![Circuit1_Vout](https://raw.githubusercontent.com/Sinchanak181/LIC_Amplifier_Configurations_Exp2/main/Circuit1_Vin.png.jpg)

---

### Output Waveform (Vout)

![Circuit1_Vin](https://raw.githubusercontent.com/Sinchanak181/LIC_Amplifier_Configurations_Exp2/main/Circuit1_Vout.png.jpg)

---

### Combined Input and Output Waveforms

![Circuit1_Vout](https://raw.githubusercontent.com/Sinchanak181/LIC_Amplifier_Configurations_Exp2/main/Circuit1_Vin_Vout.png.jpg)

---

## Gain Analysis

### 1️⃣ Practical Gain (From Transient Analysis)

Measured from waveform:

Vout(max) = 1.0873 V  
Vout(min) = 0.84293 V  

Vin(max) = 0.81999 V  
Vin(min) = 0.800 V  

Vout(pp) = 0.24437 V  
Vin(pp) = 0.01999 V  

Av (practical) = 0.24437 / 0.01999  
Av = 9.723  

Gain (dB):

Av(dB) = 20 log(9.723)  
Av(dB) = 19.75 dB  

---

##  Theoretical Gain Calculation

For CS amplifier with PMOS active load and source degeneration:

Av = − gm (ro1 || ro2) / (1 + gm Rs)

#### Transconductance (gm)

gm = 2ID / VOV  

gm = 2 × (0.334 × 10⁻³) / 0.25  

gm = 2.672 × 10⁻³ S  

gm ≈ 2.67 mS  

#### Output Resistance (ro)

ro = 1 / (λ ID)

Assuming λ = 0.1 V⁻¹ (180 nm technology)

ro1 = 1 / (0.1 × 0.334 × 10⁻³)

ro1 ≈ 29.94 kΩ  

Since ro1 ≈ ro2,

ro(eq) = ro1 || ro2  

ro(eq) ≈ 14.97 kΩ  

#### Voltage Gain

Av = − (2.672 × 10⁻³ × 14.97 × 10³) / (1 + 2.672 × 10⁻³ × 598.8)

Av ≈ −15.38 V/V  

Gain (dB):

Av(dB) = 20 log(15.38)

Av(dB) ≈ 23.74 dB

**Theoretical Gain (Linear)** = 15.38 V/V  
**Theoretical Gain (dB)** = 23.74 dB  

**Practical Gain (Transient)** = 9.723 V/V  
**Practical Gain (dB)** = 19.75 dB

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

.ac dec 10 0.1 100M

The frequency response was obtained to extract midband gain, 3dB bandwidth, and high-frequency cutoff.
### AC Frequency Response

![Circuit1_AC](https://raw.githubusercontent.com/Sinchanak181/LIC_Amplifier_Configurations_Exp2/main/Circuit1_AC_Response.png)

### Extracted Parameters

| Parameter | Value |
|-----------|-------|
| Midband Gain | 19.75 dB |
| 3dB Gain | 16.75 dB |
| Bandwidth (fH) | 219.12 MHz |

Bandwidth is determined at the frequency where gain drops by 3 dB from midband value.

### Gain Bandwidth Product (GBP)

Midband gain (linear):

Av = 10^(19.75 / 20)  
Av ≈ 9.72  

GBP = Av × Bandwidth  

GBP = 9.72 × 219.12 MHz  
GBP ≈ 2.13 GHz

### Observation
- Amplifier shows flat midband gain region.
- Gain decreases at high frequency due to parasitic capacitances.
- Bandwidth ≈ 219 MHz.
- Bandwidth Product ≈ 2.13 GHz.

