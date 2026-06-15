# Automatic Garbage Bin

![Platform](https://img.shields.io/badge/Platform-Arduino%20Uno-teal)
![Language](https://img.shields.io/badge/Language-Arduino%20C%2B%2B-blue)
![License](https://img.shields.io/badge/License-MIT-yellow)

A touchless automatic garbage bin that uses an HC-SR04 ultrasonic sensor to detect proximity and opens the lid via a servo motor — no physical contact required.

## Demo

![Hardware build](photo.jpg)

A working hardware build with the servo mounted on the lid and the HC-SR04 sensor facing outward. See [`video.mp4`](video.mp4) for a live demonstration.

## How It Works

1. The HC-SR04 sensor fires a 15 µs ultrasonic pulse and measures the echo return time.
2. Three readings are averaged to reduce noise.
3. If the measured distance is **< 50 cm**, the LED lights up and the servo opens the lid to 0°.
4. After 3 seconds the lid closes (servo moves to 150°) and the LED turns off.
5. The distance reading is printed to the Serial Monitor (9600 baud) each cycle.

## Hardware & Wiring

| Component | Details |
|---|---|
| Microcontroller | Arduino Uno |
| Distance sensor | HC-SR04 ultrasonic sensor |
| Actuator | Servo motor (standard, e.g. SG90) |
| Indicator | LED |
| Library | `Servo` (built into Arduino IDE) |

**Pin connections:**

| Component | Arduino Pin |
|---|---|
| HC-SR04 Trig | 5 |
| HC-SR04 Echo | 6 |
| Servo signal | 7 |
| LED | 10 |

See the [Tinkercad simulation](https://www.tinkercad.com/things/lCdzYm1MBHx) for the full circuit diagram.

## Prerequisites

- [Arduino IDE](https://www.arduino.cc/en/software) (any recent version)
- `Servo` library — ships with the Arduino IDE; no separate install needed
- Arduino Uno board + USB cable
- HC-SR04, servo motor, LED, breadboard, and jumper wires

## Installation

```bash
git clone https://github.com/archiskhuspe/automatic-garbage-bin.git
```

1. Open `automatic_garbage_bin.ino` in the Arduino IDE.
2. Select board: **Arduino Uno** and the correct port.
3. Click **Upload**.

## Project Structure

```
automatic-garbage-bin/
├── automatic_garbage_bin.ino   # Main Arduino sketch
├── photo.jpg                   # Hardware build photos
├── video.mp4                   # Demo video
├── research_paper.pdf          # Project report
├── LICENSE
└── README.md
```

## Limitations

- Detection threshold is fixed at 50 cm (not configurable without editing the sketch).
- No debouncing — if someone lingers within range, the lid will chain open/close cycles.
- No fill-level sensing; the bin does not indicate when it is full.
- HC-SR04 has a blind spot closer than ~2 cm and can misread highly angled surfaces.
- Serial output is for debugging only; not connected to any dashboard or alert system.

## License

Released under the [MIT License](LICENSE).
