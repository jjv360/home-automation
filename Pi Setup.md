
# Resources

- https://bartsimons.me/raspberry-pi-kiosk-tutorial/

# Prepare hardware

- Plug the screen on top of the Pi
- Make sure the HDMI bridge plug is connected
- Connect a USB keyboard to the Pi
- Connect the Pi to LAN
- Make sure to have a Micro SD card 8GB or bigger ready

# Flash the OS

- Download the [Rasbian Lite image](https://www.raspberrypi.org/downloads/raspbian/).
- Flash it onto the SD card using [Etcher](https://www.balena.io/etcher/).
- Put the SD card into the Pi, then connect the Pi to power.
- Once it's booted and you see `raspberry login:`, enter the username `pi`, and password `raspberry`.

# Install dependent software

Run these commands _(this could take a while)_

```
sudo apt update
sudo apt install xserver-xorg xinit chromium-browser
sudo apt upgrade
```

Configure x11 by running this and selecting `Anyone`

```
sudo dpkg-reconfigure x11-common
```

# Install our software

copy to /home/pi/app

# Configure x11

Create `~/.xinitrc` file:

```
xset s off
xset -dpms
xset s noblank
chromium-browser
