# U6143_ssd1306
## Preparation
```bash
sudo raspi-config
```
Choose Interface Options 
Enable i2c

##  Clone U6143_ssd1306 library in /opt
```bash
cd /opt
git clone https://github.com/UCTRONICS/U6143_ssd1306.git
```
## Compile 
```bash
cd U6143_ssd1306/C
```
```bash
sudo make clean && sudo make 
```
## Test run. CTRL+C to exit after verifying the display lights up
```
sudo ./display
```
## Add automatic start script using Systemd
- Create a new systemd file by opening it on Nano
```bash
sudo nano /etc/systemd/system/ucdisplay.service
```
- Add the following in ucdisplay.service
```bash
[Unit]
Description=ucdisplay
After=syslog.target network.target nss-lookup.target network-online.target

[Service]
User=0
Group=0
WorkingDirectory=/opt/U6143_ssd1306/C
ExecStart=/opt/U6143_ssd1306/C/display
RestartSec=5
Restart=on-failure

[Install]
WantedBy=multi-user.target
```
- Enable the display service 
```bash
sudo systemctl enable ucdisplay.service
```
- Start the display service 
```bash
sudo systemctl start ucdisplay.service
```
- The display should have come on. Check the display service status for issues
```bash
sudo systemctl status ucdisplay.service
```
- Reboot your system to ensure display starts at boot.

## For older 0.91 inch lcd without mcu 
- For the older version lcd without mcu controller, you can use python demo
- Install the dependent library files
```bash
sudo pip3 install adafruit-circuitpython-ssd1306
sudo apt-get install python3-pip
sudo apt-get install python3-pil
```
- Test demo 
```bash 
cd /home/pi/U6143_ssd1306/python 
sudo python3 ssd1306_stats.py
```

## Custom display temperature type 
- Open the U6143_ssd1306/C/ssd1306_i2c.h file. You can modify the value of the TEMPERATURE_TYPE variable to change the type of temperature displayed. (The default is Fahrenheit)
![EasyBehavior](https://github.com/UCTRONICS/pic/blob/master/OLED/select_temperature.jpg)


## Custom display IPADDRESS_TYPE type 
- Open the U6143_ssd1306/C/ssd1306_i2c.h file. You can modify the value of the IPADDRESS_TYPE variable to change the type of IP displayed. (The default is ETH0)
![EasyBehavior](https://github.com/UCTRONICS/pic/blob/master/OLED/select_ip.jpg)

## Custom display information 
- Open the U6143_ssd1306/C/ssd1306_i2c.h file. You can modify the value of the IP_SWITCH variable to determine whether to display the IP address or custom information. (The custom IP address is displayed by default)
![EasyBehavior](https://github.com/UCTRONICS/pic/blob/master/OLED/custom_display.jpg)





