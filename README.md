# FreeRTOS IMU Velocity Estimation

Real-time velocity estimation of an aircraft model from two MPU6050 IMUs
(accelerometer + gyroscope), running 5 FreeRTOS tasks on Arduino Mega 2560, Real-Time Programming course, UPB, Jan 2025.

## Architecture
- 5 tasks: read accel (5 ms), read gyro (40 ms), integrate accel, integrate gyro
  (+ complementary filter), body→Earth frame transform; periodic serial print via SimpleTimer
- Task synchronization via FreeRTOS semaphores/mutexes
- Euler integration, ZYX rotation matrix

## Hardware
Arduino Mega 2560, 2× MPU6050 on shared I2C (0x68 / 0x69). Wokwi circuit:

<img width="620" height="573" alt="Screenshot 2026-10-06 at 02 16 20" src="https://github.com/user-attachments/assets/863a23f8-b74e-4681-bd0a-62a4b82f1c31" />


## Dependencies
Arduino_FreeRTOS, Adafruit MPU6050, Adafruit Unified Sensor, SimpleTimer

## Results & known limitations
Static and slow-motion scenarios stable; abrupt motion diverges
(integration drift, no gravity compensation). See docs/.
