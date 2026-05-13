# Home-Assistantant-Voice-Satellite-with-ESP32-C61-WROOM1
This project uses the Espressif ESP32-C61-WROOM1-DevKitC-1-N8R2 Development Board 
with Max98357A Amplifier, INMP441 digital microphone and a 4-ohm speaker to create a Voice Assist Satellite for Home Assistant using ESPHome Builder.

The ESP32-C61 has 2MB Prasm, supports WiFi-6 and uses much less power compared to ESP32-S3.
(My other project using Xaio ESP32-C6 without Prasm works, but doesn't support media player while this setup does. Both C6 and C61 have only 1 I2S bus, so speaker and mic share the bus and can't listen while playing or play while listening.)

COMPONENTS:
Espressif ESP32-C61-WROOM1-DevKitC-1 (Amazon ASIN B0F8HTHXWS)

INMP441 Omnidirectional I2S Microphone Module MEMS, high precision, low power, supports ESP32 (Amazon ASIN B0FBWQF74T or equivalent)

MAX98357 I2S Audio Amplifier Module, Class D (Amazon ASIN B096ZM9LL5 or equivalent)

4 Ohm 3 Watt Mini Speaker (Amazon ASIN B0BTP67F81 or equivalent; 8 ohm will also work, lower peak volume)

Optional: LED and 1K resistor (or for brighter, 330ohm resistor)

```
Phyiscal Connections:
INMP441   ---   ESP32-C61
VDD -----------  3V3
GND ------------ GND
SD  ------------ GPIO9   (I2S data)
WS  ------------ GPIO3   (I2S word select)
SCK ------------ GPIO2   (I2S bit clock)
L/R ------------ GND      (Left channel)

MAX98357A -----  ESP32-C61
VIN -----------  5V
GND -----------  GND
DIN -----------  GPIO25  (I2S data)
LRC -----------  GPIO3   (shared with INMP441 WS)
BCLK-----------  GPIO2   (shared with INMP441 SCK)
SD  -----------  Floating
GAIN-----------  Floating (9db gain)

Optional External LED
1K Resistor ---> GPIO24
1K Resistor ---> LED Anode
GND  ----------> LED Cathode
```
<img width="874" height="532" alt="image" src="https://github.com/user-attachments/assets/016d1744-1072-475d-8211-098093124f58" />
<img width="395" height="501" alt="image" src="https://github.com/user-attachments/assets/d6258eb4-6e67-4813-a5f9-c3e10f27aa97" /> <img width="1078" height="843" alt="image" src="https://github.com/user-attachments/assets/7643e3ad-5125-48dd-8c39-51f3ec661e5a" />
(above - from bottom, first rail (-) is GND   2nd (+) is shared clock/GPIO2; third row up connect Mic data (SD)/GPIO9, and Spkr data (DIN)/GPIO25
 above the ESP from left is GND, 5V, GPIO3, GPIO2, and 3V3; top rail is to share GPIO3 to LRC on the Max and WS on the Mic
 I used a 2K resistor to the blue LED.
 below - the mic is really good & has great sensitivity and low noise)<br>
 <img width="191" height="514" alt="image" src="https://github.com/user-attachments/assets/1dce4366-2dc7-413d-ba61-4152b70b9b29" />

 <b>NOTE:</b>
 Initialization of a new board <i>could not be completed using either ESPHome Builder or web.esphome.io</i> - There is (timing?) issue preventing connection/handshake. 
 To get the device setup, I had to build the firmware using the Manual option and save the .bin file to disk, then flash using python with:
 ```
 py -3 -m esptool --port [COM##] --baud 460800 --chip esp32c61 write-flash 0x0 [c:\filefolder\devicename.factory.bin]
 ```
 After flashing manually, subsequent flash can be done wirelessly (and still unable to use USB for logs or flashing).

 
 


