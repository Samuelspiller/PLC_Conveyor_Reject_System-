# PLC_Conveyor_Reject_System-
A Logo!Soft Comfort FBD of a reject system for a conveyor

## Table of Contents
  1) Project Introduction
  2) Project Overview and Features
  3) Tech Stack, APIs and Other Resources
  4) Setup and Running Instructions
  5) Contribute and Report Issues
  6) Conclusion and License

## Project Introduction
A Function Block Diagram for a Reject system on the end of a production conveyor. Safety and Production systems are handled by seperate PLCs, and feed outputs into this system.

## Project Overview and Features

![Quick Pick of System](https://github.com/user-attachments/assets/96e093b5-4c92-479e-bea2-53617d5b29b7)

The PLC is to be programed in Logo!Soft Comfort. 
The system was originally designed to have the products manually inspected, but is being moved to run as part of an automated line. The reject system now needs to be more robust, insuring that no bad products can go through the outfeed of the machine.

The safety system is handled by a Pils system, which does provide a good signal to the reject system to allow it to run.
The production is, again, handled by a seperate PLC, and only currently provides a "Product Good" signal to the Reject PLC. There is scope to add other inputs from the Production PLC in future. 
The stop output feeds back to the Production PLC to stop the system

