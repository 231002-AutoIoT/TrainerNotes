# Projects

## Project 1
Length: 1 week

Present for End of Day on Friday.

### Overview

Research and design a simple automotive system, modeling the behavior and environment of an Electronic Control Unit (ECU). System design includes a sensor suite, circuit block diagramming, ECU logic, and expected output values and possible Diagnostic Trouble Codes (DTCs). Specific sensor research and selection includes any relevent conversion factors, and circuit diagramming includes the use of appropriate power ground circuits and ECU blocking. ECU logic design includes pseudo-coding the conversion of signal values to meaningful values,  determining nominal ranges and failure conditions, and describing the failure behaviors.

### Requirements

1. Pick a system within your vehicle
   - determine appropriate sensors for that system
   - determine appropriate end results/functions to control for that system
   - determine how an ECU might/does control those functions
2. Determine the metrics input to the ECU from the sensor
3. Determine how you would convert the information provided by the sensor into real information
   - Reference the source for your data & calculations
4. Construct a circuit diagram that considers a variety of factors
   - What conditions are being monitored by the sensors?
   - What signal does the sensor produce for those conditions?
   - What does the ECU do for each of those signals?
   - What happens as a result of the ECU within the car?
5. Present how it works
   - Include your circuit diagram
   - Describe your sensor(s) and their function
   - Describe the mathematical model (algorithm) for your sensor and it's signal
   - Present any research/resources used to develop your circuit

### Technologies

- Automotive Systems
- Circuit Diagram
- ECU Logic
- Input Sensors

## Project 2: 
Length: 1 week

Present for End of Day on Friday.

### Overview

A Python application to simulate the logic and behavior of an Electronic Control Unit (ECU) as part of a CAN bus network. The application must accept incoming data-frames, determine the appropriate action for each frame, and output the result in the correct format to the appropriate location. Each frame is analyzed to isolate the sending system, the values included in the frame, and the included error code. Based on the sending system and the error code, application logic determines an appropriate action. In the event of an error code the application determines the severity and responds by monitoring the following frames for a recurring error, or triggering a Diagnostic Trouble Code (DTC) and logging the frame in a log file. If no error is detected the application converts the data portion of the frame to a meaningful value and attaches a unit of measure based on the sending system and transmits the converted value. All signal transmission is simulated using file interaction.

### Requirements

Using Python:
  - Read the input data frames from a target file
  - Analyze each frame in sequence, using an appropriate conversion factor for the sensor to convert
    the frames to a meaningful value
  - Write the frame number, the name of the sensor, their converted data value and unit,
    and if an error was detected to the output file.
  - Log the number of input data frames analyzed, the number of errors detected in the input data frames,
    and what DTC are generated as a result of those errors to a third file.

#### Input Data Frame Format
Input frames will contain:
- 1 two-digit hexadecimal value noting the sensor producing the data
- 3 two-digit hexadecimal values with the data produced by the sensor
- 1 two-digit hexadecimal value noting if an error was detec

#### Input data frames fill match the following format:
| sensor | data A | data B | data C | error
|-|-|-|-|-
| 0x   |   0x   |   0x   |   0x   |   0x


#### Sample input data frame
0d 00 00 32 00
0a 0e 00 00 0f
01 2c 73 39 ff


#### Errors
The following error codes may be included with an input data frame. Each code should be handled according to the 
conditions listed in this section.

00 - no error
0f - single event
ff - major malfunction

- If no error is detected the data should be converted as normal and no additional action should be taken.
- If a major malfunction is detected the data should be excluded and a DTC should be noted in the log file
- If a sensor produces a single event error the data should be included if it is within the value range,and a count of the errors started. If three or more input data frames in sequence that carry a single event error, a DTC should be noted in the log file.


#### Sensors
The following sensors may be included in the input data frames. Your Python code should be able to convert any of the input data frames to a meaningful value using the conversion for that sensor,and include an appropriate unit in the output file.

|sensor code | sensor name                | value conversion | value unit | value range|
|-|-|-|-|-|
|0a          | fuel pressure              | (3A)             | kPa        | 0 - 765
0c          | engine speed               | ((256A + B)/4)   | rpm        | 0 - 16,383.75
0d          | vehicle speed              | (C)              | km/h       | 0 - 255
11          | throttle position          | ((100/255)A)     | %          | 0 - 100
2f          | fuel tank level            | ((100/255)A)     | %          | 0 - 100
5c          | oil temperature            | (A-40)           | C          | -40 - 215
67          | engine coolant temperature | (B-40)           | C          | -40 - 215
68          | air intake temperature     | (C-40)           | C          | -40 - 215


