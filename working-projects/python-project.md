## Project 2 - Python mini-project: 
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
