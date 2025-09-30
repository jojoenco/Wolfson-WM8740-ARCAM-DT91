# Wolfson-WM8740-ARCAM-DT91

The Arcam DT91 is a Dab/FM radio from Camebridge.
Now in the hands of the brand Harman which is owned by Samsung.

The Arcam DT91 is about 20 years old, and works fine except DAB (Not DAB+) is not supported anymore. (in the Netherlands)
And it was standing there doing nothing.
Then I thought the sound from the DA-Converter (DAC WM8740) was always good when playing DAB radio.
Is it maybe possible to use the DA-Converter with something else. (just for the fun of it)

I use a Raspberry-Pi for PiCorePlayer and that works great.
It is also possible to use the PiCorePlayer with an external DAC connected to the USB of the Raspberry-Pi.

I opened up the Arcam Radio and checked if I could connect something to the internal DAC-Chip to make it an external DAC.  
And it was easier then I tought.


I looked up the Data sheet of the WM8740 and found that it had an I2S option witch you can connect to an USB to I2S converter.  
For the test I used the PCM2706 (a complete PCB), USB in I2S out, Bought online.  

<img width="337" height="204" alt="PCM2706small" src="https://github.com/user-attachments/assets/6a126723-f22f-49b6-acd4-2d51f1e12f6c" />  

Inside the Arcam was a white connection with the connections I needed to connect to the PCM2706.  

<img width="353" height="274" alt="PCM2706small" src="https://github.com/user-attachments/assets/11a59549-b229-4caa-82a3-e23b5c66f8bd" />

CON402 Has 6 connections with the arrow as nr1.
1 dont use
2 BCK
3 DATA
4 LCK
5 SCK
6 GND
