# Raspberry Pi LED Matrix Playground

This is a collection of widgets and helpers to drive a LED matrix of any size created with WS2812B LED strips. 

### Hardware

Here is the high level construction details of the LED matrix panel.

Shopping List:
* WS2812B LED strips
* 5V power supply
* Rasperry Pi 4
* Extra 3 pin wire @ 22AWG
* Extra JST SM 3 Pin Connectors for extention to where your panel is from the Pi/PSU
* A bit of patience -- Takes about 4-5 hours to put it all together
* Curtain rod
* Hobby wood/bamboo @ 3/8" wide to stick on the back of the LED strips to keep them straight

In this example I built a 60x30 array with 5V 300W 60A power supply:
1. Collect a 60 count of 30 LED per meter 1M strips
2. Build the matrix in a chain pattern:
```
_   _   _   _ ...
 | | | | | |
 | | | | | |
 | | | | | |
 | | | | | |
 | | | | | |
 |_| |_| |_|
```
3. Attach power to every other strip in parallel

4. Connect GPIO 18 of the RPi4 to the green LED wire
5. Connect GND pin of the RPi4 to COM of the power supply
6. Hang the LED strips to the curtain rod with your adhesive of choice
7. Stick the wood to the back of the strips

### Pi setup
1. Install RPi OS 32 bit
2. Execute the following to globally install libraries and dependicies:
```
sudo apt update
sudo apt install -y ffmpeg
sudo pip3 install --upgrade adafruit-python-shell
wget https://raw.githubusercontent.com/adafruit/Raspberry-Pi-Installer-Scripts/master/raspi-blinka.py
sudo python3 raspi-blinka.py
sudo pip3 install rpi_ws281x adafruit-circuitpython-neopixel
sudo python3 -m pip install --force-reinstall adafruit-blinka
```
3. Update the `config.py` to adjust sizes, delays, and pin configuration.

## Test hardware
Running the test script will cycle between R..., G..., B...
```
sudo python3 test.py
```

## Playing videos
To play a video to ensure good performance resize the video before playing with ffmpg: 
```
ffmpeg -i filename.mp4 -vf scale=60:30 filename-60x30.mp4
```
To play the video on the matrix:
```
sudo python3 video.py filename.mp4
```

## Displaying an image
Reize the image in any graphic editor to the size of the matrix and save it as a PNG.
```
sudo python3 image.py image.png
```

## Scrolling Marquee
```
sudo python3 marquee.py 'Message Here'
```

## Contributing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md)

---

Created by [@natelewis](https://github.com/natelewis). Released under the MIT license.

