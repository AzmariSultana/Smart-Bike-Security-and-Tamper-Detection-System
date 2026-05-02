# Smart-Bike-Security-and-Tamper-Detection-System
Smart Motorcycle Security System designed to provide robust, low-power protection against theft. The system intelligently differentiates between accidental bumps and genuine tampering using sensor fusion and a dual-stage alarm mechanism.

# Key Features

- Dual-Stage Motion Alarm: Uses an ADXL345 accelerometer to trigger a 3-second soft beep for light vibrations and a 5-second loud siren for sustained motion.

- Intelligent Sensor Fusion: Combines accelerometer data with a magnetic reed switch (on the kickstand) to detect physical movement or forced entry.

- Anti-Brute Force Lockout: Automatically enters Lockout Mode if the alarm is triggered 3 times within a 5-minute window, engaging an ignition kill-switch.

- Remote Tracking & Alerts: Sends real-time SMS notifications with Google Maps location links via GSM (SIM800L) and GPS (NEO-6M) modules.

- Tamper Logging: Records every security event with RTC (DS3231) timestamps and GPS coordinates into the EEPROM ring buffer for forensic evidence.

- Ride Mode: Automatically disables motion sensing when the ignition key is detected (Pin D3), preventing false alarms while riding.

# System States

- DISARMED: Normal operation; monitoring for auto-arm or key insertion.
- ARMED: Active monitoring of all sensors for motion or displacement.
- WARNING (Stage 1): Soft vibration/beep alert for minor disturbances (< 3s).
- ALARM (Stage 2): Loud siren and alternating tones for continuous motion (> 5s).
- LOCKOUT: Triggered after 3 incidents; ignores sensors and requires a secret button sequence to reset.

# Hardware Requirements

- Microcontroller: Arduino Uno
- Sensors: ADXL345 Accelerometer, NEO-6M GPS, Reed Switch
- Communication: SIM800L GSM/GPRS Module
- Timekeeping: DS3231 RTC Module
- Actuators: 5V Relay Module (Kill-switch), Active Buzzer, Vibration Motor
- Power: 18650 Li-ion Battery with TP4056 Charger and XL6009 Boost Converter

# Pin Mapping
- I2C Bus (ADXL345 Accelerometer & DS3231 RTC): Connect to A4 (SDA) and A5 (SCL) for data exchange and time stamping.
- Active Buzzer: Connected to D9 (PWM) to provide multi-tone stage alarms.
- Vibration Motor: Connected to D10 (PWM) for haptic feedback during Stage 2 alarms.
- NEO-6M GPS Module: Uses A1 (RX) and A2 (TX) for satellite coordinate tracking via SoftwareSerial.
- SIM800L GSM Module: Uses D7 (RX) and D8 (TX) for sending SMS alerts and receiving remote commands.
- Ignition Kill-Switch (Relay): Controlled via A0 to engage the anti-theft lockout.
- Reed Switch (Kickstand Sensor): Connected to D2 to detect physical movement when the stand is lifted.
- Ride Key Input: Connected to D3; detects key insertion (LOW) to trigger Ride Mode.
- Control Buttons: Three tactile buttons connected to D4, D5, and D6 for arming, disarming, and secret sequences.
- Status LEDs: D11 (Red) for tens digit logs, D12 (Green) for ones digit logs, and D13 (Blue) for general status.

# Usage & Configuration
- Arm System: Press Button 2 three times (2-2-2).

- Disarm System: Press Button 1 three times (1-1-1).

- Unlock from Lockout: Enter the secret sequence: Button 1 -> Button 2 -> Button 3.

- Clear Logs: Press Button 1, then Button 3 twice (1-3-3).

# SMS Commands
Send these commands from the MASTER_PHONE number:

- STATUS: Request a full system report including current state and last known GPS location.
- UNLOCK: Remotely disarm the system during a lockout.

# Initial Setup
- GSM Baud Rate: Ensure your GSM module is set to 9600 bps (use the provided setup utility if it is at the default 115200).
- Phone Configuration: Replace the MASTER_PHONE constant in the code with your actual mobile number including the country code (e.g., +88017...).
- GPS Fix: The GPS module requires a clear view of the sky to acquire a satellite lock.
