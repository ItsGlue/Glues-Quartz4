>SASE Engineering Team

**2025 Fall:**\
We made a 3 DOF robot arm using Arduino and servos. Later we would implement an IMU and serial communication with Python. We also experimented with motor controllers and various power supplies which would be important for driving the robot.
<div align="center" style="font-size: 1.3rem;"> * * * </div>

Robot Arm:\
![[Screenshot 2026-05-20 at 1.49.55 AM.png|324]]

Python script:
```
import serial
import time

arduino = serial.Serial(port='COM3', baudrate=9600, timeout=1)
time.sleep(2)

def move_servos(elbow, shoulder, body):
    cmd = f"{elbow},{shoulder},{body}\n"
    arduino.write(cmd.encode('utf-8'))
    time.sleep(0.1)
    while arduino.in_waiting:
        response = arduino.readline().decode().strip()
        print("Arduino:", response)

move_servos(69, 69, 69)
move_servos(80, 10, 45)
```

**2026 Spring:**\
In the spring we would begin finalizing the circuit design on altium and also work on the SET side project.

[[SET Side Project]]