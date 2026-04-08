The Screen Automation System is an advanced industrial control solution designed to automate the alignment of printing screens using real-time computer vision. In traditional setups, aligning a screen for a 3-axis stage is done manually, which is slow and prone to error. This project digitizes that process by creating a "closed-loop" system between high-level vision sensors and industrial PLCs.

The Problem
Industrial screen printing requires micron-level precision across three axes (X, Y, and Z/Theta). Manual alignment causes downtime and material waste.

The Solution
We utilize a Distributed Intelligence model. Instead of taxing a single controller, we split the workload:

Vision Sensing: A Master RPi 5 uses the Sony IMX708 sensor (Camera Module 3) to detect alignment markers (e.g., plus marks or edges) at high frame rates.

Data Gateway: A Slave RPi 5 handles the network overhead and protocol translation, ensuring the Master's vision loop remains uninterrupted by Modbus latency.

Industrial Execution: A Delta AS228T PLC manages the high-speed pulse outputs (PTO) required to drive the 3-axis stepper system smoothly.

System Workflow
Capture: Master RPi 5 detects the screen position using OpenCV.

Calculate: The system computes the error offset between the current position and the target home position.

Communicate: The offset is sent via UDP over Wi-Fi to the Slave RPi.

Translate: The Slave converts the coordinates into 16-bit or 32-bit integers compatible with Modbus TCP registers.

Actuate: The Delta PLC reads these registers and triggers the stepper drivers to move the motors until the vision sensor confirms alignment.

Technical Challenges Overcome
Latency Optimization: Used UDP sockets instead of TCP for faster data throughput between Raspberry Pis.

Protocol Bridging: Successfully interfaced Python-based IoT hardware with industrial PLC registers using the pymodbus library.

Precision Mapping: Calibrated pixel-to-millimeter ratios to ensure the vision system accurately directs the physical motor movement.
