
# Build Journal

## The Nonchalant

This is where I have added the work I did while making The Nonchalant

I made this car using ESP32 and wanted to control it just by moving my hand

I worked on the car design wiring and code and kept everything in the same project

## 1 Starting the Project

I wanted to make a car that works using hand movements instead of a normal remote

For this I used two ESP32 boards

One ESP32 reads the hand movements using an MPU9250 sensor and the other ESP32 controls the car

I used ESP NOW to send commands between them

For the motors I used an L298N motor driver and four BO motors

I also added an HC SR04 sensor at the front to detect obstacles

### Circuit Diagram

![Circuit Diagram](assets/circuit-diagram.png)

## 2 Wiring

I connected the MPU9250 to the controller ESP32 using GPIO 15 and GPIO 14

For the car I connected the L298N motor driver to GPIO 26 25 17 and 16

GPIO 32 and 33 are used to control the motor speed

The ultrasonic sensor uses GPIO 18 and 19

I also used a resistor divider for the Echo pin because the sensor gives 5V and the ESP32 works with 3.3V signals

## 3 Designing the Car

I used Fusion 360 to make the chassis

I wanted to design the body myself instead of using a ready made car chassis

I started with the base and then made space for the motors battery and other parts

I also designed the motor mounts and a place for the ultrasonic sensor at the front

### Base Design

![Chassis Sketch](assets/cad-sketch-base.png)

### Motor Mount

![Motor Mount](assets/cad-side-bracket.png)

### Front Sensor Mount

![Sensor Mount](assets/cad-bumper-mount.png)

After making the basic design I added some support around the chassis and motor mounts to make them stronger

I checked the full model in Fusion 360 to see how everything would fit

### Full Car Design

![Full CAD Assembly](assets/cad-full-assembly.png)

### Chassis Support

![Reinforced Chassis](assets/cad-reinforcement.png)

I saved the design in Fusion 360 and STEP formats so I could use it again or make changes later

## 4 Building the Car

After finishing the design I printed the chassis parts

Then I attached the four BO motors and wheels

I placed the ESP32 and L298N motor driver inside the car

The ultrasonic sensor was placed at the front

I connected the wires and checked that the wheels had enough space to move

### Electronics Inside the Car

![Car Electronics](assets/PHOTO-2026-10-23-02-08-37.jpg)

## 5 Hand Controller Code

For the hand controller I used the MPU9250 sensor

The sensor reads how much I tilt my hand

The ESP32 uses these readings to decide which command to send

I kept the tilt limit at 15 degrees

If I tilt my hand more than that the controller sends a movement command

If my hand is straight it sends a stop command

The commands are sent every 100 milliseconds using ESP NOW

I used GPIO 15 for SDA and GPIO 14 for SCL

I also had to add the MAC address of the car ESP32 in the controller code

The MAC address already written in the code is just an example and needs to be changed

### ESP NOW Code

![ESP NOW Setup](assets/code-espnow-setup.png)

### Gesture Calculation

![Gesture Calculation](assets/code-gesture-math.png)

## 6 Car Receiver Code

The ESP32 on the car receives the commands from the hand controller

It then controls the motors using the L298N motor driver

I used GPIO 32 and 33 for motor speed control

The speed value is set to 180 out of 255

For turning the car runs the motors on one side and stops the other side

When I tilt my hand backward the car switches to reverse mode

Tilting backward again switches it back

## 7 Obstacle Detection

I used the HC SR04 sensor to detect objects in front of the car

I set the distance limit to 20 cm

If something comes too close the car stops for a moment then turns right and stops again

The code also checks the distance before moving forward

This helps the car avoid hitting objects in front of it

## 8 Testing

After connecting everything I tested the car using the hand controller

I checked the forward backward left and right movements

I also checked how the car turns and how the ultrasonic sensor responds when something is in front of it

### Turning Test

![Car Turning](assets/car-turning-test.jpg)

I kept the wheels off the ground while checking the motor directions

I also checked the MAC address to make sure both ESP32 boards could communicate

## 9 Demo

I added a short video showing the car moving using hand gestures

[Watch the Driving Video](assets/VIDEO-2026-10-23-02-05-10.mp4)

## 10 Final Notes

This project helped me learn more about ESP32 wireless communication sensors motor control and 3D design

I got to work on both the hardware and coding parts

The main thing I wanted was to make a car that could move based on my hand movements

I still have a few things I can improve later but I enjoyed making this project