#### Output Data Format
----------------------------
The output data file should include all of the important information from the input data frames, in a 
human-readable format. Each input data frame should be represented by a line in the output data.
Each line of output data should include:
- The number of the frame
- A time stamp
- The sensor name
- The converted data
- The unit for the converted data
- The DTC if one is required for the frame


#### Output Data Example

input data frames:
0d 00 00 32 00
68 00 00 f0 0f
0c ff 00 88 ff

output data file:
1 - 14:35:45 - vehicle speed - 50 km/h
2 - 14:35:46 - air intake temperature - 200 C
3 - 14:35:47 - engine speed - DTC - P0725

### Technologies

- Python
- ECU Logic
- CAN
- Bus Design

## Project 3:
Length: 2 weeks

Due to length and primary material for the project is from Wednesday of week 3 to Wednesday of week 4, this project will span two weeks. However, we will have a check-in & confirmation of the material the associate is working on the friday prior, requirements marked with (C). Main presentation will include the prior, along with the remaining requirements by end of day Thursday week 4.

### Overview

[SME Reference Document for design behind project](https://core.ac.uk/download/pdf/79618454.pdf)

The project centers on utilizing Model-Based Design systems from the project's inception to System-in-the-Loop (SIL) testing. The primary goal is to approve at least 5 Electronic Control Units (ECUs) for integration into an automotive system. This involves crafting a Concept of Operations outlining the system's proposed concept and operational aspects. Subsequently, a detailed document encompassing Requirements & Architecture, including a Block Diagram, will be developed to communicate high-level system expectations. Further, Detailed Design Diagrams, featuring Circuit Diagrams, will be created to offer a comprehensive low-level overview of the system's architecture. The final phase entails Module Design and Simulation using Simulink, where each component's physical or functional behavior is modeled and verified through simulation using test data. This process ensures that all components operate as expected within the designed system of choice. 

### Requirements

The project focuses on leveraging the initial stages of our Model-Based Design systems all the way through SIL testing. Select at least 5 ECUs, working together in an automotive system that you must approve through your trainer. You will present a rough draft of the topics 1-3 for approval and insurance you're on the right track with your project. Final presentations will occur Thursday afternoon, presenting in a professional format (i.e. PPT) and showcasing the simulation of this system as it was designed through Simulink. See each topic below for details of expectations for each section. 

All material must be submitted to SharePoint, see submission instructions below!

1. (C) Concept of Operations (CONOPS)
   - A document that describes a proposed system concept and how that concept would be operated in an intended environment.  The user community develops the CONOPS to communicate the vision for the operational system to the acquisition and developer community. A CONOPS can also be written by the buyer, developer, or acquirer to communicate their understanding of the user’s needs and how a system will fulfill them.

2. (C) Requirements & Architecture (includes Block Diagram)
    - Document will typically describe the system's functional, interface, performance, data, security, etc. requirements as expected by the user. It is used by business analysts to communicate their understanding of the system to the users. Very high-level overview

3. (C) Detailed Design Diagrams (includes Circuit Diagram)
    - Baseline in selecting the architecture is that it should realize all which typically consists of the list of modules, brief functionality of each module, their interface relationships, dependencies, database tables, architecture diagrams, technology details etc. Low-level overview.

4. Module Design and Simulation (Simulink)
    - You model each component within the system structure to represent the physical or functional behavior of that component. You verify the basic component behavior by simulating them using test data.
    - Model the system in simulink based on all the prior material to begin simulating the system to test components are working as expected.

#### Submission of Material

Please upload all materials for this project into this [capstone-project](https://revaturetech.sharepoint.com/:f:/s/231002-OnlineVA-AutomotiveiOTTesting/Ek2mNSSpAfVNlyeJbNs3n60BtxqdXjS7M0ZdwGW0JEM7jw?e=jmQLdq) folder on the sharepoint, under your own personal folder as follows:
    1. Name personal folder firstname-lastname
    2. Within personal folder, include the following folders:
       1. `conops` - contains material for Concept of Operations
       2. `ddd` - contains material for Detailed Design Diagrams
       3. `md&s` - contains material for Module Design & Simulation
       4. `r&a` - contains material for Research & Architecture
    3. Within your personal folder, please include a copy of the slide deck as presented on Thursday

### Technologies

- Automotive Systems
- ECU Logic
- Circuit Diagram
- Block Diagram
- MATLAB/Simulink
- Model-Based Design

