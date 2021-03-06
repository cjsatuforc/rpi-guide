# Setup
The following sections explain the required steps to prepare the PC/Mac and the Raspberry Pi

## Table of Contents   
### 1.   [Preparing the Raspberry Pi SD card](#sdcard)
### 2.   [Initiating the RPi](#sdcard)
#### a.         [Running the Raspberry Pi with a monitor](#rpi_monitor)
#### b.         [Running the Raspberry Pi headless](#rpi_headless)
### 3.   [Remote access to Raspberry Pi](#remote) 

<a name="sdcard"/>


## Preparing the Raspberry Pi SD card
1.  Download Raspbian OS image from https://www.raspberrypi.org/downloads/raspbian/
2.  Burn it to the SD card using DiskImager https://sourceforge.net/projects/win32diskimager/

<a name="rpi_monitor"/>

## Initiating the RPi
### Running the Raspberry Pi with a monitor
1.	Connect the RPi to a monitor, mouse, keyboard, and start the RPi
2.	From the network icon on the desktop toolbar connect to a WiFi network
3.	Open Terminal
4.	Run ifconfig to find the RPi’s IP address

<a name="rpi_headless"/>

### Running Raspberry Pi Headless (without a monitor)
This section will only work if you burned Raspbian onto the SD card, and may not work if you started with Noobs (the OS already burned on the SD card that comes with the RPi)
1.	Plug the SD card reader into your computer
2.	Open the cmdline.txt file on the main root of the SD card and append the following
```
ip=192.168.100.200::192.168.100.1:255.255.255.0:rpi:eth0:off
```
Where `192.168.100.200` is the *IP address*, `192.168.100.1` is the *network gateway*, and `255.255.255.0` is the *network mask*. You are free to change the IP address to any value as long as you choose one on the same subnet at the you set your computer to in Step 8

3.  Plug the SD card back into the RPi, then connect the RPi to your computer using an ethernet cable

4.  Right-click the network icon on your computer's toolbar and choose "Network and Sharing Center"
5.  From the side menu, choose **Change adapter settings**
6.  Right-click the **Ethernet** network adapter, and choose **Properties**
7.  In the scroll-down menu, choose **Internet Protocol Version 4 (TCP/IPv4)** and select **Properties**
8.  Select **Use the following IP address**, and set the *IP* to `192.168.100.201`, *subnet mask* to `255.255.255.0`, and *default gateway* to `192.168.100.1`

Finally, test the conneciton by opening **Windows Command Line** and typing in
```
ping 192.168.100.200
```

<a name="remote"/>
         
## Accessing the RPi remotely
### Connecting through SSH
1. Download an SSH client on your Windows machine such as PuTTY (http://www.putty.org/)

2.  Type in the PI address of the RPi that you acquired in Step 4 of [Running the Raspberry Pi with a monitor](#rpi_monitor) or Step 2 of [Running Raspberry Pi Headless](#rpi_headless)

![Screenshot](/images/putty.png?raw=true "Login")

3.  Enter raspberry when asked for the password

![Screenshot](/images/puttylogin.png?raw=true "Login")

4.  You now have access to the Pi through its terminal
P.S. If you get a "refused to connect" message, take the SD card out of the RPi and plug it into your SD reader, then on the main root creat an empty file and call it "ssh" with not format. Plug the SD card back into the RPi and it should work.

### Accessing the graphical interface remotely through VNC

### PC
Install VNC viewer from https://www.realvnc.com/en/connect/download/viewer/

### Raspberry Pi
#### Download realVNC
Once you've established an SSH connection through Putty, type in
```
sudo apt-get update
sudo apt-get install realvnc-vnc-server realvnc-vnc-viewer
```
#### Enable VNC
1. Run the following command
```
sudo raspi-config
```
![Screenshot](/images/vncallow.png?raw=true "Login")

2. Navigate to **Interfacing Options**, then scroll down and select **VNC > Yes**.

![Screenshot](/images/vncallow3.PNG?raw=true "Login")

3. Restart
```
sudo reboot
```

### Usage
1. Open VNCViewer on your computer, and type the IP address of the Raspberry Pi that you acquired in Step 4 of [Running the Raspberry Pi with a monitor](#rpi_monitor) or Step 2 of [Running Raspberry Pi Headless](#rpi_headless) followed by port `5900` e.g. `192.168.100.200:5900`
2. Enter the Raspberry Pi’s username and password to access the RPi's desktop

![Screenshot](/images/vncdesktop.png?raw=true "Login")
