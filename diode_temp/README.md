Temperature Dependence of Diodes

Simulation Setup
I simulated a 1N4148 diode in series with a 1kΩ resistor using LTspice. I used the `.temp 25 75` directive to compare behavior at room temperature (25°C) and elevated temperature (75°C).
A DC sweep was performed from -5V to 5V.
<img width="1602" height="800" alt="diode_temp" src="https://github.com/user-attachments/assets/3d16c885-5c99-4eb8-9f7e-c51c46872b48" />



Observations

Forward Voltage
At 25 degC: The diode turns on at approximately 0.7V.
At 75 degC: The turn-on voltage shifts left to approximately 0.6V.
Change: A decrease of roughly 100mV.
Physics: This is due to the increase in intrinsic carrier concentration in the semiconductor material as temperature rises.
The increased thermal energy reduces the energy barrier (bandgap) required for carriers to cross the junction, lowering the forward voltage drop. The typical coefficient is -2mV/°C for silicon.

Reverse Current
25 degC: Reverse leakage current is very small.
At 75°C: Reverse leakage current increases significantly.
Physics: Reverse saturation current is thermally generated. As temperature increases, more electron-hole pairs are generated thermally, increasing the leakage current exponentially. It roughly doubles for every 10°C increase.

## Why This Matters in Real Systems
Thermal Runaway (Power Electronics)
In power rectifiers or high-current applications, as the diode heats up, its forward voltage drops.
Higher Current, More Power Dissipation.
More Power, More Heat.
This creates a positive feedback loop called Thermal Runaway. If not managed with proper heatsinking, the diode can destroy itself.

### 2. Precision Circuit Errors
In analog circuits (like temperature sensors or bandgap voltage references), the -2mV/°C coefficient is a major source of error. If a circuit is designed to be precise at 25°C, it may drift significantly at 75°C, 
causing logic errors or measurement inaccuracies. Engineers must use temperature compensation techniques to mitigate this.

### 3. Standby Power Consumption
In battery-powered devices (IoT, phones), reverse leakage current increases with temperature. A device left in a hot car (75°C+) might drain its battery much faster than expected due to increased leakage 
in reverse-biased protection diodes.
