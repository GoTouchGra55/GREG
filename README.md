# GREG

GREG is a custom SBC designed to act as the main computer for a rover. It is built around the Allwinner T527 SoC and includes custom memory, power management, connectivity, camera, display, sensor, and motor-control hardware.

CAD REPO - [REPO](https://github.com/unknowngamer69/Orion-Rover)

## Hardware

- SoC: Allwinner T527
- RAM: 2 GB Samsung LPDDR4
- PMIC: AXP717-family
- Storage: MicroSD
- Networking: Ethernet
- Connectivity: 2× USB-A + 1× USB-C
- Display: HDMI + 5" LCD interface
- Cameras: 3-camera support (2 with multiplexing)
- Sensors: 6× ToF + LiDAR
- Debug: UART/debug connector
- Expansion: External breakout connector

## Motor Driver

Motor control is handled by a separate PCB instead of the T527.

- MCU: STM32G4
- Motor drivers: 3× DRV8262
- Motors: 6× brushed DC motors with built-in encoders

Separating the motor controller from the SBC keeps the main PCB free from clutter and noise.

## Schematics

SBC - [SEE SCHEMATICS](<Schematics(PDF)/GREG.pdf>)  
Motor Driver - [SEE SCHEMATICS](<Schematics(PDF)/GREG-MTRDRV.pdf>)

## Routing

(To be done in the upcoming week!)

## Authors

Shaurya (Electronics) - [@GoTouchGra55](https://github.com/GoTouchGra55)  
Krish (CAD) - [@unknowngamer69](https://github.com/unknowngamer69)
