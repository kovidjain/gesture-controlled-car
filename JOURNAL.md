
# The Nonchalant — Build Journal

## Stage 1 — The idea

**Time spent: 2h 30m**

I wanted to make a small car that I could control just by moving my hand

Instead of using a remote with buttons I thought it would be more interesting to use a sensor to read the tilt of my hand

I chose the MPU9250 for this and decided to use two ESP32 boards. One would stay in my hand and the other would go inside the car

I used ESP NOW to send the commands between the boards without needing a WiFi router

I also wanted to design the body myself in Fusion 360

![Finished Car](assets/PHOTO-2026-10-23-01-56-13.jpg)

## Stage 2 — Wiring everything

**Time spent: 2h**

I started by figuring out all the connections for the controller and the car

The hand controller needed the MPU9250 connected to GPIO 15 and 14 on the ESP32

The car had more wires because of the four motors and the L298N motor driver

I used GPIO 26 25 17 and 16 for the motor directions and GPIO 32 and 33 for speed control

I connected the ultrasonic sensor to GPIO 18 and 19

I also used a resistor divider on the Echo wire because the ESP32 needs a 3.3V signal

![Circuit Diagram](assets/circuit-diagram.png)

## Stage 3 — Designing the base

**Time spent: 4h 30m**

I opened Fusion 360 and started working on the bottom part of the car

I needed enough room for the battery and electronics while keeping the body fairly small

I worked on the shape of the base and where the four motors would sit

I checked the wheel positions and made sure there was enough space around them

I also thought about where the wires would go when everything was assembled

![Chassis Base](assets/cad-sketch-base.png)

## Stage 4 — Finishing the CAD design

**Time spent: 3h 30m**

After the base was ready I worked on the other parts of the chassis

I made the motor mounts and the front section for the ultrasonic sensor

I added some reinforcement so the body would be stronger after printing

I checked the full model in Fusion 360 to see how everything would fit together

When I finished the model I saved the Fusion 360 file and exported a STEP file

![Full CAD Model](assets/cad-full-assembly.png)

## Stage 5 — Assembling the car

**Time spent: 3h 30m**

Once the chassis parts were printed I started putting the car together

I fitted the four BO motors and attached the wheels

Then I placed the ESP32 and L298N motor driver inside the chassis

I had to leave space for the battery and wiring

I mounted the ultrasonic sensor at the front and connected the remaining wires

After that I checked whether the wheels could rotate without touching the body

![Car Assembly](assets/PHOTO-2026-10-23-02-08-37.jpg)

## Stage 6 — Coding the hand controller

**Time spent: 3h 30m**

I worked on the code that reads the hand movements using the MPU9250

The sensor gives the tilt readings and the ESP32 uses them to decide which command to send

I kept the tilt threshold at 15 degrees so small movements would not keep changing the direction

Tilting forward sends a forward command and tilting sideways sends the turning commands

Keeping my hand level makes the car stop

I also used a backward tilt to switch reverse mode

The commands are sent using ESP NOW about every 100 milliseconds

![Gesture Controller Code](assets/code-gesture-math.png)

## Stage 7 — Motor control

**Time spent: 3h**

I worked on the receiver code for the ESP32 inside the car

The receiver gets commands from the hand controller and uses the L298N to control the motors

I set the PWM speed to 180 out of 255

For turning I made one side of the wheels move while the other side stopped

This lets the car turn without a separate steering mechanism

I also added the reverse mode so the driving direction could be changed from the controller

![ESP NOW Setup](assets/code-espnow-setup.png)

## Stage 8 — Obstacle detection

**Time spent: 1h 30m**

I added the HC SR04 ultrasonic sensor because I wanted the car to react when something was in front of it

I set the distance limit to 20 cm

If an object gets too close the car stops and turns right for a short time

After turning it stops again

I also made the code check the distance before moving forward

![Ultrasonic Sensor Mount](assets/cad-bumper-mount.png)

## Stage 9 — Testing the car

**Time spent: 2h**

After uploading the code to both ESP32 boards I started testing the car

I first checked the motor directions while the wheels were raised

Then I put the car on the floor and tried controlling it by tilting my hand

I checked forward movement and both turning directions

I also tested reverse mode and placed an object in front of the ultrasonic sensor to check the obstacle response

![Car Turning Test](assets/car-turning-test.jpg)

## Stage 10 — Final demo

**Time spent: 1h**

After getting the car working I recorded a short video of it moving

I used the hand controller to show the forward movement and turning

The two ESP32 boards communicate using ESP NOW so the controller doesn't need a router

I kept the Arduino code CAD files and photos together so I could share the project

There are still a few things I could improve later but I got the main hand controlled car working

![Chassis Reinforcement](assets/cad-reinforcement.png)

[Watch the Driving Video](assets/VIDEO-2026-10-23-02-05-10.mp4)
