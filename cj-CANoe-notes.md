# CAN 500kBaud 1ch

CAN IG - Interactive Generatore 
- Add CAN Frame
  - Every 1000ms send CAN Data DLC 8
  - Send 0xE, 0x2, 0x3
  - ID = 200
  - Start

Check your Trace to see the output from the CAN IG above
Limit functionality that we can only Access 4
- CANoe vs BusMaster 
    - Less manaul creation required
    - Built in functionalities common to the industry
    - quickly simulate real-world examples to get started
    - Industry Standard

[Real World Sample Databases for CANoe - dbc files](https://github.com/commaai/opendbc)

Insert 3 networks. No need to work on the DB from scratch
- Config each, first 1 
  - Include Sample_Database::ABS
  - Execution: Standard
  - Compile
- Repeat 2 more times for PCM & BCM
  
Add Signal Generators to help manipulate data
- Vehicle Speed: Sine wave 0-255

Data
- Add Signals, focus the one you're more interested with

Graphics will show the data as it changes over time

Break into learning how to create our own dbc

# ACC Example
Cruise_Switch_Request for Signal
- Length Bit: 3
- Value Type: Unsigned
Brake_Switch_1 for Signal
- Length: 1
- Value Type: Unsigned
ACC_Driver_Information_Message
- Length: 8
- Value Type: Unsigned
- Ask What is being sent to the Instrument Cluster by the ACC Module?
Brake_Switch_2
- Length: 1
- Value Type: Unsigned
ACC_State
- Length: 3 
- Value Type: Unsigned
Target_Speed
- Length: 8
- Value Type: Unsigned 
Vehicle Speed
- Length: 8
- Value Type: Unsigned
Brake_Decel_Request
- Length: 8
- Value Type: Unasigned

Messages
ACC_ECU_INFO
0x100
BCM_ECU_INFO
0x200
ECM_ECU_INFO
0x300
ICM_ECU_INFO
0x400