# Humanoid Robot: 6-Servo Control & Walking Motion

This project demonstrates basic servo motor control and outlines a walking motion algorithm for a humanoid robot. It includes an Arduino sketch that programs **6 servo motors** to perform a synchronized sweep motion for 2 seconds, followed by holding all motors at a fixed 90° position. The design and simulation were created using **Tinkercad**.

---

## Project Overview

- Control 6 servo motors using Arduino
- Perform synchronized sweep motion for 2 seconds
- Hold all motors at 90° after sweeping
- Design and simulate the circuit in Tinkercad
- Outline a walking algorithm for humanoid locomotion

---

## Hardware Requirements

- Arduino Uno or compatible board  
- 6 Servo motors (e.g., SG90 or MG996R)  
- External power supply for servos  
- Breadboard and jumper wires  
- USB cable for programming  

---

#### This Arduino sketch performs the following:

1. **Initialization**: Attaches 6 servo motors to pins 2–7.
2. **Sweep Phase**: All servos sweep from 0° to 180° and back for 2 seconds.
3. **Hold Phase**: All servos are set to 90° and remain fixed.

#### Motion Summary

```text
- Sweep: 0° → 180° → 0° (repeated for 2 seconds)
- Hold: All servos set to 90° indefinitely
```

---

## Walking Motion Algorithm

This algorithm outlines how a humanoid robot can walk using 6 servo motors—3 per leg (hip, knee, and ankle). The motion is based on alternating leg movement and shifting the robot’s center of mass.

---

## Step-by-Step Algorithm

```text
1. Initialize all servos to standing position (legs straight, feet flat).

2. Shift weight to left leg:
   - Slightly bend left knee and ankle.
   - Tilt torso left for balance.

3. Lift right leg:
   - Raise right hip.
   - Bend right knee and ankle to lift foot.

4. Move right leg forward:
   - Rotate right hip forward.
   - Extend right knee slightly.

5. Place right foot down:
   - Lower right hip.
   - Straighten right knee and ankle.

6. Shift weight to right leg:
   - Slightly bend right knee and ankle.
   - Tilt torso right for balance.

7. Lift left leg:
   - Raise left hip.
   - Bend left knee and ankle.

8. Move left leg forward:
   - Rotate left hip forward.
   - Extend left knee slightly.

9. Place left foot down:
   - Lower left hip.
   - Straighten left knee and ankle.

10. Repeat steps 2–9 for continuous walking.
```

---

## Tinkercad Simulation

[View Tinkercad Project](https://www.tinkercad.com/things/dM8usR6bpeF-6-servo-motors?sharecode=bUMjEK4jpvu4HrTlsLACRMI9x5N1ijWmqF1_MvRmrgA)

---

## Preview

![tinkercad design]()

---

## Design Overview

- **Arduino Uno** connected to 6 servo motors 
- **External power supply** for servo stability  
- **Breadboard layout** for organized wiring  
- Simulated **sweep and hold behavior** matching the Arduino code

---

## Code

```code
#include <Servo.h>

Servo servos[6];  // Array to hold 6 servo objects
int pos = 0;      // Position variable

unsigned long startTime;
const int sweepDuration = 2000; // Duration to sweep in milliseconds

void setup() {
  // Attach each servo to its respective pin (adjust pins as needed)
  servos[0].attach(2);
  servos[1].attach(4);
  servos[2].attach(7);
  servos[3].attach(8);
  servos[4].attach(12);
  servos[5].attach(13);

  startTime = millis(); // Record the start time
}

void loop() {
  // Sweep for 2 seconds
  while (millis() - startTime < sweepDuration) {
    for (pos = 0; pos <= 180; pos += 1) {
      for (int i = 0; i < 6; i++) {
        servos[i].write(pos);
      }
      delay(15);
    }
    for (pos = 180; pos >= 0; pos -= 1) {
      for (int i = 0; i < 6; i++) {
        servos[i].write(pos);
      }
      delay(15);
    }
  }

  // After sweeping, hold all servos at 90 degrees
  for (int i = 0; i < 6; i++) {
    servos[i].write(90);
  }

  // Stop further execution
  while (true); // Infinite loop to freeze at 90°
}
```
