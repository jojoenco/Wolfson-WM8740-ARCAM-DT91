# Wolfson-WM8740-ARCAM-DT91

The Arcam DT91 is a Dab/FM radio from Camebridge.
Now in the hands of the brand Harman which is owned by Samsung.

The Arcam DT91 is about 20 years old, and works fine except DAB (Not DAB+) is not supported anymore. (in the Netherlands)  
And it was standing there doing nothing.  
Then I thought the sound from the DA-Converter (DAC WM8740) was always good when playing DAB radio.  
Is it maybe possible to use the DA-Converter with something else. (just for the fun of it)  

## make an external DAC from the Arcam DT91  

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
1 (dont use)  
2 BCK  
3 DATA  
4 LCK  
5 SCK  
6 GND  

The PCM2706 PCB has also the same connections on the right side.  
But I dont use the 5V connection, it gets power from the USB connection connected to the Pi.

But it didn´t work directly.  
The WM8740 had to be set on I2S mode.  
So I lift up to legs of the chip that needed to be set on High and conneted them to 5V, that is Nr 23 and 28 of the chip.  

![WM8740-I2S](https://github.com/user-attachments/assets/1c8aba13-b08c-43ed-beb6-f2c2f4c40fbd)  

Then I removed the DAB antenne signal print with the DSP DRE200P tuner chip, may otherwise interfere with the digital signal.  

Then i setup the raspberry-pi with Picoreplayer and connected the micro-usb to the pi.  
https://www.picoreplayer.org/  

![pi-connected to test-small](https://github.com/user-attachments/assets/521228bd-16ea-4a66-b6c3-a27b753b3a98)

I tested it on small computer speakers and it works, and the sound was good.  

## fluorescent screen

The DT91 also has an Fluorescent screen and I tought maybe I can use it to display the song information, but I could not get it to display the right information, only stripes and loose letters or something like that.  
Maybe later I figure it out.  
### ST7789  
https://docs.picoreplayer.org/projects/add-a-1-54-inch-spi-display/  

Then I used a display already supported by PicorePlayer, that is a 1.5inch st7789 display, and fit it between the metal plate in the front and the button print.  
But in front of the display there is a orange kind of plastick glass, so the picture looks like a sepia photo.  
![ST7789sepia2](https://github.com/user-attachments/assets/8aa08a8b-3035-4fdd-bd69-6470b5ea34c5)  

# assamble everything inside  

Then I connected and soldered everything inside.  
![Pi3Binside2](https://github.com/user-attachments/assets/9646cf67-2f54-400e-9180-57d34795dd77)  

# Terrible sound
And then I connected it to the Amplifier, and tested the sound.  
It was terrible cracks and clicks and pops in the sound, and I tought what can it be I only connected a screen and assembled everyting together.  
So I chanced the power supply (and tested), disconnected the screen (and tested), cut the data lines on the PCB comming from tghe other side of the mainboard (and tested).  
![Data lines cut](https://github.com/user-attachments/assets/42ae6c08-da84-4e87-886f-0735188ae50e)  

Nothing worked.







