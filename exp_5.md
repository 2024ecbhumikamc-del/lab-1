## EXPERIMENT - 5

## Design op-amp based circuits and analyze the following response:

- Supply voltage: ±Vcc = 12V  
- Output voltage: Vout(p) = 9V  
- Load resistance: RL = 1kΩ  
- frequency : f = 500Hz  

### (d) Non-inverting Amplifier
Design a non-inverting amplifier with voltage gain:
- Av = 6 V/V

### (e) Voltage Follower
Design a voltage follower with:
- RL = 360Ω

### (d) Non-Inverting Amplifier

### non-inverting amplifier circuit:

 <img width="1364" height="597" alt="Screenshot 2026-04-28 211542" src="https://github.com/user-attachments/assets/96b9c2e4-e705-4677-ae0a-9a7a5eac4d8d" />


  
### Theory
A non-inverting amplifier is an op-amp circuit where the input signal is applied to the non-inverting terminal (+). The inverting terminal (-) is connected to the output through a feedback network.

Main points:
- Output is in phase with input
- High input impedance
- Gain depends on feedback resistors

Voltage gain formula:
Av = 1 + (Rf / R1)

Given:
Av = 6

So,
6 = 1 + (Rf / R1)
Rf / R1 = 5

Example:
R1 = 1k ohm
Rf = 5k ohm
Vin = 4.5(peak)
Av = 1 + (5000 / 1000) = 6
Theoretical Vout = 6 * 4.5V = 27V

---

### Working Principle
- Input voltage is applied to the non-inverting terminal
- Due to high gain of op-amp, voltage at both terminals becomes almost equal
- This is called virtual short condition
- Feedback network sends part of output to inverting terminal
- Op-amp adjusts output to maintain equal input voltages
- Output is amplified version of input

Output equation:
Vout = Av × Vin

## transient analysis:

<img width="1358" height="605" alt="Screenshot 2026-04-28 211640" src="https://github.com/user-attachments/assets/74194430-fdac-4da8-8b54-e58cf03e494e" />

## Transient Analysis – Simulation Results
- **Amplifier Gain:**    The circuit operates with a voltage gain of approximately **6**.
- **Input Signal:**    A sine wave with a peak amplitude of **4.5 V** is applied.
- **Output Behavior:**    The output voltage saturates at approximately **±11.8 V**.
- **Reason for Clipping:**    The expected output swing (~27 V) exceeds the available supply rails (**±12 V**).    Hence, the output waveform gets clipped at the limits.

- **Inference:**    This indicates that the op-amp is operating in the **saturation region**.
-  For an undistorted output waveform, the input amplitude should be **less than 2 V**.

### FREQUENCY RESPONSE ANALYSIS

<img width="1365" height="580" alt="Screenshot 2026-04-28 213514" src="https://github.com/user-attachments/assets/863d2709-e078-467a-ad7a-cb6b235564e7" />


#### 1. Low-Frequency Region (1 Hz – ~100 kHz)
- Gain is constant at ≈ 15–16 dB  
- Output is in-phase with input (0° phase shift)  
- Amplifier operates in ideal region  

✔ This matches the theoretical gain

---

#### 2. Cut-off Frequency and Bandwidth (~150 kHz – 170 kHz)
- Gain drops by 3 dB from its midband value  
- This defines the bandwidth of the amplifier  

Bandwidth ≈ 150 kHz – 170 kHz  

---

#### 3. Mid-Frequency Roll-off (~200 kHz – few MHz)
- Gain decreases gradually  
- Slope ≈ -20 dB/decade  

✔ Indicates a single dominant pole system

---

#### 4. High-Frequency Region (> few MHz)
- Gain drops rapidly  
- Phase shifts toward -180°  
- Effects of internal capacitances dominate  

---

#### 5. Very High-Frequency Region (> GHz up to 100 GHz)
- Irregular peaks and distortions observed  
- Caused by:
  - Parasitic capacitances
  - Numerical limitations of simulation
  - Non-ideal op-amp model behavior  



---

### GAIN-BANDWIDTH PRODUCT (GBW)

For µA741:

GBW ≈ 1 MHz  

Bandwidth = GBW / Gain  
Bandwidth ≈ 1 MHz / 6 ≈ 166 kHz  

✔ The calculated bandwidth closely matches the simulated value

---

### PHASE RESPONSE

- Starts near 0° (non-inverting behavior)  
- Gradually decreases with frequency  
- Approaches -180° at high frequencies  

---

### KEY RESULTS

| Parameter | Value |
|----------|------|
| Gain (Av) | 6 |
| Gain (dB) | ≈ 15.56 dB |
| Bandwidth | ~150 kHz – 170 kHz |
| Roll-off Rate | -20 dB/decade |
| Phase Shift | 0° to ~ -180° |
| Valid Frequency Range | Up to few MHz |
| Simulated Range | 1 Hz – 100 GHz |

---

### IMPORTANT REMARK

Although the AC sweep is performed up to 100 GHz, the :contentReference[oaicite:0]{index=0} is practically limited to low-frequency applications (≤ few MHz). Therefore, only the low and mid-frequency regions are considered valid for analysis.

---

### CONCLUSION

The AC analysis confirms that the non-inverting amplifier:

- Achieves the expected gain of ≈ 15.56 dB  
- Has a bandwidth of approximately 150–170 kHz  
- Exhibits a single-pole roll-off characteristic  
- Follows the gain-bandwidth limitation of the µA741 op-amp  

Thus, the simulation results are in close agreement with theoretical predictions, validating the performance of the designed circuit.









