# Build journal: The Nonchalant

These are my notes from designing and assembling the gesture-controlled car. I kept the wiring, firmware, and chassis work in one project so I could check the mechanical and electronics decisions together.

## Planning the controls

I wanted to try a hand-tilt controller instead of a joystick. I chose two ESP32 boards so one could read the sensor and the other could stay on the car. ESP-NOW lets them exchange the small movement commands directly. I also planned an ultrasonic sensor for the front of the chassis, with the L298N driving the four geared motors in left and right pairs.

The first wiring plan used GPIO 15 and 14 for I2C on the controller. On the car, the L298N direction pins use GPIOs 26, 25, 17, and 16; the enable pins use 32 and 33. The HC-SR04 uses GPIO 18 for trigger and 19 for echo. I added a resistor divider to the echo line because the ESP32 input is 3.3 V tolerant and the sensor echo can be 5 V.

![Circuit plan](assets/circuit-diagram.png)

## Designing the chassis

I made the chassis in Fusion 360 and called the project “The Nonchalant.” I wanted a custom layout for the motors, battery, driver, and sensor instead of starting from a flat plate. I worked on the base first, then the motor mounts and the front sensor opening. The assembly view helped me check where the wheels and electronics would sit before printing.

![Chassis sketch](assets/cad-sketch-base.png)

![Motor mount detail](assets/cad-side-bracket.png)

![Front sensor mount](assets/cad-bumper-mount.png)

I added reinforcement around the chassis and motor-mount areas, then exported the model as Fusion 360 and STEP files. The project folder contains the assembly files and CAD images used during the design.

![Full CAD assembly](assets/cad-full-assembly.png)

![Reinforced chassis detail](assets/cad-reinforcement.png)

## Assembly

After printing the parts, I mounted the four BO motors and fitted the wheels. The receiver ESP32 and L298N sit in the chassis, and the HC-SR04 fits at the front. I routed the wires inside the body and checked that the wheels could turn without rubbing against it.

![Electronics inside the chassis](assets/PHOTO-2026-10-23-02-08-37.jpg)

## Controller firmware

The controller sketch reads the MPU-9250 accelerometer over I2C and calculates pitch and roll. A tilt past 15 degrees selects a movement command; when the hand is closer to level, it sends a brake command. The sketch sends a packet about every 100 ms over ESP-NOW.

I used GPIO 15 for SDA and GPIO 14 for SCL. The receiver's MAC address has to be entered in the `carMAC` array before the boards can talk to each other. The value in the repository is an example placeholder.

![ESP-NOW setup](assets/code-espnow-setup.png)

![Gesture angle calculation](assets/code-gesture-math.png)

## Receiver and driving behavior

The receiver sketch maps each command to the motor pins. It uses PWM on GPIOs 32 and 33, with the speed set to 180 on an 8-bit scale. Left and right turns stop one motor pair while driving the other. A backward tilt toggles the reverse direction state.

The distance check uses a 20 cm threshold. When an object is close, the receiver brakes, waits briefly, turns right for a short interval, and brakes again. The sketch also checks for an obstacle before driving forward.

![Car turning during a test](assets/car-turning-test.jpg)

The folder includes a short driving video and additional assembly photos. Before repeating the build, I would check the motor directions with the wheels raised and confirm the receiver MAC address in the controller sketch.

[Driving video](assets/VIDEO-2026-10-23-02-05-10.mp4)
