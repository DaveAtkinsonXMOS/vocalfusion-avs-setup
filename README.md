# xCORE VocalFusion Kits for Amazon AVS on a Raspberry Pi

This repository provides a simple-to-use automated script to install the Amazon AVS SDK on a Raspberry Pi and configure the Raspberry Pi to use the **xCORE VocalFusion Kits for Amazon AVS**.

The XMOS **xCORE VocalFusion Kits for Amazon AVS** provide far-field voice capture using the XMOS XVF3100, XVF3500, and XVF3510 voice processors.

Combined with a Raspberry Pi running the Amazon Alexa Voice Service (AVS) Software Development Kit (SDK), these kits allow you to quickly prototype and evaluate talking with Alexa.

To find out more, visit: https://www.xmos.ai/vocalfusion-voice-interfaces/ (XVF3510/3500)  
or https://www.xmos.ai/vocalfusion-conference-calling/ (XVF3100)  
and: https://developer.amazon.com/alexa-voice-service

## Prerequisites
You will need:

- Either

   **xCORE VocalFusion XVF3510 Kit for Amazon AVS**: XK-VF3510-L71, or  
   **xCORE VocalFusion Stereo 4-Mic Kit for Amazon AVS**: XK-VF3500-L33-AVS, or  
   **xCORE VocalFusion 4-Mic Kit for Amazon AVS**: XK-VF3000-L33-AVS

- Either

   Raspberry Pi 3 with Micro-USB power supply (min. 2A) and HDMI cable, or  
   Raspberry Pi 4 with USB-C power supply (min. 3A) and Micro HDMI to Standard HDMI (A/M) Cable

- MicroSD card (min. 16GB)
- Powered speakers with audio 3.5mm analogue plug

   Stereo for the XVF3510 and XVF3500, or  
   Mono for the XVF3100
   
- Monitor with HDMI input
- USB keyboard and mouse
- Fast-Ethernet connection or WiFi with internet connectivity

You will also need an Amazon Developer account: https://developer.amazon.com

## Hardware Setup
Set up your hardware by following the **Hardware Setup Guide** for your product.

   XVF3510: https://www.xmos.ai/file/xvf3510-dev-kit-setup-guides  
   XVF3500: https://www.xmos.ai/file/xvf3500-dev-kit-setup-guides  
   XVF3100: https://www.xmos.ai/file/xvf3000-3100-dev-kit-setup-guides  

## Firmware Upgrade
Once the hardware is setup, upgrade the firmware on your AVS development kit. The firmware can be found here:  

   XVF3510: https://www.xmos.ai/file/xvf3510-int-release  
   XVF3500: https://www.xmos.ai/file/vocalfusion-stereo-evaluation-binaries  
   XVF3100: https://www.xmos.ai/file/vocalfusion-speaker-evaluation-binaries  
   
To upgrage the firmware you will need the XMOS xTAG adapter https://www.xmos.ai/xtag-debug-adapter/

## Create a Raspberry Pi system disk
Install the Raspberry Pi Imager on a host computer, and install Raspberry Pi OS (32-bit). Raspberry Pi Imager is available here: https://www.raspberrypi.org/software/

## AVS SDK installation and Raspberry Pi audio setup
The **Getting Started Guide** for your platform details setup steps up to this point. What follows are the steps specific to setting up the AVS SDK.

1. Boot the Raspberry Pi from the SD card, and follow the instructions to set up your locale, connect to WiFi, and update the system.

2. Reboot the system to ensure the latest kernel is running.

3. Open a terminal window on the Raspberry Pi desktop and clone the vocalfusion-avs-setup repository:

   ```git clone https://github.com/xmos/vocalfusion-avs-setup```

4. Register an AVS product, create a security profile and save a *config.json* file by following https://developer.amazon.com/en-US/docs/alexa/alexa-voice-service/register-a-product.html. It is strongly recommended that the config.json file should be saved onto a USB memory stick for future use.

5. Close the browser and any other applications to avoid the Raspberry Pi freezing during the AVS SDK installation.

6. Copy the *config.json* from the location it was saved to in step 4. into the directory `vocalfusion-avs-setup`

7. Run the installation script by entering:

   ``` cd vocalfusion-avs-setup```

   And then either
   
   XVF3510: ```./auto_install.sh xvf3510```  
   XVF3500: ```./auto_install.sh xvf3500```  
   XVF3100: ```./auto_install.sh xvf3100```

   Read and accept the AVS Device SDK license agreement.

8. You will be asked whether you want the Sample App to run automatically when the Raspberry Pi boots. It is recommended that you respond "yes" to this option.

9. Read and accept the Sensory license agreement. Wait for the script to complete the installation. The script is configuring the Raspberry Pi audio system, downloading and updating dependencies, building and configuring the AVS Device SDK. It takes around 30 minutes to complete.

10. Enter `sudo reboot` to reboot the Raspberry Pi and complete the installation.

11. If you selected the option to run the Sample App on boot you should now be able to complete the registration by following the instructions on the screen, although you may need to scroll back to see them. A code will be printed on the screen, and you will be prompted to visit https://amazon.com/us/code, log in to your developer account, and enter the code when prompted.

12. Now you can execute an AVS command such as "Alexa, what time is it?".

   On the XMOS **xCORE VocalFusion XVF3510 Kit for Amazon AVS**, the LED on the Pi HAT board will change colour when the system hears the "Alexa" keyword, and will then cycle back and forth whilst waiting for a response from the Amazon AVS server.

   On the XMOS **xCORE VocalFusion Stereo 4-Mic Kit for Amazon AVS** and **xCORE VocalFusion 4-Mic Kit for Amazon AVS**, the LEDs on the development board should reflect the approximate direction from which the microphones are receiving a stimulus.

## Running the AVS SDK Sample App
The automated installation script creates a number of aliases which can be used to execute the AVS Device SDK client, or run the unit tests:
- `avsrun` to run the Sample App.

## Changing Sensory operating point

To change to operating point of the Sensory keyword engine, edit the shell script run by the `avsrun` alias: 

   `~/sdk-folder/avs-device-sdk/tools/Install/.avsrun-startup.sh`
   
and change the third argument to SampleApp from the default value of `12` to the desired value.
