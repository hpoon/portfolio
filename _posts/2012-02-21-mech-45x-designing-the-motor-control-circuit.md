---
layout: post
title: "MECH 45X – Designing the Motor Control Circuit"
categories:
  - Engineering
  - Electronics
  - Robotics
image: assets/images/ubc_mech.png
description: "Electrical design for a robotic grasper motor control circuit with Arduino, motor selection, and H-bridge drivers"
---

This post is recreated from the original at [https://blog.henrypoon.com/blog/2012/02/21/mech-45x-designing-the-motor-control-circuit/](https://blog.henrypoon.com/blog/2012/02/21/mech-45x-designing-the-motor-control-circuit/)

Knowing that two motors will be controlled for the grasper, a control circuit was required to determine how much voltage would be delivered to the motor and when they would be on or off. Each motor would also require position feedback for determining when to stop the motor actuation. The following section describes the process used for designing this microcontroller based circuit. These sections also show a heavy emphasis on the electrical portion of the design and less of the physical portion. The physical portion of the design can be visualized with the CAD design.

## 1.0 Motors

The chosen motors are:

- Finger grasping – Cytron IG32E-264K at a cost of USD $57.03 from RobotShop
- Finger sliding – Cytron MO-SPG-30E-20K at a cost of USD $22.58 from RobotShop

Both motors meet the torque speed requirements for this project.

### 1.1 Finger Grasping Actuation

From the initial budget, the budget set for actuators was set at $325. The torque requirement needed for gripping was also calculated and each finger would require 4 Nm at its output to lift a 4 kg object using only the fingertips. The evaluation criteria states that the device grasp as fast as possible and that the client would have the highest satisfaction if the device cost was less than $700.

Looking on several websites that sold motors, the following DC motor was chosen: Cytron IG32E-264K at a cost of USD $57.03 from RobotShop. The specifications are as follows:

| Spec                        | Value     |
| --------------------------- | --------- |
| DC voltage                  | 12 V      |
| Gear ratio                  | 264:1     |
| Stall torque (w/o gearing)  | 0.0392 Nm |
| No load speed (w/o gearing) | 7300 rpm  |
| Stall current               | 5 A       |

At 12 V with gearing included, the stall torque would be 20.7 Nm (without consideration of mechanical efficiency). A motor with a high stall torque is also beneficial because it lowers the gear ratio required, which leads to the use of less space for gearing. The motor also comes with its gearing, which contributes to its high torque. Given the high stall torque of this motor addition gear reduction is not required. During grasping, the motor will be exerting high torque at low speeds and therefore, the motor will be operating near the stall torque. The torque here is more than sufficient even with mechanical efficiency losses accounted for.

For finger actuation before grasping occurs, there is a low load and therefore the motor will be operating closer to the no load speed. The no load speed with gear reduction is 27.7 rpm (without consideration of mechanical efficiency). Split among three output shafts, the speed would be 9.21 rpm. Even with the load of the fingers accounted for, this is still acceptable based on requirements and evaluation criteria.

While the torque is a lot higher than required, this motor was only more expensive than a motor of one size smaller by less than three dollars. The electrical characteristics were also identical. With a higher motor torque, the grasper would be comfortable in lifting objects even heavier than 4 kg, which is another benefit based on the evaluation criteria.

### 1.2 Finger Sliding Actuation

The motor required here does not require a large torque since motion in this degree of freedom is not expected to handle heavy loads. This motor only requires enough torque to overcome the friction of the finger on the power screw that it is mounted on. Therefore, a low-cost motor (relative to the grasping motor) will suffice. The DC motor of choice is the Cytron MO-SPG-30E-20K at a cost of USD $22.58 from RobotShop.

The specifications are as follows:

| Spec                         | Value    |
| ---------------------------- | -------- |
| DC voltage                   | 12 V     |
| Gear ratio                   | 20:1     |
| Rated torque (after gearing) | 78.4 mNm |
| Rated speed (after gearing)  | 185 rpm  |
| Rated current                | 410 mA   |

An initial estimate of two 200 g fingers sliding on a 1/2" diameter power screw with a steel-steel sliding interface (friction coefficient of 0.8) shows that only 20 mNm of torque is required. Therefore, this motor meets the requirement. The power screw also has 13 threads per inch, and at the rated 185 rpm, the power screw would slide linearly at 6 mm/s.

### 1.3 Motor Type

DC and servo motors are motors that are suitable for the project. An investigation between DC and servo motors showed that many manufacturers of motors did not provide the necessary specifications for choosing a servo motor in terms of the values of the no load, stall torque, and stall current. While servos generate a lot of torque relative to their size when compared to DC motors, it is not feasible to use a servo motor because of the unknowns in the specifications. It is possible to buy several servos and test them, but this is costly and time consuming. At this stage in the project, the team is not able to commit the time to investigate further.

Comparison of the cost of the grasping motor relative to motors from Maxon Motor, a supplier of motors for UBC Thunderbots, shows that the price of a motor of the same power output costs approximately the same amount. However, a fundamental difference is that the motor from Maxon does not include a gearbox, while the chosen motor for this project does.

## 2.0 Microcontroller

The microcontroller of choice is the Arduino Diecimila. The primary motivator for using this board is because the UBC Thunderbots team already has this board and is currently unused. The Thunderbots team has generously provided the board for use on this project.

The MCU will allow the turning the motors on and off, changing motor direction, changing motor speed, and reading encoder feedback.

## 3.0 Voltage Regulation for Encoders

Since the power supply is likely going to be run at 12 V, the encoders will require voltage regulation down to 5 V (the operating voltage of the encoder for the motors). The chosen voltage regulator is the MC78L05A at a cost of USD from Digikey. According to the typical application diagram of the datasheet, two capacitors will also be required (0.33 μF and 0.1 μF). The cost of these are less than $1.

The voltage regulator will be wired up in this way as the datasheet shows:

![]({{ site.baseurl }}/assets/images/image.png)

The input will be from the 12 V source, and the output will be to the encoders.

## 4.0 Motor Driver

To control the motors, an H-Bridge is to be used. However, due to the different current flows for each motor, one motor driver will require a high current capacity while the other one will not. The high current capacity motor driver consists of a driving circuit using two half-bridges. The low current capacity motor driver is made up of 1 IC.

### 4.1 Finger Grasping Motor Driver

To design the H-Bridge for controlling the motor, an L6205 motor driver will be used. Each of them costs USD $11.36 from Digikey and can withstand a continuous current of 2.8 A and a peak current of 5.8 A and can be interfaced with the microcontroller with PWM inputs. The driver can also be run in a parallel mode to double the current ratings by using both of its full bridges together. The datasheet provides an application circuit as follows:

![]({{ site.baseurl }}/assets/images/image1.png)

![]({{ site.baseurl }}/assets/images/image2.png)

Output pins from the Arduino can turn the motor on and off through the enable pins. Direction is controlled by adjusting the voltage polarity between IN1 and IN2.

There are also two output pins for current sensing. By using it to measure the current draw, the microcontroller program can determine what the torque is through the use of the motor curves provided in the motor specifications.

### 4.2 Finger Sliding Motor Driver

The motor driver of choice is the L293D and each one costs $2.50 from Digikey. Bidirectional control of a DC motor can be achieved by adapting the application circuit from the datasheet:

![]({{ site.baseurl }}/assets/images/image3.png)

The 1A and 2A pins determine the direction of the motor or the motor deceleration. A truth table is provided in the datasheet.

## 5.0 Power Supply

To power the grasper, a power supply plugged into the wall will be used. It is expected that the future robot will have a power source of its own which will power the hand as well. Therefore, for the purposes of testing the grasper for this project only a wall power supply will be required.

Looking at the maximum electrical power consumption of the two motors, the total comes to ~65 W (12 V _ 5 A + 12 V _ 0.41 A). The other components also consume power and so the final power consumption will be higher. To compensate, a 12 V power supply with a maximum wattage and current of 84 W and 7 A was selected. The part number is CENB1090 and each costs USD $70.48 from Digikey.

## 6.0 Power Supply Connector

The power supply chosen has one port that uses a Molex Mini-Fit Jr. Receptacle. Therefore, a proper receptacle must be used so that proper wire routing can power all the circuitry. This also means that the future robot will also require a matching plug for this receptacle.

## 7.0 Fuses

Fuses will also be used as a redundant mechanism to stop the motor in case the current draw is too high. The primary method of stopping the motor is through the current sense pins on the motor driver.
