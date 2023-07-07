# EGL315 TEAM D

# Introdution to our project
Welcome to Zombie Universe! In this exciting IR game, you'll find yourself in a post-apocalyptic world overrun by zombies. It's up to you, armed with an infrared sensor equipment, to withstand the zombie assault and discover a way out. Prepare for a thrilling, heart-pounding journey!

# Storyboard
![Alt text](images/storyboard.jpeg)

# System Diagrams
 ## Control Diagram
![Alt text](images/Control%20System.jpg)

## Audio Diagram
![Alt text](images/Audio%20Diagram.png)

## Video Diagram
![Alt text](images/video%20diagram.png)

## Lighting Diagram
![Alt text](images/lighting%20diagram.png)


# Equipment List
![Alt text](images/BOM.png)

# Floor Plan
![Alt text](images/Floor%20Plan%201.jpg)
![Alt text](images/Floor%20Plan%202.jpg)

# Lay0ut And Setup

## Connection & Remote

![Alt text](images/Remote.jpg)

## Screen Set-Up
![Alt text](images/Screen.jpg)

## IR Sensor Placement
![Alt text](images/IR%20Sensor.jpg)
Each IR Sensor respond to only 1 button . Power , 1 , 2,4 & 5.  

## Audio Setup
![Alt text](images/3.5mm%20Cable%20made%20finish%20for%20315.jpg)
Finish soldering of 3.5mm cable which will be connected to the amplifier.

![Alt text](images/Amplifier%20Setup%20for%20315.jpg)
Amplifier setup at the back of the screen and connected to the 2 passive speakers.

## IR System Code

```
import RPi.GPIO as GPIO
import time
# Set up GPIO mode and pin
GPIO.setmode(GPIO.BCM)
IR_PIN1 = 17  # Power button
IR_PIN2 = 27  # Number 1 button
IR_PIN3 = 22  # Number 2 button
IR_PIN4 = 25  # Number 4 button
IR_PIN5 = 24  # Number 5 button

GPIO.setup(IR_PIN1, GPIO.IN, pull_up_down=GPIO.PUD_DOWN)
GPIO.setup(IR_PIN2, GPIO.IN, pull_up_down=GPIO.PUD_DOWN)
GPIO.setup(IR_PIN3, GPIO.IN, pull_up_down=GPIO.PUD_DOWN)
GPIO.setup(IR_PIN4, GPIO.IN, pull_up_down=GPIO.PUD_DOWN)
GPIO.setup(IR_PIN5, GPIO.IN, pull_up_down=GPIO.PUD_DOWN)

```
Broadcom SOC channel numbering is the GPIO mode that is set by this line.These lines assign GPIO pin numbers to each button. Check that these pin numbers correspond to the actual connectors on your Raspberry Pi. The GPIO pins are configured as inputs with pull-down resistors using these lines. This guarantees that when the buttons are not pushed, the input is pulled low (GND).

```
# Button names
BUTTON_NAMES = {    
	IR_PIN1: "Power button",
	IR_PIN2: "Number 1 button",    
	IR_PIN3: "Number 2 button",
	IR_PIN4: "Number 4 button",   
	IR_PIN5: "Number 5 button",
}
try:    # Main loop to continuously read IR signals
    while True:        
for pin, button_name in BUTTON_NAMES.items():
if GPIO.input(pin) == GPIO.LOW:                
print(f"Signal received from {button_name}")
        # Delay between readings
        time.sleep(0.1)
# Gracefully handle a KeyboardInterrupt (Ctrl+C)
except KeyboardInterrupt:
    pass
# Clean up resources
GPIO.cleanup()

```

The GPIO pin numbers are associated with human-readable names for each button in this dictionary.This is the main loop, which constantly reads the button states. It loops over the dictionary of 'BUTTON_NAMES', verifying the status of each button. If a button is pressed (GPIO input is LOW), a message identifying which button was pressed is printed. To reduce excessive CPU utilization, there is also a 0.1-second wait between measurements.