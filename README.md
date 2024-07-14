![image](https://github.com/user-attachments/assets/9dece88d-7722-427b-b1b8-ec403f4cdf3a)# Obstacle Detection and Navigation Robot


## Project Overview

This project involves the design and development of an obstacle detection and navigation robot. The robot is equipped with infrared (IR) sensors to detect obstacles and navigate through its environment by avoiding them. The project encompasses hardware assembly, sensor integration, and software programming to achieve autonomous navigation.

## Table of Contents

- [Introduction](#introduction)
- [System Requirements and Specifications](notion://www.notion.so/Rough-Work-65d1028c62dc474b89b225765077fc3d?pvs=94#system-requirements-and-specifications)
- [Methodology](notion://www.notion.so/Rough-Work-65d1028c62dc474b89b225765077fc3d?pvs=94#methodology)
- [Implementation](notion://www.notion.so/Rough-Work-65d1028c62dc474b89b225765077fc3d?pvs=94#implementation)
    - [Hardware Assembly](notion://www.notion.so/Rough-Work-65d1028c62dc474b89b225765077fc3d?pvs=94#hardware-assembly)
    - [Component Connections](notion://www.notion.so/Rough-Work-65d1028c62dc474b89b225765077fc3d?pvs=94#component-connections)
    - [Logical Programming](notion://www.notion.so/Rough-Work-65d1028c62dc474b89b225765077fc3d?pvs=94#logical-programming)
- [Testing and Debugging](notion://www.notion.so/Rough-Work-65d1028c62dc474b89b225765077fc3d?pvs=94#testing-and-debugging)
- [Results](notion://www.notion.so/Rough-Work-65d1028c62dc474b89b225765077fc3d?pvs=94#results)
- [Applications and Future Scope](notion://www.notion.so/Rough-Work-65d1028c62dc474b89b225765077fc3d?pvs=94#applications-and-future-scope)

## Introduction

The Obstacle Detection and Navigation Robot is designed to autonomously navigate its environment while avoiding obstacles. The robot uses IR sensors to detect obstacles and adjusts its path accordingly.

## System Requirements and Specifications

The robot system includes:

- Arduino Uno R3 microcontroller
- L298 motor driver module
- N20 motors with rubber wheels
- Infrared (IR) sensors
- 12V power supply
- Robot chassis

## Methodology

The methodology includes the following steps:

1. Assembling the robot hardware
2. Connecting components to the microcontroller and power supply
3. Programming the Arduino to process sensor data and control the motors
4. Calibrating the IR sensors for reliable obstacle detection
5. Testing and debugging the system for optimal performance

## Implementation

### Hardware Assembly

The assembly involves mounting the sensors, motors, and microcontroller onto the robot chassis. Key components are strategically placed to ensure balance and functionality.

### Component Connections
|        |               
|--------|
| All components are interconnected using male-female jumper wires. The motor driver is connected to the power supply and the Arduino, which processes sensor data and controls the motors. | 
| <img align="centre" alt="coding" width="500" hight="500" src="https://github.com/user-attachments/assets/4b3ae8a9-5125-4cee-86b3-31959b03460a"> |

### Logical Programming

The Arduino is programmed using the Arduino IDE. The code involves:

- Reading sensor data
- Calculating errors based on sensor readings
- Adjusting motor speeds and directions to avoid obstacles
|  **Flow-chart**      |  **Code** |             
|--------|--------|
| <img align="centre" alt="coding" width="500" hight="500" src="https://github.com/user-attachments/assets/2f229a44-5d1b-4269-880a-75688ad1b721"> | 
```c                                                                                                                                                                        
#define m1 4  //Right Motor MA1                                                                                                                                                                                                                       \
#define m2 5  //Right Motor MA2                                                                                                                                                                                                                       \
#define m3 2  //Left Motor MB1                                                                                                                                                                                                                        \
#define m4 3  //Left Motor MB2                                                                                                                                                                                                                        \
#define e1 9  //Right Motor Enable Pin EA                                                                                                                                                                                                             \
#define e2 10 //Left Motor Enable Pin EB                                                                                                                                                                                                              \
#define near A5                                                                                                                                                                                                                                       \
                                                                                                                                                                                                                                                      \
void setup() {                                                                                                                                                                                                                                        \
  pinMode(m1, OUTPUT);                                                                                                                                                                                                                                \
  pinMode(m2, OUTPUT);                                                                                                                                                                                                                                \
  pinMode(m3, OUTPUT);                                                                                                                                                                                                                                \
  pinMode(m4, OUTPUT);                                                                                                                                                                                                                                \
  pinMode(e1, OUTPUT);                                                                                                                                                                                                                                \
  pinMode(e2, OUTPUT);                                                                                                                                                                                                                                \
  pinMode(near, INPUT);                                                                                                                                                                                                                               \
}                                                                                                                                                                                                                                                     \
                                                                                                                                                                                                                                                      \
void loop() {                                                                                                                                                                                                                                         \
  int s6 = analogRead(near);//distance sensor value                                                                                                                                                                                                   \
  if(s6 > 500) { //robot move forward direction                                                                                                                                                                                                       \
    analogWrite(e1, 255);                                                                                                                                                                                                                             \
    analogWrite(e2, 255);                                                                                                                                                                                                                             \
    digitalWrite(m1, HIGH);                                                                                                                                                                                                                           \
    digitalWrite(m2, LOW);                                                                                                                                                                                                                            \
    digitalWrite(m3, HIGH);                                                                                                                                                                                                                           \
    digitalWrite(m4, LOW);                                                                                                                                                                                                                            \
  } else { //robot change the path by taking turn                                                                                                                                                                                                     \
    analogWrite(e1, 255);                                                                                                                                                                                                                             \
    analogWrite(e2, 255);                                                                                                                                                                                                                             \
    digitalWrite(m1, HIGH);                                                                                                                                                                                                                           \
    digitalWrite(m2, LOW);                                                                                                                                                                                                                            \
    digitalWrite(m3, LOW);                                                                                                                                                                                                                            \
    digitalWrite(m4, HIGH);                                                                                                                                                                                                                           \
    delay(500);                                                                                                                                                                                                                                       \
    //robot move again on changed path                                                                                                                                                                                                                \
    analogWrite(e1, 255);                                                                                                                                                                                                                             \
    analogWrite(e2, 255);                                                                                                                                                                                                                             \
    digitalWrite(m1, HIGH);                                                                                                                                                                                                                           \
    digitalWrite(m2, LOW);                                                                                                                                                                                                                            \
    digitalWrite(m3, HIGH);                                                                                                                                                                                                                           \
    digitalWrite(m4, LOW);                                                                                                                                                                                                                            \
    delay(500);                                                                                                                                                                                                                                       \
  }                                                                                                                                                                                                                                                   \
}                                                                                                                                                                                                                                                     \
```  |



## Testing and Debugging

The robot is tested in different environments to ensure reliable obstacle detection. Various materials (wood, metal, glass, etc.) are used to test the response time and detection range of the IR sensors.

## Testing & Observation

| Testing with White Surface Object  | Testing with Black Surface Object |Testing with Glass Object |     
|--------|---------------|---------------|
| <img align="right" alt="coding" width="300" hight="400" src="https://github.com/tejascw/Intelligent_Obstacle_Navigator_IR_Sensor_Based_Robot/blob/main/ASSET/WHITE_SURFACE_OBJECT2-ezgif.com-video-to-gif-converter.gif"> | <img align="right" alt="coding" width="300" hight="400" src="https://github.com/tejascw/Intelligent_Obstacle_Navigator_IR_Sensor_Based_Robot/blob/main/ASSET/BLACK_OBJECT1-ezgif.com-video-to-gif-converter.gif"> | <img align="right" alt="coding" width="300" hight="400" src="https://github.com/tejascw/Intelligent_Obstacle_Navigator_IR_Sensor_Based_Robot/blob/main/ASSET/GLASS_OBJECT-ezgif.com-video-to-gif-converter.gif">
|**Observtion:**                 |          **Observtion:**       |             **Observtion:**    |
|                 |                 |                 |
|**Testing with Metal Object** |      **Testing with Rubber Object**          |    **Testing with Wood Object**             |   
| <img align="right" alt="coding" width="300" hight="400" src="https://github.com/tejascw/Intelligent_Obstacle_Navigator_IR_Sensor_Based_Robot/blob/main/ASSET/METAL_OBJECT-ezgif.com-video-to-gif-converter.gif"> |<img align="right" alt="coding" width="300" hight="400" src="https://github.com/tejascw/Intelligent_Obstacle_Navigator_IR_Sensor_Based_Robot/blob/main/ASSET/RUBBER_OBJECT-ezgif.com-video-to-gif-converter.gif">| <img align="right" alt="coding" width="300" hight="400" src="https://github.com/tejascw/Intelligent_Obstacle_Navigator_IR_Sensor_Based_Robot/blob/main/ASSET/WOOD_OBJECT-ezgif.com-video-to-gif-converter.gif"> | <img align="right" alt="coding" width="300" hight="400" src="https://github.com/tejascw/Intelligent_Obstacle_Navigator_IR_Sensor_Based_Robot/blob/main/ASSET/WOOD_OBJECT-ezgif.com-video-to-gif-converter.gif"> |
| **Observtion:**                |    **Observtion:**             |      **Observtion:**           |
|                 |                 |                 |

## Results

The robot successfully navigates its environment by detecting and avoiding obstacles. It demonstrates reliable performance in both bright and dark conditions.

## Applications and Future Scope

The Obstacle Detection and Navigation Robot can be used in various applications, including:

- Autonomous vehicles
- Industrial automation
- Smart home systems
