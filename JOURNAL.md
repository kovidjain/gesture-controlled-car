
# The Nonchalant — Build Journal

## Stage 1 — Starting with the idea

**Time spent: 2h 30m**

I wanted to make a car that could move based on how I tilted my hand. I didn't want to use a normal remote because I wanted to try something different.

I decided to use an MPU9250 sensor to read my hand movements and two ESP32 boards to communicate using ESP-NOW.

I planned to use four BO motors with an L298N motor driver. I also wanted to add an ultrasonic sensor so the car could avoid obstacles.

I decided to design the chassis myself in Fusion 360.

![Finished Car](assets/PHOTO-2026-10-23-01-56-13.jpg)

## Stage 2 — Parts and wiring

**Time spent: 2h**

I started working on the circuit connections. I connected the MPU9250 to the controller ESP32 using GPIO 15 and 14.

On the car I connected the L298N motor driver to GPIO 26, 25, 17 and 16. I used GPIO 32 and 33 for motor speed control.

I also connected the ultrasonic sensor using GPIO 18 and 19. Since the Echo pin can output 5V, I used a resistor divider to protect the ESP32.

I made a circuit diagram so I could keep track of the connections.

![Circuit Diagram](assets/circuit-diagram.png)

## Stage 3 — Designing the chassis base

**Time spent: 4h 30m**

I opened Fusion 360 and started designing the base of the car.

I had to make enough space for the battery, motors and electronics. I also needed to think about where the wheels would sit.

I made the basic shape first and then worked on the motor mounting positions.

I checked the dimensions because I wanted everything to fit properly after printing.

![Chassis Base](assets/cad-sketch-base.png)

## Stage 4 — Finishing the 3D design

**Time spent: 3h 30m**

I continued working on the chassis in Fusion 360.

I made the remaining mounting parts and added a place for the ultrasonic sensor at the front.

I also added some reinforcement around the chassis so it would be stronger.

After checking the complete model, I saved the Fusion 360 design and exported a STEP file.

![Full CAD Assembly](assets/cad-full-assembly.png)

## Stage 5 — Printing and assembling the car

**Time spent: 3h 30m**

After finishing the design I started putting the car together.

I fitted the four BO motors into the printed chassis and attached the wheels.

Then I placed the ESP32, L298N motor driver and battery inside the car.

I also mounted the ultrasonic sensor at the front and connected the wires.

I checked the wheel movement and made sure the parts were fitted properly.

![Car Assembly](assets/PHOTO-2026-10-23-02-08-37.jpg)

## Stage 6 — Making the hand controller

**Time spent: 3h 30m**

I started writing the code for the hand controller in Arduino IDE.

The MPU9250 reads the tilt of my hand. I used the readings to decide whether the car should move forward, left, right or stop.

I kept the tilt threshold at 15 degrees because I didn't want small hand movements to trigger commands.

I used ESP-NOW to send commands to the car every 100 milliseconds.

I also added a reverse toggle using a backward hand movement.

![Gesture Controller Code](assets/code-gesture-math.png)

## Stage 7 — Getting the motors to move

**Time spent: 3h**

I worked on the receiver ESP32 code.

The car receives commands from the hand controller and uses the L298N motor driver to control the wheels.

I set the PWM speed to 180 out of 255.

For turning I made one side of the motors run while the other side stopped. This allowed the car to turn without needing a steering mechanism.

I also worked on making sure the reverse command changed the driving direction.

![ESP NOW Code](assets/code-espnow-setup.png)

## Stage 8 — Adding obstacle detection

**Time spent: 1h 30m**

I worked on the HC-SR04 ultrasonic sensor.

I set the obstacle distance to 20 cm.

When the sensor detects something too close in front of the car, the code stops the motors and makes the car turn right for a short time.

After turning it stops again.

I also added a distance check before the car moves forward.

![Ultrasonic Sensor Mount](assets/cad-bumper-mount.png)

## Stage 9 — Testing everything

**Time spent: 2h**

I started testing the car after uploading the code to both ESP32 boards.

First I checked the motor directions with the wheels raised.

Then I tested the hand gestures to see if the car moved in the correct direction.

I also checked the reverse toggle and the obstacle detection.

I tested the car on the floor to see how it behaved while turning and moving forward.

![Car Turning Test](assets/car-turning-test.jpg)

## Stage 10 — Final demo

**Time spent: 1h**

After putting everything together I recorded a short video of the car moving.

I used the hand controller to move the car forward and turn it.

I also checked that the wireless communication was working during the demo.

I kept the code, CAD files and project photos together so I could upload them with the project.

![Chassis Reinforcement](assets/cad-reinforcement.png)

[Watch the Demo Video](assets/VIDEO-2026-10-23-02-05-10.mp4)
