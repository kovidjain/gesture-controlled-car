
# The Nonchalant Build Journal

## Log 1 Planning the Car

Time 1.5 hours

I wanted to make a car that I could control using my hand instead of a normal remote

I decided to use two ESP32 boards and an MPU9250 sensor to read hand movements

For the car I chose four BO motors an L298N motor driver and an ultrasonic sensor

I also wanted to design the body myself instead of using a ready made chassis

![Finished Car](assets/PHOTO-2026-10-23-01-56-13.jpg)

## Log 2 Wiring

Time 2 hours

I worked on the connections for the ESP32 boards and sensors

The MPU9250 uses GPIO 15 and 14 on the controller

For the motor driver I used GPIO 26 25 17 and 16

GPIO 32 and 33 control the motor speed

The ultrasonic sensor uses GPIO 18 and 19

I also used a resistor divider for the Echo pin to reduce the voltage from 5V to 3.3V

![Circuit Diagram](assets/circuit-diagram.png)

## Log 3 Chassis Base

Time 4.5 hours

I started making the car body in Fusion 360

I made the base first and checked how much space I needed for the motors battery and electronics

I wanted the chassis to be small but still have enough room for everything

After making the base I checked where the wheels and motor mounts would go

![Chassis Base](assets/cad-sketch-base.png)

## Log 4 Finishing the Design

Time 3.5 hours

I continued working on the car design in Fusion 360

I made the motor mounts and checked where the wheels would sit

I also worked on the front part of the chassis for the ultrasonic sensor

After checking the full model I added some support around the motor mounts

I saved the finished design as a Fusion 360 file and also exported it as a STEP file

![Full CAD Assembly](assets/cad-full-assembly.png)

## Log 5 Assembly

Time 3.5 hours

After finishing the design I printed the chassis parts

I attached the four BO motors and fitted the wheels

Then I placed the ESP32 and L298N motor driver inside the car

I mounted the ultrasonic sensor at the front and connected the wires

I checked that the wheels could move without touching the body

![Car Electronics](assets/PHOTO-2026-10-23-02-08-37.jpg)

## Log 6 Hand Controller

Time 3.5 hours

I started working on the hand controller code using Arduino IDE

The MPU9250 reads the tilt of my hand and the ESP32 uses that to decide which command to send

I kept the tilt limit at 15 degrees so small movements would not make the car move

The controller sends commands every 100 milliseconds using ESP NOW

I also added the receiver ESP32 MAC address so both boards could communicate

![Gesture Code](assets/code-gesture-math.png)

## Log 7 Motor Control

Time 3 hours

I worked on the code for the ESP32 inside the car

It receives commands from the hand controller and controls the motors through the L298N driver

I set the motor speed to 180 out of 255

For turning one side of the wheels moves while the other side stops

I also added reverse mode which changes when I tilt my hand backward

![ESP NOW Code](assets/code-espnow-setup.png)

## Log 8 Obstacle Detection

Time 1.5 hours

I added the HC SR04 ultrasonic sensor to the car code

I kept the distance limit at 20 cm

If something comes too close the car stops and turns right for a short time

After turning it stops again

The code also checks the distance before moving forward

![Front Sensor Mount](assets/cad-bumper-mount.png)

## Log 9 Testing

Time 3 hours

After uploading the code I started checking the car

I tested the motor directions with the wheels raised

Then I tried moving the car using the hand controller

I checked the forward left and right movements and also tested reverse mode

I placed an object in front of the ultrasonic sensor to check how the car reacted

![Car Turning Test](assets/car-turning-test.jpg)

## Log 10 Final Demo

Time 1 hour

After finishing the car I recorded a short driving video

I used the hand controller to move the car in different directions

The controller sends commands using ESP NOW and the car moves based on the hand movements

I also kept the code photos and CAD files together in the project folder

![Chassis Reinforcement](assets/cad-reinforcement.png)

[Watch the Driving Video](assets/VIDEO-2026-10-23-02-05-10.mp4)
