# Smart-Bike-Security-and-Tamper-Detection-System
Smart Motorcycle Security System designed to provide robust, low-power protection against theft. The system intelligently differentiates between accidental bumps and genuine tampering using sensor fusion and a dual-stage alarm mechanism.

# Key Features

Dual-Stage Motion Alarm: Uses an ADXL345 accelerometer to trigger a 3-second soft beep for light vibrations and a 5-second loud siren for sustained motion.

Intelligent Sensor Fusion: Combines accelerometer data with a magnetic reed switch (on the kickstand) to detect physical movement or forced entry.

Anti-Brute Force Lockout: Automatically enters Lockout Mode if the alarm is triggered 3 times within a 5-minute window, engaging an ignition kill-switch.

Remote Tracking & Alerts: Sends real-time SMS notifications with Google Maps location links via GSM (SIM800L) and GPS (NEO-6M) modules.

Tamper Logging: Records every security event with RTC (DS3231) timestamps and GPS coordinates into the EEPROM ring buffer for forensic evidence.

Ride Mode: Automatically disables motion sensing when the ignition key is detected (Pin D3), preventing false alarms while riding.

