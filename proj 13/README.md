Women Safety IoT Device

An IoT-based women safety device designed to provide an emergency alert when the user presses an SOS button. The device uses an ESP32 microcontroller, GPS for location information, and a GSM module to send an emergency SMS. A buzzer and LED provide local indications.

Features

Emergency SOS button

GPS location tracking

Emergency SMS alert

Audible buzzer alarm

LED status indication

ESP32-based control

Automatic emergency message generation

Simulation and testbench support

System Architecture
                    ┌──────────────────┐
                    │    SOS Button    │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │      ESP32       │
                    │  Microcontroller  │
                    └─────┬─────┬──────┘
                          │     │
              ┌───────────┘     └──────────────┐
              ▼                                ▼
       ┌──────────────┐                 ┌──────────────┐
       │  GPS Module  │                 │ GSM Module   │
       │   NEO-6M     │                 │ SIM800L      │
       └──────┬───────┘                 └──────┬───────┘
              │                                │
              ▼                                ▼
       Location Data                     Emergency SMS
                                              
                    ┌──────────────────┐
                    │ Buzzer + LED     │
                    │ Emergency Alarm  │
                    └──────────────────┘

Components
Component	Purpose
ESP32	Main controller
NEO-6M GPS	Obtains latitude and longitude
SIM800L GSM	Sends emergency SMS
Push Button	Emergency/SOS input
Buzzer	Local emergency alarm
LED	Device status
Resistors	Current limiting/pull-up
Breadboard	Prototype construction
Jumper wires	Connections
Pin Connections
SOS Button
Device	ESP32
Button	GPIO 27
Other terminal	GND

The ESP32 internal pull-up resistor is used.

Buzzer
Device	ESP32
Buzzer +	GPIO 26
Buzzer -	GND
LED
Device	ESP32
LED anode	GPIO 2
LED cathode	GND through resistor
GPS NEO-6M
GPS	ESP32
TX	GPIO 16
RX	GPIO 17
GND	GND
VCC	Appropriate supply
SIM800L
SIM800L	ESP32
TX	GPIO 4
RX	GPIO 5
GND	GND
VCC	Dedicated suitable supply

Important: SIM800L modules can require significant current during transmission. Use a suitable power supply rather than powering the module directly from an ESP32 GPIO pin.

Software Requirements

Arduino IDE

ESP32 board package

TinyGPS++ library

ESP32-compatible serial communication

GSM SIM card with SMS capability

Required Library

Install:

TinyGPSPlus


In Arduino IDE:

Sketch → Include Library → Manage Libraries


Search for TinyGPSPlus and install it.

Working Principle

The ESP32 continuously monitors the SOS button.

When the button is pressed, the emergency mode is activated.

The buzzer starts producing an alarm.

The LED starts blinking.

The GPS module provides the current coordinates.

The ESP32 creates an emergency message containing the location.

The GSM module sends the SMS to the predefined emergency contact.

The device continues indicating emergency mode until it is reset.

Example Emergency Message
EMERGENCY ALERT!

SOS button activated.

Location:
Latitude: 15.8281
Longitude: 78.0373

Google Maps:
https://maps.google.com/?q=15.8281,78.0373


The coordinates above are only an example.

Test Cases
Test	Input	Expected Result
T01	Power ON	Device initializes
T02	SOS not pressed	Normal monitoring
T03	SOS pressed	Emergency mode activated
T04	SOS pressed + GPS available	Location obtained
T05	SOS pressed + GSM available	SMS sent
T06	SOS pressed + GPS unavailable	Emergency mode continues
T07	SOS pressed + GSM unavailable	Local alarm continues
T08	Multiple SOS presses	Device remains in emergency state
Simulation

The project can be simulated by representing the ESP32 inputs and outputs and replacing physical GPS/GSM hardware with simulated serial data.

The simulation should verify:

SOS button detection

Buzzer activation

LED activation

GPS coordinate processing

Emergency message generation

System response when GPS data is unavailable

Project Advantages

Compact emergency device

Real-time location information

Automatic emergency notification

Simple user interaction

Low-cost prototype

Can be extended with additional IoT features

Future Improvements

Possible extensions include:

Mobile application

Cloud-based location monitoring

Fall detection

Accelerometer-based abnormal movement detection

Voice activation

Long-press SOS activation

Battery monitoring

Multiple emergency contacts

Live location tracking

Geofencing

Limitations

This prototype depends on GPS availability and cellular network availability. GPS accuracy can vary depending on environmental conditions, and GSM communication may not work where cellular coverage is unavailable.

This project is intended as an educational prototype and should not be considered a guaranteed emergency-response system.

Author

Women Safety IoT Device Project

Built using ESP32, GPS, GSM and embedded IoT technologies.