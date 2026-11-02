# The Nonchalant: ESP32 gesture-controlled car

The Nonchalant is a four-wheel-drive car that I designed and built to explore a different kind of remote control. I tilt a hand-held MPU-9250 sensor to send movement commands from one ESP32 to another over ESP-NOW. The ESP32 on the car drives the motors through an L298N board, while an HC-SR04 sensor checks for obstacles in front.

The project folder includes the Arduino sketches, wiring diagram, build photos, a short driving video, and Fusion 360 and STEP CAD files.

![The assembled car](assets/PHOTO-2026-10-23-01-56-13.jpg)

![Electronics mounted in the car](assets/PHOTO-2026-10-23-02-08-37.jpg)

## How it works

The controller reads the accelerometer, calculates pitch and roll, and sends a command about every 100 ms. Tilting past the 15-degree threshold selects forward, left, right, or reverse. A level hand sends the brake command. Reverse is a toggle: tilting backward changes the direction state on the car, and another backward command changes it back.

The receiver uses skid steering. It controls the left and right motor pairs separately, so it can slow one side to turn. When the distance sensor sees an object within 20 cm, the receiver stops, turns right briefly, and stops again.

```text
Hand tilt → MPU-9250 → Controller ESP32
                           │ ESP-NOW
                           ▼
HC-SR04 → Receiver ESP32 → L298N → 4 motors
```

## Parts used

| Part | Qty. | Role |
|---|---:|---|
| ESP32 development board | 2 | Hand controller and car receiver |
| MPU-9250 IMU | 1 | Measures hand tilt |
| L298N motor driver | 1 | Drives the left and right motor pairs |
| BO geared DC motors and wheels | 4 each | Move the car |
| HC-SR04 ultrasonic sensor | 1 | Checks distance in front of the car |
| 7.4 V battery pack | 1 | Main power source |
| 3D-printed chassis parts | — | Hold the motors and electronics |

## Wiring

### Hand controller: MPU-9250 to ESP32

| MPU-9250 | ESP32 |
|---|---|
| VCC | 3V3 |
| GND | GND |
| SDA | GPIO 15 |
| SCL | GPIO 14 |

### Car: L298N to ESP32

| L298N | ESP32 |
|---|---|
| IN1 | GPIO 26 |
| IN2 | GPIO 25 |
| IN3 | GPIO 17 |
| IN4 | GPIO 16 |
| ENA | GPIO 32 |
| ENB | GPIO 33 |

The left motors are connected together on one L298N output pair; the right motors use the other pair. GPIO 32 and 33 set the motor speed in the receiver sketch.

### Car: HC-SR04 to ESP32

| HC-SR04 | ESP32 |
|---|---|
| VCC | 5V |
| GND | GND |
| TRIG | GPIO 18 |
| ECHO | GPIO 19, through a resistor divider |

The HC-SR04 Echo pin can output 5 V. Use a resistor divider to bring it down to 3.3 V before connecting it to the ESP32. Join the grounds of the battery, driver, sensor, and ESP32. Do not power the motors from ESP32 GPIO pins.

![Circuit diagram](assets/circuit-diagram.png)

## Uploading the sketches

1. Install the ESP32 board support package and the `MPU9250_asukiaaa` library in Arduino IDE.
2. Upload a sketch that prints the receiver ESP32's MAC address, then copy that address.
3. In `GestureController/GestureController.ino`, replace the example bytes in `carMAC` with the receiver's MAC address.
4. Upload `GestureController.ino` to the hand controller and `GestureCarReceiver.ino` to the car receiver.
5. Open both serial monitors at 115200 baud. Check that the controller prints commands and that the car reports ESP-NOW ready.
6. With the wheels off the ground, check the motor directions and steering before driving on the floor.

The MAC address in the checked-in controller sketch is a placeholder, so the two boards will not communicate until you replace it.

## CAD and project files

- [`3D Cad/The Nonchalant (1).f3d`](3D%20Cad/The%20Nonchalant%20%281%29.f3d) — editable Fusion 360 design
- [`3D Cad/The Nonchalant.step`](3D%20Cad/The%20Nonchalant.step) — STEP assembly export
- `GestureController/` — transmitter sketch
- `GestureCarReceiver/` — receiver and motor-control sketch
- `assets/` — photos, circuit diagram, model preview, and demo video
- [`JOURNAL.md`](JOURNAL.md) — build notes

![CAD model](assets/car-3d-model.svg)

## Demo

[Watch the driving video](assets/VIDEO-2026-10-23-02-05-10.mp4)
