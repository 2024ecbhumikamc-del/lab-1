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

  ## (d) Non-Inverting Amplifier

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

---

- Output and input are in same phase
- Gain is always greater than or equal to 1
- Circuit is stable due to negative feedback


  ### non-inverting amplifier circuit:

  <img width="1363" height="611" alt="Screenshot 2026-04-28 210239" src="https://github.com/user-attachments/assets/88b9e1eb-94fe-4fa9-9096-dec3daef8e7d" />






