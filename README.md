# Wolfson-WM8740-ARCAM-DT91

The Arcam DT91 is a Dab/FM radio from Cambridge.
Now in the hands of the brand Harman which is currently owned by Samsung.

The Arcam DT91 is about 20 years old, and works fine except that DAB (Not DAB+) is not supported anymore (in the Netherlands).  
And it was sitting around collecting dust.  
Then I thought the sound from the DA-Converter (DAC WM8740) was always good when playing DAB radio.  
Would it be possible to use the DA-Converter with something else instead? (just for the fun of it)  

## Make an external DAC from the Arcam DT91  

I use a Raspberry-Pi for PiCorePlayer and that works great.  
It is also possible to use the PiCorePlayer with an external DAC connected to the USB of the Raspberry-Pi.

I opened up the Arcam Radio and checked if I could connect something to the internal DAC-Chip to make it an external DAC.  
And it was easier then I thought.

I looked up the datasheet of the WM8740 and found that it had an I2S option which you can connect to an USB to I2S converter.  
For testing purposes, I used the PCM2706 (a complete PCB) which does USB in, I2S out, bought online.  

<img width="337" height="204" alt="PCM2706small" src="https://github.com/user-attachments/assets/6a126723-f22f-49b6-acd4-2d51f1e12f6c" />  

Inside the Arcam was a white connector (CON402) with the connections I needed to connect to the PCM2706.  

<img width="353" height="274" alt="PCM2706small" src="https://github.com/user-attachments/assets/11a59549-b229-4caa-82a3-e23b5c66f8bd" />

CON402 Has 6 connections with the arrow as pin 1.  
1. (dont use)  
2. BCK  
3. DATA  
4. LCK  
5. SCK  
6. GND  

The PCM2706 PCB also has the same connections on the right side.  
But I don´t use the 5V connection, it gets power from the USB connection connected to the Pi.

But it didn´t work directly.  
The WM8740 had to be set to I2S mode.  
So I lifted up the pins of the chip that needed to be set on high and connected them to 5V, that is pin 23 and 28 of the chip.  

![WM8740-I2S](https://github.com/user-attachments/assets/1c8aba13-b08c-43ed-beb6-f2c2f4c40fbd)  

Then I removed the DAB receiver module with the DSP DRE200P tuner chip, otherwise it may interfere with the digital signal.  
![dab-tuner](https://github.com/user-attachments/assets/32016f2c-5239-48c1-b17a-cf427f79800f)

Then I setup the Raspberry Pi with piCorePlayer and connected the micro-usb to the pi.  
https://www.picoreplayer.org/  

![pi-connected to test-small](https://github.com/user-attachments/assets/521228bd-16ea-4a66-b6c3-a27b753b3a98)

I tested it on some small computer speakers and it works, and the sound was good.  

## Fluorescent screen

The DT91 also has a Fluorescent screen and I thought maybe I can use it to display the song information, but I could not get it to display the right information, only stripes and loose letters or something like that.  
Maybe I can figure it out later.  
### ST7789  
https://docs.picoreplayer.org/projects/add-a-1-54-inch-spi-display/  

Then I used a display already supported by piCorePlayer, that is a 1.5inch ST7789 display, and fit it between the metal plate in the front and the button PCB.  
But in front of the display there is a orange kind of plastic glass, so the picture looks like a sepia photo.  
![ST7789sepia2](https://github.com/user-attachments/assets/8aa08a8b-3035-4fdd-bd69-6470b5ea34c5)  

# Assembling everything inside  

Then I connected and soldered everything inside.  
![Pi3Binside2](https://github.com/user-attachments/assets/9646cf67-2f54-400e-9180-57d34795dd77)  

# Terrible sound
And then I connected it to the Amplifier, and tested the sound.  
There were terrible cracks, clicks and pops in the sound, and I thought what might be the cause, I only connected a screen and assembled everything together.  
So I swapped the power supply (and tested), disconnected the screen (and tested), cut the data lines on the PCB comming from the other side of the mainboard (and tested).  
![Data lines cut2](https://github.com/user-attachments/assets/2af120b7-073e-4733-ad51-c31b9c964296)


Nothing worked.  
Then I changed the Raspberry Pi from a 3B to a 4. (and I tested it)  
Still not solved.  
Pffffff.....  
## Solved
Then I thought the only thing that I did not change is the ribbon-cable between the PCM2706 and the WM8740.  
I swapped it for an audio cable with shielding, and that changed everyting. :blush:  
![shieldingCable](https://github.com/user-attachments/assets/00f5232b-c78b-4a7e-be74-f96fb7269937)  
Perfect and clean sound, looks like the folded ribbon cable picked up digital noise.  

## PCM2706  
The USB to I2S converter, is a €5,- simple converter max 16bits 48Khz.  
There are better (meaning higher specs, don´t know if it sounds better, have not tried it yet) models like the CT7601 or something like that, they can be set to 24bits 192Khz, which I will test later.  

#  Buttons and rotary  
https://docs.picoreplayer.org/projects/control-jivelite-by-rotary-encoders-and-buttons/  
The front of the DT91 also has a rotary knob and some buttons.  
I took off the white ribbon cable from the front PCB to the main PCB because of the voltage on the print (22 Volt to the fluorescent display), to prevent it from going to the Raspberry Pi and damage it.  
Then I desoldered the SMD resistors on the front PCB close to the rotary and the buttons I wanted to use, and soldered some cables to the back contacts of the buttons and the rotary, and connected it to the Raspberry Pi, and followed the description on the site from raspberry pi jivelite rotary encoders and buttons, But that did not work, got an error.  
Then I asked my son he looked at the script and changed some things, then I tried it again and it worked, but turning was the other way around, asked my son again and solved.  
So my advice is if it doesn´t work, ask your son. :blush:  

## WiFi  
When you close the DT91 the raspberryPi has no WiFi anymore, the case of the Dab radio is almost completely from matal (Faraday cage), when you need WiFi then you have to move the antanna outside of the case.  
![antanna](https://github.com/user-attachments/assets/f352ee55-c219-4e03-ba5c-3701b61d0d50)

## USB Back  
Sometimes you need to complete something with the mouse on the pi, and you can open the case every time and connedct a mouse, but with the Tuner PCB removed there is a hole to connect the USB extension cable so you can connect a mouse on the outside.  
![USB Cable](https://github.com/user-attachments/assets/b8e5319e-78d7-4b7a-9523-7a96db041083)
![USB Hole2](https://github.com/user-attachments/assets/e7316b34-3042-4557-b929-f85be1720e9a)



# In short:  
Open DT91 find White connector next to the  






 




