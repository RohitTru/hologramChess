This is a repo to house some code to display some pixels on the Crystalfontz CFA-10105 0V0 OLED transparent display using a raspberry pi


To install git on a raspberry Pi
```bash
sudo apt update
sudo apt install git
```

For our display we are going to be using SPI so we need to enable SPI on the raspberrypi:
It shouldnt be on by default but you can check to see if you have SPI eneable by running the following command:
```bash
lsmod | grep spi
```

To enable it run
```bash
sudo raspi-config nonint do_spi 0
```
Now reboot the system
```bash
sudo reboot
```
Now lets run some commands to check to see if spi is enabled:
```bash
lsmod | grep spi && echo "---" && ls -l /dev/spi* && echo "---" && dmesg | grep spi
```

output should look something like the following;
```bash
crw-rw---- 1 root spi 153, 0 Mar  8 02:04 /dev/spidev0.0
crw-rw---- 1 root spi 153, 1 Mar  8 02:04 /dev/spidev0.1
```

Now, let's make sure you have the right permissions to use SPI. We should add your user to the 'spi' and 'gpio' groups:
```bash
sudo usermod -a -G spi,gpio $USER
```
| Display Pin | Name | Function | RPi Physical Pin | RPi GPIO# | Notes |
|------------|------|---------------|------------------|------------|--------|
| 1 | VCC | +3.3V Power | Pin 17 | - | Power pin |
| 2 | GND | Ground | Pin 20 | - | Ground pin |
| 3 | D0 | Clock (SCLK) | Pin 23 | GPIO 14 | SPI Clock |
| 4 | D1 | MOSI | Pin 19 | GPIO 12 | SPI Data |
| 5 | RST | Reset | Pin 31 | GPIO 22 | Reset line |
| 6 | DC | Data/Command | Pin 35 | GPIO 24 | Data/Command control |
| 7 | CS | Chip Select | Pin 24 | GPIO 10 | Chip Select |


