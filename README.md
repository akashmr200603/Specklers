# Hardware-Accelerated stLSCI on PolarFire SoC

**PolarFire FPGA Design Contest 2026 Submission**
**Track:** Track 1 – PolarFire SoC Discovery Kit

## Project Overview
This repository contains the system architecture for a low-power, edge-integrated **Spatio-Temporal Laser Speckle Contrast Imaging (stLSCI)** system built on the Microchip PolarFire SoC Discovery Kit. 

Non-invasive, high-resolution imaging of microvascular blood flow is critical for neurosurgery, stroke research, and dermatology. Currently, LSCI relies heavily on bulky desktop PCs or GPUs to compute the intensive spatio-temporal math ($K = \sigma / \mu$) required to convert raw speckle patterns into blood flow maps. 

We propose moving this computation entirely to the edge. By leveraging the low-power FPGA fabric and DSP blocks of the PolarFire SoC, our system performs real-time spatio-temporal contrast calculations (7x7 spatial window, 30-frame temporal depth) on a 720p 60fps video stream. The onboard RISC-V Microprocessor Subsystem (MSS) orchestrates the camera via I2C and streams the processed, lightweight blood-flow contrast map to a host display via Gigabit Ethernet.

## Innovation
Calculating spatio-temporal contrast across a 30-frame depth at 60 fps typically overwhelms embedded memory bandwidth. To solve this, our architecture leverages a novel "rolling accumulator" utilizing the SoC's DDR4 controller and internal LSRAM line buffers. By updating the historical sums ($\Sigma X$ and $\Sigma X^2$) per pixel rather than recalculating the entire 30-frame buffer from scratch, we reduce DDR4 bandwidth usage by over 80%.

## Hardware Requirements
*   **Microchip PolarFire SoC Discovery Kit**
*   **Camera:** MIPI CSI-2 Monochrome Global Shutter Camera (OV9281)
*   **Optics:** 785nm Coherent Laser Diode with diffuser / He-Ne Laser Diode with diffuser
*   **Host Display:** PC receiving Gigabit Ethernet UDP stream

## Repository Content
*   `System_Block_Diagram.pdf`: The architectural block diagram detailing the hardware/software partitioning between the FPGA fabric, DDR4, and the RISC-V MSS.
