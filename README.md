# Aim of the project
LibreVerter - An open inverter, built for a lifetime. 
A home inverter, to interface battery systems and PV systems with the UK and EU electricity grids.

The LibreVerter must be:
- Durable
- Repairable
- Open-Source

The main goal of the project is to develop an open source inverter (Hardware and Software).  
The initial configuration of the project will be a single phase, 2 kW inverter. 

An important part of the project is to be able to work with different types of switching components (IGBT/MOSFET). Nowadays, we often see that inverters are replaced after 10 years but they keep working or some faulty inverters that are not easily repared because the design is not modular or easy to fix.

Then, the goal is to design an Open Source inverter that is modular to be easy to be fixed and flexible enough to have differents functionalities (batteries/PV/...)

The project will be divided into different "workpackages" based on the functional blocks needed to make the whole system work. These functional blocks are called "Modules", and may be split into further modules where necessary. The diagram below shows the module definitions we are currently working to. 

<img width="1330" height="720" alt="WattWell Block Diagram-External Interfaces - Operational drawio (3)" src="https://github.com/user-attachments/assets/8eaf413c-4e8b-467d-855a-313eac3cd6d3" />

1. Supervisory control: development of the main control board able to get the measurements, generate references, ... This board embeds the main mcu.
2. Inverter Board
3. DC/DC converter: Able to take a variable DC input (48V +/- 20%) and output a stable DC output controllable between 360 V and 500 V.
4. DC Link: A DC link capable of self-protection
5. A DC filter for smooth input/output
6. DC Protections for over-current and over-voltage protection
7. DC connections for physically connecting the DC source to WattWell
8.  AC filter for smooth sine wave input/output
9. AC protection for over-current and over-voltage protection. Required for compatibility with grid codes.
10. Connections for phsyically conecting the external electrical system to WattWell
11. Human Machine Interface (HMI) to act as the interface between the user and the supervisory control

For the Inverter board, two sub-modules are assumed:
1. Control and Driver board: interface between the supervisory control board and power switch (IGBT's/Mosfet's). The driver board needs to generate the PWM signals based on a reference from the supervisor.
2. Power circuit: power circuit of the inverter

# Who are we making this for?
Our ideal customer profile is:
A “solar as a service” provider. Responsible for through life maintenance. Because:
1. They are able to buy WattWells via individual customer orders.
2. Their interests are aligned with selling as many systems as possible, as well as being able to maintain the systems at low cost. Repair and re-use are essential.
3. They are regularly buying inverter systems.
4. They are likely to be a relatively small company, maybe 10-50 people, with big buying power via their customers.

We are also interested in serving other customers who want an inverter for life; we'd love to hear from you if you fit that description! 

# Expected functionalities

- Being able (and allowed) to be connected to the European grid
- MPPT for solar panels (with DC/DC)
- Battery connection
- Communication capabilities (serial,...)
- Working in islanding mode (offgrid)

# 1. Supervisory control board:

For the supervisory control, the firmware on the main mcu should have (main mcu based on STM32G434):

1. Low level drivers
2. Basics functionalities (bootloader, debug uart, pll,...)
3. Advanced functionalities (power management, MPPT, state machine)

The main control board will be able to measure:
1.  3AC voltages (max 400V) - ADC min 14bits
2.  2DC voltages (max 1500V) -ADC min 14bits
3.  4AC/DC current measurement - ADC min 14bits
4.  Temperature measurement

The main control board will have the following interface:
1.  2X UART(1X to RS485; 1X to USB)
2.  1xSPI
3.  2xI2C
4.  1xCAN
5.  6X PWM's
6.  6X DO's
7.  6X DI's
8.  6X AI'S (temp from IGBT/Mos)

Other functions:
1.  Debug LED
2.  RTC (supercap based)
3.  Additionnal ROM (TBD)
4.  Watchdog
5.  Power supply for IGBT's/Mosfets
   
