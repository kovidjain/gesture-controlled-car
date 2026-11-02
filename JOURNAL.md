
# The Nonchalant

## Build Journal

I made The Nonchalant to try controlling a car using my hand instead of a remote

It has four wheels and uses two ESP32 boards

One reads my hand movements and the other controls the car

I designed the body in Fusion 360 and used 3D printed parts for the chassis

These are my notes from making the car

![The Nonchalant](assets/PHOTO-2026-10-23-01-56-13.jpg)

## Log 1 Planning

Time 1.5 hours

I wanted to try making a car that could move when I tilted my hand

I chose an MPU9250 sensor to read the movement and two ESP32 boards to send commands between the controller and the car

For the wheels I used four BO motors with an L298N driver

I also wanted the car to detect things in front of it so I included an HC SR04 sensor

![Car](assets/PHOTO-2026-10-23-01-56-13.jpg)

## Log 2 Wiring

Time 2 hours

I worked out which pins to use for the sensors and motor driver

The MPU9250 uses GPIO 15 and 14 on the controller

On the car I used GPIO 26 25 17 and 16 for the motor directions

GPIO 32 and 33 are for motor speed

The ultrasonic sensor uses GPIO 18 and 19

I put a resistor divider on the Echo line because the sensor can send 5V and the ESP32 input needs 3.3V

![Circuit Diagram](assets/circuit-diagram.png)

## Log 3 Chassis Base

Time 4.5 hours

I opened Fusion 360 and started making the base of the car

I wanted enough room for the battery and electronics without making the body too big

I worked on the motor mounts and checked where the wheels would sit

I also planned the front part of the chassis for the ultrasonic sensor

![Chassis Base](assets/cad-sketch-base.png)

![Motor Mount](assets/cad-side-bracket.png)

## Log 4 Finishing the Design

Time 3.5 hours

I continued working on the Fusion 360 model

I made the front sensor mount and added support near the motor mounts

I checked the full assembly to see where the wheels and electronics would go

After that I saved the Fusion 360 file and exported the STEP model

![Sensor Mount](assets/cad-bumper-mount.png)

![Full Assembly](assets/cad-full-assembly.png)

![Chassis Support](assets/cad-reinforcement.png)

## Log 5 Assembly

Time 3.5 hours

After printing the parts I started putting the car together

I attached the four motors and wheels to the chassis

Then I placed the ESP32 and L298N driver inside the body

The ultrasonic sensor went at the front

I connected the wires and checked that nothing was touching the wheels

![Car Assembly](assets/PHOTO-2026-10-23-02-08-37.jpg)

## Log 6 Hand Controller

Time 3.5 hours

I wrote the controller code using Arduino IDE

The MPU9250 reads the tilt of my hand and the ESP32 turns that into movement commands

I used 15 degrees as the limit for detecting a gesture

The controller sends commands every 100 milliseconds using ESP NOW

I also had to enter the MAC address of the ESP32 on the car so the two boards could communicate

![ESP NOW Code](assets/code-espnow-setup.png)

![Gesture Code](assets/code-gesture-math.png)

## Log 7 Motor Control

Time 3 hours

I worked on the code for the ESP32 inside the car

It receives the commands from the hand controller and uses the L298N to control the motors

I set the motor speed to 180 out of 255

For turning one side of the wheels moves while the other side stops

I also added reverse mode which changes when I tilt my hand backward

Tilting backward again changes it back

![Car Turning](assets/car-turning-test.jpg)

## Log 8 Obstacle Sensor

Time 1.5 hours

I worked on the ultrasonic sensor code

The sensor checks the distance in front of the car

I kept the limit at 20 cm

If an object is too close the car stops turns right for a short time and stops again

The car also checks the distance before moving forward

![Front Sensor Mount](assets/cad-bumper-mount.png)

## Log 9 Testing

Time 3 hours

I tested the motors with the wheels raised first

Then I tried the hand controller to check the forward left and right movements

I checked the reverse mode too

I also placed an object in front of the ultrasonic sensor to check the stopping and turning behavior

![Car Test](assets/car-turning-test.jpg)

## Log 10 Final Demo

Time 1 hour

I recorded a short video of the car moving with the hand controller

The controller sends commands over ESP NOW and the car follows the hand movements

I kept the video photos code and CAD files in the project folder

This was the final part of my build

![Final Car](assets/PHOTO-2026-10-23-01-56-13.jpg)

[Watch the Driving Video](assets/VIDEO-2026-10-23-02-05-10.mp4)

## Work Hours

| Work | Hours |
|---|---:|
| Planning | 1.5 |
| Wiring | 2 |
| Chassis Base | 4.5 |
| Finishing the Design | 3.5 |
| Assembly | 3.5 |
| Hand Controller | 3.5 |
| Motor Control | 3 |
| Obstacle Sensor | 1.5 |
| Testing | 3 |
| Final Demo | 1 |
| **Total** | **27** |

## Final Notes

I wanted to build a car that I could control without using a normal remote

This project gave me a chance to work with ESP32 boards sensors motors and 3D design

I learned how to send commands using ESP NOW and how to use hand movements to control the car

I still have a few things I want to improve later
