# Vehicle Architecture
- Vehicle sketch - label generic parts
- Basic vehicle components - engine, ignition, spark plugs, distributor, battery, alternator, radiator, starter, breaks, shocks, etc
- You can't update the car while you're driving it.
- Introduce Autosar and ADAS for self study
- history of cars
- mechanical vs. electronic - Carb vs Feul Injection
- basic engine function - 4-stroke vs 2-stroke functionality
- basic powertrain functionality
- manual vs automatic transmission
- battery - provide subsystem power/constant power supply
- Alternator - takes rotational energy from the running engine, and generates electrical enegry to supply the battery
- Radiator - circulate coolant through a set of fins to cool the engine
- Suspension
- Axels
- Brakes - disc and drum vs regenerative
- Catalytic Converter
- Muffler
- Tailpipe
- Fuel Tank - what ways can you think of to read the fuel level?
- AC Compressor

- Car anatormy: the basics - https://www.youtube.com/watch?v=fPjOWekzeGI
- Vehicle sketch - detailed component labels

- Shocks
- Steering System

- Driver Alertness Monitor discussion
- Tire Pressure Monitor discussion
- Remote Keyless Entry discussion

- sensor lookup
    - Crankshaft position sensor - p0335
    - Camshaft position sensor - p0340
    - Throttle position sensor TPS - p0120-4, 2138, 2135




# Power / Ground
- sketch a home circuit
- discuss/define power and ground
- list continuous power acessories(kl-30)
- list ignition power accessories (kl-15)
- list accessory power accessories (KLR)
- define/discuss kl-15
- define/discuss kl-30
- individually list 20 kl-15 and 5 kl-30 systems
- Simple battery circuit (ohms law, 12v one lightbulb, add a lightbulb and make both 6v)
- Simple chassis ground circuit
- battery negative terminal (chassis ground) - kl-31
- battery positive terminal - kl-30
- delay relay - on until x time after ignition turn off - kl-30g
- constant power fault - on until fault is detected - kl-30g_f
- ignition switch - kl-15 (push button ignition, or key to "ON")
- sketch circuit with kl-15, kl-30, kl-31, kl-30g, kl-30g_f
- introduce common circuit diagram component symbols
- review horn circuit (blocks)
- sketch horn circuit (diagram)
- sketch camera circuit (diagram)
- review relay contacts
- sketch relay with sensor circuit
- lm35 temperature sensor (signal value conversion)
- sketch fan relay circuit with lm35 sensor
- sketch fan relay wircuit with kl-15/kl-30

- https://vladgur.com/workshop-manual/bmw-x7-50i-g07_2019_edition-12.2019_ewd_ag/?page=97
- examine and describe a wiring diagram

- Wiring/circuit wrapup discussion

# Electronic Contol Unit
- mini-project - develop a custom ECU - components, signals, kl-15/kl-30

- ecu discussion
- sketch ecu circuit diagram (block diagramming)


# Diagnostics and troubleshooting
- find and sketch MIL

## ECU design example
- introduce Wokwi and arduino
- signal I/O, 1/0 (5v/0v)
- digital v analog signals
- virtual breadboarding with temperature sensor
- arduino uno, ds-18b20 tmp sensor, led (w resistor)
- PIR - passive infrared sensor

- https://arduinogetstarted.com/tutorials/arduino-button-led

- H-bridge motor controller
- PWM - pulse width modulation - simulate an analogue voltage signal by controlling the average of a series of digital pulses.


## Autosar
- https://github.com/openAUTOSAR/classic-platform/tree/master

- Automotive Open System Architecture
- Common "Library"/standard libraries
- Standardized interfaces
- hardware to application integration (puzzle peices analogy)

- v-Model
    - Refinement
        - Requirements
        - System spec
        - Functional spec (MIL)
        - Architecture design
        - Module design
        - Implementation

    - Validation and Verification
        - Implementation
        - Module test (SIL)
        - Integration test (HIL)
        - Functional Test (HIL)
        - System Test
        - Maintenance

- interface diagramming
    - IO count, interface blocks
