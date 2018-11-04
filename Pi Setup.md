
# Resources

- https://bartsimons.me/raspberry-pi-kiosk-tutorial/
- https://www.waveshare.com/wiki/5inch_HDMI_LCD

# Prepare hardware

- Plug the screen on top of the Pi
- Make sure the HDMI bridge plug is connected
- Connect a USB keyboard to the Pi
- Connect the Pi to LAN
- Make sure to have a Micro SD card 8GB or bigger ready

# Flash the OS

> You should connect both the Pi's power and the one on the screen, to prevent it getting underpowered. If you see the yellow electricity icon in the top-right of the screen, the Pi is not getting enough power and may corrupt data.

- Download the [Rasbian Lite image](https://www.raspberrypi.org/downloads/raspbian/).
- Flash it onto the SD card using [Etcher](https://www.balena.io/etcher/).
- Copy the [LCD driver](https://www.waveshare.com/wiki/5inch_HDMI_LCD) .tar.gz for Raspbian Lite onto the card.
- Put the SD card into the Pi, then connect the Pi to power.
- Once it's booted and you see `raspberry login:`, enter the username `pi`, and password `raspberry`.

# Configure OS to login automatically

Run `sudo raspi-config` and then choose Boot Options > Desktop / CLI > Console Autologin.

# Install dependent software

Run these commands _(this could take a while)_

```
sudo apt update
sudo apt install xserver-xorg xinit chromium-browser git
sudo apt upgrade
```

# Setup LCD panel

To fix the LCD's offset sizing, run `sudo nano /boot/config.txt` and add this to the end of the file:

```
hdmi_group=2
hdmi_mode=87
hdmi_cvt 800 480 60 6 0 0 0
hdmi_drive=1
```

> Press Ctrl+X to exit nano after you're done editing, and then press Y and Enter to save changes.

Reboot by entering `sudo reboot now`.

# Install our software

Install our app to `/home/pi/home-automation` by running:

```
git clone https://github.com/jjv360/home-automation.git
```

# Configure the OS to launch our app on startup

Create ~/.xinitrc file by running `nano ~/.xinitrc` and then make it look like this:

```
xset s off
xset -dpms
xset s noblank
chromium-browser --window-size=800,480 --kiosk http://localhost:8080
```
