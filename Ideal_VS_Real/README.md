
## Task: Ideal vs. Practical Diode Analysis (LTspice)

## 1. Circuit Setup
I simulated a simple series circuit consisting of:
- **V1:** DC Voltage Source (Swept from -5V to 5V)
- **R1:** 1kΩ Resistor (Current limiter)
- **D1:** Diode (Switched between Ideal and 1N4148 models)

## 2. Schematics

### Ideal Diode Model
<img width="1600" height="807" alt="ideal_schematic" src="https://github.com/user-attachments/assets/8b827c24-7e51-4a30-b30f-66588b1f8dd6" />


### Practical Diode Model (1N4148)
<img width="1601" height="796" alt="real" src="https://github.com/user-attachments/assets/bc5a15f6-d047-427e-b49b-dc469b91dd96" />

![Real Schematic](real_schematic.png)

## 3. Simulation Results & Comparison

### A. Difference in Turn-on Voltage
- **Ideal:** The simulation shows the diode turning on exactly at **0V**. There is no barrier potential; current flows immediately as soon as voltage is positive.
- **1N4148:** The practical diode requires approximately **0.65V to 0.7V** to overcome the silicon PN junction potential barrier. Below this voltage, the current is negligible (leakage current only).

### B. Difference in Current Behavior
- **Ideal:** Once forward-biased (V > 0), the I-V curve is a vertical line. This implies zero internal resistance ($R_s = 0$). The current is limited only by the external resistor ($I = V_{source} / R$).
- **1N4148:** The curve shows an exponential "knee." Even when conducting, the diode has a dynamic resistance. The voltage drop across the diode remains relatively constant at ~0.7V regardless of current (within limits), which subtracts from the voltage available for the resistor.

### C. Why Ideal Models Are Still Used
Ideal models are essential for **initial hand calculations** and **logic design**. They simplify non-linear differential equations into simple ON/OFF states. For example, in a 12V power supply rectifier, ignoring the 0.7V drop results in less than 6% error, which is acceptable for quick topology analysis. It allows engineers to determine circuit states (conducting vs. blocking) without complex math.

### D. When Ideal Models Become Inaccurate
Ideal models fail in:
1.  **Low Voltage Circuits:** In 3.3V or 1.8V logic, a 0.7V drop is 20-40% of the supply voltage. Ignoring it leads to massive errors in current calculation.
2.  **Power Efficiency:** In battery-powered devices, $P_{loss} = V_f \times I$. An ideal model predicts 0W loss, but a real diode generates heat.
3.  **Precision Analog:** In signal clipping or temperature sensing, the exact exponential behavior of the diode is critical, which the ideal model completely misses.

## 4. Conclusion
While the ideal diode is a useful abstraction for understanding circuit logic, the 1N4148 simulation demonstrates the physical reality of semiconductor behavior: the barrier potential and non-linear resistance are fundamental properties that must be considered in precise electronic design.
