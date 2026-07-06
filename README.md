# Soupypoopy - A silly soup created by lok out @fallout

Soup is fallout soul and we want to make a memory about it. That's why we created Soupypoopy, where Soup can dance, sing, and poop.

## Zine

## How to use

1.Put all your poopy experience inside soup.
2.Left ear button play a random song, right ear button to make soup dance. Watch soups' performance, forget your any kind of poopy experiene, and take the happiest memory to your home!
3.At a random time, soup will poop. Catch it if you can!!
4.Remember the precious experience you had in fallout:)

## How to make it : The Ultimate Building Guide
1. 3D Print & Assemble: Print all CAD components and snap-fit the housing together.

2. Mount Hardware: Secure the three MG90S servos into their designated slots; attach the poop tunnel to the designated output port.

3. Install Electronics: Mount the Seeed XIAO ESP32C3, PCA9685 driver, PAM8403 amplifier, and buck converter into the internal chassis mounts.

  1. Power: Connect the dual 18650 battery pack to the buck converter input; wire the converter output (set to 5V) to the red/blue breadboard rails or main power distribution.
  2. I2C Bus: Wire PCA9685 SDA and SCL to the ESP32-C3 SDA and SCL pins.
  3. Servos: Connect servo signal wires to the PCA9685 PWM output channels (0-2).
  4. Audio: Connect the PAM8403 L+/L- to the speaker and the Audio In to ESP32 Pin 5.

5. Firmware: Use PlatformIO to upload the "Ultimate Code" firmware to the ESP32-C3.

6. Final Integration: Verify all ground connections are common, close the chassis, and insert the batteries.

7. System Check: Power on, verify servo movement, and confirm audio output triggers via the button.



## Final Product
Check out [demo video](https://youtu.be/WR7H3MUDWkc)

## Schematic

<img width="889" height="601" alt="image" src="https://github.com/user-attachments/assets/79c3010b-7271-4639-87c0-a4a48dad1c8d" />


## CAD & Key mechanism
### The full body
<img width="970" height="602" alt="image" src="https://github.com/user-attachments/assets/848d41ed-1a23-4be2-875f-29d5cde9d061" />

This is the full body CAD of Soupypoopy. Now, lets explore how the three key mechanisms: <mark>1. pooping</mark>, <mark>2. dancing</mark> and <mark>singing </mark> works! 

### Pooping

https://github.com/user-attachments/assets/58249dca-2009-4cac-ab2c-7619b41a9ac4


For pooping, we use three CAD components -- poopshooter, poop, and pooping tunnel together with the MG90S motor. Specifically, through using the poopshooter as extension for the servo motor, and turning the servo by 45 degree when soup turns around for 5 time, we made the pooping mechanism.

### Dancing
We used two motors, with one for each arm. The MG90S motor is attached to the shoulder of soups body which has servo-shaped hole, and the servo horn is connected to the arm which has round shaped hole as same as depth of the servo horn. 
<img width="1170" height="762" alt="image" src="https://github.com/user-attachments/assets/4d7987b6-92b9-44a9-af8d-a9254fa1935d" />
<img width="1352" height="720" alt="image" src="https://github.com/user-attachments/assets/bb6de0bc-24ff-44f8-83cf-7499d1581787" />


### Singing
We attached the speaker inside the soup, and holded it by hot glue. 



## Firmware
Core Functionality - Performance Trigger: 
- Responds to a button press on the "Left Ear" pin (Pin 2).Motor Sequence: Initializes the DC motor flywheels (via Pin 6 and Pin 7) with a 1-second ramp-up delay to achieve target speed.Payload Deployment:- Triggers the relay-controlled solenoid (Pin 10) for a 250ms pulse while motors are at peak speed.Audio & Animation: Plays a randomized musical sequence (Mario or Tetris themes) through the SPEAKER_PIN (Pin 5) while simultaneously driving a servo motor (Pin 4) in a sweeping motion synchronized to the beat.
-  Pin AssignmentsComponentESP32-C3 PinPerformance Button2Servo Motor4Speaker (PAM8403)5DC Motor IN16DC Motor IN27Relay (Solenoid)
- LogicIdle State: The system sits in a low-power loop, monitoring the Left Ear button pin.
- Activation: Upon detecting a LOW signal (button press), the system enters the triggerPerformance() routine.
- Mechanical Execution:Motors spin up to launch velocity.Solenoid fires a single, timed pulse to deploy the payload.Motors stop.
- Audio/Visual Sequence: The system selects a random song array and iterates through frequency/duration data, generating tones while mapping servo angles to create a "dancing" effect.Return: Servo returns to center (90°) and the system returns to the idle state.