- DIO digital input output interface
- https://www.autosar.org/fileadmin/standards/R19-11/CP/AUTOSAR_SWS_DIODriver.pdf

- AUTOSAR components - https://www.autosartoday.com/article/what_are_dem_dlt_dcm_and_det/
    - DEM - processes the diagnotic codes - diagnostic event manager
    - DET - Development Error Tracer
    - DCM - Diagnostic Communication Manager
    - OBD - On Board Diagnostic
    - DLC - Diagnostic Link Connector
    - DTC - Diagnostic Trouble Code


# ECU Wokwi practice
- UseCase:
If Temperature >= 50C -> Fan ON
Else -> Fan OFF


# Crankshaft Sensor Writeup
- research crankshaft, position sensor, and signals/failures
- throttle position sensor, signals/failures
- TPMS research, ECU circuit block diagram, pseudocode logic, error codes
- OBD

- https://www.youtube.com/watch?v=U2fygPCavq0

- sensor -> ECU -> ERROR CODE -> DEM
- OBD service and PID

- https://en.wikipedia.org/wiki/OBD-II_PIDs

- DTCs

- https://www.dmv.de.gov/VehicleServices/inspections/pdfs/dtc_list.pdf

- UDS - Unified Diagnostic Services - ECU communication protocol (specified by ISO 14229-1). Diagnostic tools are able to contact all ECUs installed in a vehicle that have UDS enabled.

- https://www.youtube.com/shorts/JcMHMeYCGKc

- https://www.csselectronics.com/pages/uds-protocol-tutorial-unified-diagnostic-services



# Python
- data types
- string manipulation
- operators
- control flow
- .methods
- collections
- classes
- magic/double-underscore/dunder methods
- functions
- file IO


# CAN
- sketch abs, Dash-board, and BCM ecus and sensors
- two wires
- easy to connect
- broadcast protocol (all can see, only one needs to recieve and confirm)
- fake messaging with chat (AJ, the tire pressure is 50 PSI. / recieved)
- messaging priority (kyle, this is low priority, your door is closed. Larry, this is important, you just hit something!)
- CANH and CANL wires (high and low state)
    - EMF/fault voltage (signal interference)
    - engine start, alternator, spark-plug wires
    - differential voltage
    - CANH runs 2.5-5, CANL runs 0-2.5
    _|----|___|---|____ CANH
    -|____|---|___|---- CANL
- messaging styles
    - main/nodes (master/slave)
    - direct (phonecall/bluetooth)
    - broadcast (megaphone on the street)
- synchronous vs asynchronous
    - can is asynchronous, but have a consistent baudrate (speed of transmission)
- bus length inverse-relationship to baudrate (the longer the wire, the slower it goes)


## CAN Bus
- Busmaster - https://rbei-etas.github.io/busmaster/
- MinGW - linked from busmaster
- based on simple block diagram, build DB file
    - ABS, Dash, BCM newtowk DB
    - ABS - 4 wheel speed sensors
    - BCM - 4 Door sensors, 1 Seatbelt sensor
    - Dash - Buzzer output, lamp output
- signal generator

## CANoe
- dbc file
    - signals
    - messages
- nodes
    - ECU
    - Interactive Generators (IG)
- demo file walk-through

## Simulink
- MATLAB online - https://www.mathworks.com/
    - free acct = 20 hrs per week
    - 30 day trial acct = unlimited

- blocks
    - constant
    - display
    - operations (add, subtract)
    - logical gates (AND, OR)
    - control flow (if/if action)

- Magesh Jayakumar Simulink/Arduino video series - https://www.youtube.com/watch?v=bB5-mvA41cI&list=PLnFVwvy9GeM4Z994R8sbDLFE9yj8Ad9KN

- Flow Control Exercise - FlowControl.md
    - flow chart - paper and pencil
- Chart blocking
    - state, transition
    -
        ```
        {NAME}
        entry:
        {in/out actions}
        ```
    -
        ```
        state1
        entry:
        out1 = in1;
        ```

    - transition = conditions
        [condition1 == 1]
    - transition = delay/actions
        after(10, sec)



- CAN Pack/UnPack blocks
- CAN Transmit/Recieve blocks
