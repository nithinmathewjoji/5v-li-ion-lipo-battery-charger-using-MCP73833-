
# 5v-li-ion-lipo-battery-charger-using-MCP73833

## Table of Contents
- [Description](#Description)
- [Features](#Features)
- [Typical Application Circuit Diagram](#Typica-Application-circuit-diagram)
- [Components and Connections](#Components-and-Connections)
- [How to Build](#how-to-build)
- [Applications](#applications)
- [Contributing](#contributing)
- [License](#license)


# Description

The MCP73833/4 is a highly advanced linear charge
management controller for use in space-limited, cost
sensitive applications. The MCP73833/4 is available in
a 10-Lead, 3 mm x 3 mm DFN package or a 10-Lead,
MSOP package. Along with its small physical size, the
low number of external components required makes
the MCP73833/4 ideally suited for portable
applications. For applications charging from a USB
port, the MCP73833/4 can adhere to all the
specifications governing the USB power bus.
The MCP73833/4 employs a constant current/constant
voltage charge algorithm with selectable preconditioning and charge termination. The constant voltage
regulation is fixed with four available options: 4.20V,
4.35V, 4.40V, or 4.50V, to accomodate new, emerging
battery charging requirements. The constant current
value is set with one external resistor. The MCP73833/
4 limits the charge current based on die temperature
during high power or high ambient conditions. This
thermal regulation optimizes the charge cycle time
while maintaining device reliability.
Several options are available for the preconditioning
threshold, preconditioning current value, charge
termination value, and automatic recharge threshold.
The preconditioning value and charge termination
value are set as a ratio, or percentage, of the
programmed constant current value. Preconditioning
can be set to 100%. Refer to Section 1.0 “Electrical
Characteristics” for available options and the
“Product Indentification System” for standard
options.
The MCP73833/4 is fully specified over the ambient
temperature range of -40°C to +85°C



## Features

• Complete Linear Charge Management Controller
- Integrated Pass Transistor
- Integrated Current Sense
- Integrated Reverse Discharge Protection
• Constant Current / Constant Voltage Operation 
with Thermal Regulation
• High Accuracy Preset Voltage Regulation:
- 4.2V, 4.35V, 4.4V, or 4.5V, + 0.75%
• Programmable Charge Current: 1A Maximum
• Preconditioning of Deeply Depleted Cells 
- Selectable Current Ratio
- Selectable Voltage Threshold
• Automatic End-of-Charge Control
- Selectable Current Threshold
- Selectable Safety Time Period
• Automatic Recharge
- Selectable Voltage Threshold
• Two Charge Status Outputs
• Cell Temperature Monitor
• Low-Dropout Linear Regulator Mode
• Automatic Power-Down when Input Power 
Removed
• Under Voltage Lockout
• Numerous Selectable Options Available for a 
Variety of Applications:
- Refer to Section 1.0 “Electrical 
Characteristics” for Selectable Options
- Refer to the Product Identification System for 
Standard Options
• Available Packages:
- DFN-10 (3 mm x 3 mm)
- MSOP-10

# Typica-Application-circuit-diagram
![Typica-Application-circuit-diagram](https://github.com/user-attachments/assets/9d7c4255-e3f1-42b1-ab00-7c44e064a513)

## Circuit Explanation

### Components-and-Connections
1. **MCP73833 Battery Charger IC**:
   - **VBAT (Pins 9, 10)**: Connects to the positive terminal of the Li-ion battery. It handles the charging output to the battery.
   - **VDD (Pins 1, 2)**: Connects to the 5V input from the USB-C VBUS pin.
   - **PG (Pin 7)**: Connected to an LED through a 470Ω resistor. This pin indicates whether the USB power supply is connected (Power Good).
   - **STAT1 (Pin 3) and STAT2 (Pin 4)**: Connected to LEDs through 470Ω resistors to indicate charging status. 
     - **STAT1 ON** (STAT2 OFF) indicates charging.
     - **STAT2 ON** (STAT1 OFF) indicates charging complete.
2. **USB Type-C Connector**:
   - **VBUS**: Connected to **VDD** pins (1, 2) of MCP73833.
   - **GND**: Connected to ground (VSS) of the MCP73833.
   - **CC1 and CC2**: Each connected to ground through a 5.1 kΩ resistor, to request 5V from the USB-C source.
3. **Thermistor (THERM Pin 8)**:
   - The thermistor connected to **THERM** is optional but recommended for monitoring battery temperature. This setup provides thermal protection by adjusting charging current if the temperature rises.

### Status LED Explanation
- **PG LED**: Connected to **PG (Pin 7)**, lights up when power is connected.
- **STAT1 LED**: Connected to **STAT1 (Pin 3)**, lights up when the battery is charging.
- **STAT2 LED**: Connected to **STAT2 (Pin 4)**, lights up when the battery is fully charged.

### Charging Current (PROG Pin 6)
- The **PROG pin** (Pin 6) determines the charging current based on the connected resistor. In this circuit:
  - **I<sub>CHG</sub> = 1000 / R<sub>PROG</sub>**
  - With a 1kΩ resistor connected to **PROG**, the charging current will be approximately **1000 mA**.

### Typical Application Circuit

![Circuit Diagram](link_to_image)  <!-- Insert the circuit image link here -->

### Component List
| Component          | Value   | Description                              |
|--------------------|---------|------------------------------------------|
| MCP73833           | -       | Battery Charger IC                       |
| USB Type-C Connector | -       | USB-C input for 5V power                 |
| Resistor           | 5.1kΩ   | Connects CC1 and CC2 pins to GND         |
| Resistor           | 470Ω    | Limits current to status LEDs            |
| Resistor           | 1kΩ     | Sets charging current to 1000 mA         |
| Capacitor          | 1µF     | Decoupling capacitor on VDD and VBAT     |
| Thermistor (Optional) | 10kΩ | For thermal protection                    |
| LED                | -       | For power and charge status indicators   |

## Usage Instructions

1. **Powering the Charger**:
   - Connect a USB-C power source (5V) to the USB-C connector. The **PG LED** should light up to indicate that power is available.
   
2. **Connecting the Battery**:
   - Connect the positive terminal of your single-cell lithium-ion battery to the **VBAT** pin (Pins 9 and 10).
   - Connect the negative terminal of the battery to **GND** (VSS).

3. **Charging Status**:
   - When the battery is charging, the **STAT1 LED** will be ON.
   - When the battery is fully charged, the **STAT2 LED** will be ON, and the **STAT1 LED** will turn OFF.

4. **Customizing Charging Current**:
   - To adjust the charging current, change the resistor connected to **PROG (Pin 6)**.
   - For example, a 2kΩ resistor will set the charging current to **500 mA** (I<sub>CHG</sub> = 1000 / R<sub>PROG</sub>).

5. **Thermal Monitoring** (Optional):
   - If using a thermistor, connect it between **THERM** (Pin 8) and **GND**. This will adjust charging current based on battery temperature to prevent overheating.

## Safety Notes
- Use a high-quality Li-ion battery with built-in protection circuits.
- Ensure proper heat dissipation as Li-ion charging can generate heat.
- Always verify connections before powering the circuit to avoid short circuits or overcharging.

---

This README provides a comprehensive overview of your USB Type-C Li-ion battery charger project. You can customize it further or add specific details based on your testing and usage. Let me know if you need additional sections!

[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](https://choosealicense.com/licenses/mit/)
