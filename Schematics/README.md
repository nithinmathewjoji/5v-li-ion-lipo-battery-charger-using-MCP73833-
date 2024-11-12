# detailed circuit explanation for your **USB Type-C Li-ion Battery Charger** project using the **MCP73833** IC:

## Table of Contents
- [Circuit Explanation](#circuit-explanation)
  - [Power Input and USB Type-C Configuration](#power-input-and-usb-type-c-configuration)
  - [Battery Charging Control](#battery-charging-control)
  - [Status LED Indicators](#status-led-indicators)
  - [Charging Current Configuration (PROG Pin)](#charging-current-configuration-prog-pin)
  - [Thermal Monitoring (THERM Pin)](#thermal-monitoring-therm-pin)
  - [Detailed Component List](#detailed-component-list)


## Circuit Explanation

This section provides an in-depth explanation of each part of the circuit for the USB Type-C Li-ion Battery Charger, which is powered by the **MCP73833** IC. This IC is a versatile, single-cell, Li-ion battery charger with built-in protection features, making it suitable for safe and efficient charging from a 5V USB Type-C input.

### Power Input and USB Type-C Configuration

1. **USB Type-C Connector**: The USB Type-C connector is the input power source. It provides 5V from any standard USB Type-C power adapter or port. 
   - **VBUS Pin (5V)**: This pin on the USB Type-C connector supplies 5V and connects directly to the **VDD** pins (Pins 1 and 2) of the MCP73833, providing the operating voltage for the IC and powering the charging circuitry.
   - **GND Pin**: This pin connects to the ground of the entire circuit, ensuring a common reference point for all components.
   - **CC1 and CC2 Pins**: These configuration channel pins are connected to ground through **5.1kΩ resistors**. This configuration signals the USB-C source that the device is expecting a 5V supply (not requiring higher voltages, such as 9V or 12V). This setup ensures compatibility with standard USB-C power sources that provide 5V output.
   - **EH Pin**: This pin is connected to the **Power Good (PG)** output (Pin 7) of the MCP73833. By connecting this, the circuit can detect if VBUS is present or not. When power is supplied, the PG pin goes low, which can be used to turn on a Power Good LED.

2. **Decoupling Capacitor (1µF)**: A **1µF ceramic capacitor** is connected between **VDD** and **GND** to stabilize the power supply and filter any high-frequency noise. This capacitor is essential for ensuring that the MCP73833 receives a clean 5V signal, especially important in USB applications where voltage fluctuations may occur.

### Battery Charging Control

1. **Battery Positive Terminal (VBAT - Pins 9 and 10)**: The VBAT pins connect to the positive terminal of the single-cell Li-ion battery. This is the output from the MCP73833, where it supplies a regulated current and voltage to charge the battery safely.
   - The MCP73833 controls the charging process by adjusting the output to maintain a stable charging voltage (typically 4.2V for a single Li-ion cell) and a controlled current, ensuring efficient charging.

2. **Battery Negative Terminal (GND - Pin 5)**: The ground terminal of the battery connects to the circuit's common ground, providing the return path for the current. This ground connection is shared by all other components in the circuit.

### Status LED Indicators

The MCP73833 features two status indicators, **STAT1** and **STAT2**, which provide real-time feedback on the charging state using LEDs.

1. **Power Good LED (PG Pin - Pin 7)**:
   - The **PG** pin is connected to an LED via a **470Ω resistor**. This LED turns on when a valid power source (5V from USB-C) is connected. When VBUS power is present, the PG pin goes low, causing current to flow through the LED, illuminating it.
   - This LED indicates that the charger is connected to power and ready to charge the battery.

2. **Charging Status LED (STAT1 - Pin 3)**:
   - **STAT1** is connected to another LED through a **470Ω resistor**. This LED turns on while the battery is charging. The MCP73833 pulls **STAT1** low during charging, which allows current to pass through the LED and illuminates it.
   - When the charging process is in progress, this LED provides a clear visual indicator.

3. **Charge Complete LED (STAT2 - Pin 4)**:
   - **STAT2** is connected to a third LED via a **470Ω resistor**. This LED turns on when the battery is fully charged.
   - When the battery reaches the fully charged state (typically 4.2V for a single-cell Li-ion battery), **STAT2** goes low, turning on the LED. This allows the user to see that charging is complete.

### Charging Current Configuration (PROG Pin)

The **PROG** pin (Pin 6) allows for adjustment of the charging current using an external resistor. The charging current, ** $I_{CHG}$ **, is determined by the following formula:

$I_{CHG} = \frac{1000}{R_{PROG}}$]

To set the charging current:
- **1kΩ Resistor**: Provides a charging current of **1000mA** (1A).
- **2kΩ Resistor**: Provides a charging current of **500mA**.
- **4kΩ Resistor**: Provides a charging current of **250mA**.

For example, if you want to limit the charging current to 500mA, use a 2kΩ resistor on the **PROG** pin. This flexibility allows you to adjust the charging speed based on the battery capacity and desired charging rate.

### Thermal Monitoring (THERM Pin)

The **THERM** pin (Pin 8) provides thermal monitoring and allows the charger to respond to temperature changes, which is crucial for battery safety.

1. **Thermistor Setup**: The **THERM** pin is typically connected to a **10kΩ thermistor** (temperature-sensitive resistor) in series with a fixed resistor. The thermistor is placed close to the battery or within the battery pack to measure the temperature during charging.
   - **Purpose**: The MCP73833 can reduce or stop charging if the temperature exceeds safe limits, preventing potential overheating or thermal runaway.
   - **Function**: As the temperature increases, the resistance of the thermistor changes. When the thermistor detects a high temperature, it sends a signal to the MCP73833, which can then reduce or suspend charging to ensure safety.

This thermal regulation feature is essential for protecting the battery, particularly in compact applications where heat buildup might be an issue.

### Detailed Component List

| Component            | Value            | Purpose                                          |
|----------------------|------------------|--------------------------------------------------|
| MCP73833             | -                | Main charging IC for Li-ion battery              |
| USB Type-C Connector | -                | Input power source, provides 5V from USB         |
| Decoupling Capacitor | 1µF              | Stabilizes input voltage from USB                |
| Resistor             | 470Ω (x3)        | Current limiting for status LEDs                 |
| Resistor             | 1kΩ, 2kΩ, etc.   | Sets charging current via PROG pin               |
| LED                  | Red/Green/Yellow | Visual indicators for power, charging, complete  |
| Thermistor           | 10kΩ             | Monitors battery temperature for safety          |
| Resistors (CC1, CC2) | 5.1kΩ each       | Sets USB-C power mode to 5V                      |

