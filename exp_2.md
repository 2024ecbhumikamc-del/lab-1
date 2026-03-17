# Experiment-2___029
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


