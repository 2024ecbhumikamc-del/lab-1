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







