




# Title of Project - "CORE-V Vision APU"
# Project Concept Proposal

## Date of proposal - 2023-03-25

## Authors
- Michael Aronson,  Rumble Development Corp.  
- Alfred Shiu,  Empaiot PTE LTD

## High Level Summary of project, project components, and deliverables

- The goal of this project is to design and build a low-power, yet powerful, event-driven vision processor for the edge.  Typical applications will target a 12 month battery life.

- The project builds on CORE-V-MCU, but replaces CV32E40P with CVP32E40Pv2, adds a neural network accelerator and high power domain with CVA6 and ARA for advanced AI and image processing.  Like the CORE-V-MCU, this project is primarily open-source but uses selected proprietary components.  An OpenHW development board will accompany this chip project.

- The device will be fabricated using Global Foundries 22FDX,  with a target size of 4mm x 4mm., using low power memory, and ABB for minimal leakage.

- Three power domains
	- Always-on domain
		- oscillator, timer, and power management
		- can wake up low power domain on timer
	- Low power domain
		- CV32E40Pv2 + peripherals (similar to CORE-V MCU)
		- ISP and compression (proprietary), powerful enough to handle 4K video at 30 fps capture and display
		- Binary Neural Network accelarator (proprietary,  but may be possible to open source at later stage) .  This will analyze incoming signals, and decide when to wake up the high power domain.  The fast BNN model can provide close to real time event detection at low power and pre-process such signal for fast execution by the high power domain to help keep the overall power budget low.
	
	-  High Power domain
		- CVA6 + 8-lane ARA
		- Run more sophisticated AI and OpenCV,  using RVV compliant vector processor

- Cloud FPGA implementation
	- Implement on AWS F1 instance
	- Simulate I/O through combination of RTL on FPGA and software layer on host
	- This approach allows us to utilize high density FPGAs,  and share development among teams that are geographically distant 

- Development board
	- Designed as an open source board and sold through OpenHW like the CORE-V-MCU-Devkit



## Summary of market or input requirements
### Known market/project requirements at PC gate

- This design is optimized for battery powered, always on applications.  A representative example would be a door camera.  The Always-on domain could wake up the low power domain every few seconds.  A low resolution image could then be captured,  and checked with a neural network for person detection.  If a person is detected,  the high power domain could be awakened,  and facial recognition could be performed,  and video captured.

- Video processing targets 4K 30fps performance

### Potential future enhancements

## Who would make use of OpenHW output

- As the project output will be a set of technical artifacts embodying the MCU design, OpenHW members or others can use the CORE-V-Vision APU as the basis of an industrial design targeting Vision processing AI applications with CORE-V processors. Note however that some components will not be open-sourced. The FPGA and development boards will support AI-application prototyping, development, and performance evaluation

- This project will serve as a silicon demonstration of both the CVA6-ARA combination,  and the CV32E40Pv2 core


## Initial Estimate of Timeline
- Tapeout:  Q4

## Explanation of why OpenHW should do this project

- As OpenHW is the main industry open-source organization devoted to embedded and application class RISC-V processors and accelerators, industry-qualify verification, development of open-source MCU prototype chips using GF22FDX, and required software support, OpenHW is the suitable organization to drive this project. 

- The OpenHW ecosystem will benefit from expanding the architectural space of OpenHW MCU designs and the VISION-APU will pave the way for prospective users of AI-focussed architectures using hybrid arrangements of CORE-V cores.

- This project will provide resources for additiional verification of the CVA6-ARA core.

- The cloud FPGA methodology we are developing will be useful for future projects within the community

## Industry landscape: description of competing, alternative, or related efforts in the industry

## OpenHW Members/Participants committed to participate
- Empaiot Pte Ltd.
- Rumble Development Corp.
- We are finalizing arrangements with ETH Zurich and Polytechnique Montreal for student participation


## Project Leader(s)
### Technical Project Leader(s)
- Michael Aronson,  Rumble Development
- Timmy Lai,  Empaiot
### Project Manager, if a PM is designated


## Next steps/Investigation towards Project Launch
- Finalize specifications
- Develop verification plan
- Finalize IP vendors
- Choose back-end service provider

### Target Date for PL
- April TWG meeting
