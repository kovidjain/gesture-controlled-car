
# The Nonchalant — Build Journal

## Stage 1 — The idea

**Time spent: 2h 30m**

I wanted to try making a car that I could move without holding a normal remote

The idea was to use my hand to control it. Like tilting my hand forward to move and sideways to turn

I had an MPU9250 in mind for reading the tilt and decided to use two ESP32 boards. One would be in my hand and the other would stay on the car

I chose ESP NOW because I didn't want to make an app or connect everything to WiFi

I also decided to make the car body myself in Fusion 360

At this point I had a rough idea of what I wanted and which parts I would need

![Finished Car](assets/PHOTO-2026-10-23-01-56-13.jpg)

## Stage 2 — Getting the wiring sorted

**Time spent: 2h**

There were quite a few connections to work out for this car

The controller side only needed the MPU9250 connected to the ESP32. I used GPIO 15 for SDA and GPIO 14 for SCL

The car side had more wires because of the four motors and the L298N driver

I connected the motor control pins to GPIO 26 25 17 and 16. The speed control pins went to GPIO 32 and 33

The ultrasonic sensor used GPIO 18 and 19

I also used a resistor divider on the Echo wire because I couldn't connect the 5V signal directly to the ESP32

I kept the circuit diagram nearby so I could check the connections

![Circuit Diagram](assets/circuit-diagram.png)

## Stage 3 — Starting the chassis in Fusion 360

**Time spent: 4h 30m**

I started the 3D model with the bottom plate of the car

I needed a place for four motors and a battery and I also had to leave space for the ESP32 and motor driver

I didn't want the body to be much bigger than it needed to be

I worked on the base shape and the motor positions first

I spent time checking the dimensions and thinking about where the wires would pass through

This was the first proper part of the car that I made in Fusion 360

![Chassis Base](assets/cad-sketch-base.png)

## Stage 4 — The rest of the 3D model

**Time spent: 3h 30m**

After the base I worked on the parts that would hold everything in place

I made the motor mounts and the front section for the ultrasonic sensor

I also added some reinforcement to the chassis

I looked at the complete assembly in Fusion 360 to check where everything would sit

Once the model was ready I saved the Fusion 360 file and exported a STEP version too

![Full CAD Model](assets/cad-full-assembly.png)

## Stage 5 — Building the actual car

**Time spent: 3h 30m**

This was the part where I could finally put the pieces together

I fitted the BO motors into the printed chassis and attached all four wheels

Then I placed the ESP32 and the L298N motor driver on the car

I had to keep the battery and wiring in mind because there wasn't unlimited space inside

I mounted the ultrasonic sensor at the front

After connecting everything I checked that the wheels had enough room to rotate

![Car Assembly](assets/PHOTO-2026-10-23-02-08-37.jpg)

## Stage 6 — Writing the hand controller code

**Time spent: 3h 30m**

I started working on the part that reads my hand movements

The MPU9250 gives the readings and I use them to work out which way my hand is tilted

I kept the limit at 15 degrees because I didn't want tiny movements to keep changing the direction

When I tilt my hand forward it sends a forward command. Tilting left or right sends the turning commands

When my hand is level it sends the brake command

I also used a backward tilt to change reverse mode

The controller sends the commands using ESP NOW about every 100 milliseconds

![Hand Controller Code](assets/code-gesture-math.png)

## Stage 7 — Making the car respond

**Time spent: 3h**

Now I had to make the ESP32 on the car do something with the commands it received

I wrote the receiver code and connected it to the motor driver controls

I kept the PWM value at 180 out of 255

For turning I made one side of the wheels run while the other side stopped

I didn't need a separate steering motor because the car turns using the wheels on each side

I also added the reverse mode so I could change the driving direction from the hand controller

![ESP NOW Setup](assets/code-espnow-setup.png)

## Stage 8 — Working on the obstacle sensor

**Time spent: 1h 30m**

I wanted the car to react if something was directly in front of it

I used the HC SR04 sensor for checking the distance

I set the distance limit to 20 cm

If an object is too close the car brakes and turns right for a short time

It stops again after turning

I also made the receiver check the distance before moving forward

![Front Sensor Mount](assets/cad-bumper-mount.png)

## Stage 9 — Testing the movements

**Time spent: 2h**

Once the code was uploaded to both ESP32 boards I started testing everything together

I checked the motors with the wheels raised first

Then I put the car down and tried the hand controller

I checked whether it moved forward and turned the right way when I tilted my hand

I tried the reverse toggle as well

I also placed something in front of the ultrasonic sensor to check the obstacle response

![Car Turning Test](assets/car-turning-test.jpg)

## Stage 10 — Final video

**Time spent: 1h**

After the car was working I recorded a short video of it moving

I used the hand controller to show the forward movement and turning

The controller and car communicate directly using ESP NOW so I didn't need to connect them to a router

I kept the CAD model Arduino code and project pictures together for uploading

I still have a few things I could improve but I was able to make the hand controlled car I originally wanted

![Chassis Reinforcement](assets/cad-reinforcement.png)

[Watch the Driving Video](assets/VIDEO-2026-10-23-02-05-10.mp4)
