# Burning Man 2022 Project

### Start the collector program
`python3 conversation_collector`

To auto run at boot (from usb-drive, or modify the script to run a local program):

Copy the `scripts/auto_run_from_usb.sh` to pi's `Desktop`

`cp -r /etc/xdg/lxsession ~/.config/` *only If you don't have ~/.config/lxsession already*

`nano ~/.config/lxsession/LXDE-pi/autostart`

Add `@lxterminal -e sh /home/milton/Desktop/auto_run_from_usb.sh`

### Set system default volume level

Set the volume level manually then run this: `sudo alsactl store`

--------------------------------------------------------

## Sculpture
fully assemble the sculpture
- button
- solar
- light (battery leds)

## Supporting Hardware
Install a collar on the base of the pole, round plate with holes where you can bolt it on the ground - people may knock it over

How to prevent this from being stolen

Modular design for swappable top solar panel but secure against wind etc.

## Gameday
Make sure power solution works - test outside for 3+ days

--------------------------------------------------------


## Notes

### Package Dependency 
- Stable OS: Raspberry Pi OS (32-bit) `Release 2022-04-04; installed with Raspberry Pi Imager v1.7.2`
- wave `sudo pip3 install wave`
- RPI.GPIO `sudo pip3 install RPi.GPIO`
- numpy `sudo pip3 install numpy`
- pydub `sudo pip3 install pydub`
- pyaudio `sudo pip3 install pyaudio`
- Rubberband `sudo apt-get install rubberband-cli && sudo pip3 install pyrubberband`
- BiblioPixel `sudo pip3 install bibliopixel`
- RPiWS281x `sudo pip3 install rpi_ws281x`
- ESPEAK-NG see below instructions:
  - `sudo apt install espeak-ng espeak-ng-data libespeak-ng-dev`
  - `sudo pip3 install py-espeak-ng`
  - Open /etc/modprobe.d/raspi-blacklist.conf and add blacklist snd_bcm2835
  - Open /lib/modprobe.d/aliases.conf and comment out the line options snd-usb-audio index=-2
  - sudo nano /boot/config.txt then comment out this line: dtparam=audio=on
  - sudo reboot. Then check with `aplay -l`

### Hard-wiring / Setup
- Make sure to update the hard-coded path in files_manager.py `ROOT_PATH` and create sub-directories
- Also updates `DEVICE_NAME` if you use a different speaker-mic than Jabra SPEAK 410

## Design
*Installation Design*
![hardware_design_diagram](./design/Installation&#32;Hardware&#32;Design&#32;v0.1.png)

*Software Design, but mostly outdated*
![design_diagram](./design/design.png)


--------------------------------------------------------
--------------------------------------------------------
--------------------------------------------------------
# Old notes below

## 6/5 BM art team requirements
- Hardware: install a collar on the base of the pole, round plate with holes where you can bolt it on the ground
- Hardware: make the entire pole well lit - use BATTERY powered LEDs

## Priorities
[Prio] until 5/31

### Software
- [MEDIUM][---] Sound sculptor - add different sound effects per hour in day / special for burn night etc.
- [MEDIUM][---] Breathing light POC: different patterns for different states. random brain dump:
  - playing: pulsing yellow
  - idle: glow white
  - recording: blinking green
  - acknowledging button pressed: red single pulse
- [LOW][---] Sound sculptor - make it cooler
- [LOW][---] UI/UX - add more ideas / poems to the Poet
### Hardware
- [HIGH][milton] Design & implement power solution - solar / batteries
  - Current bug: solar doesn't work :(
  - References
    - https://hive.burningman.org/posts/14167796
    - https://forums.raspberrypi.com/viewtopic.php?t=96544
    - https://howchoo.com/g/mmfkn2rhoth/raspberry-pi-solar-power
- [MEDIUM][---] Breathing light POC: single LED or LED strip
  - This looks cool
  - reference https://www.admfactory.com/breathing-light-led-on-raspberry-pi-using-python/
- [LOW][---] Make a robust and aesthetically pleasing shell
  - Ideally we can have some artist to do this
  - Directly out of wood? or 3D printed w/ heat-resistant materials?
- [LOW][---] Playa installation solution: Harsh environment
  - the whole thing needs to be resistant to STRONG wind / heat / rain
  - https://forums.raspberrypi.com/viewtopic.php?t=54812
  - https://forums.raspberrypi.com/viewtopic.php?f=63&t=44684
### Known bugs
- [MEDIUM][---] Raspberry Pi changes path to the USB device randomly sometimes, breaking run from usb drive function
  - 1) implement a more robust usb drive scanning logic
  - 2) failback to run from desktop files if usb not detected
### UX Improvements
- [MEDIUM][---] Raise voice UI volume to the same level of the playback volume
- [MEDIUM][---] Some people inclined to long press the button thinking they need to
  - with current logic this will continually spawn one recording session after another, which is not ideal
  - 1) make sure we don't record button press during recording time
  - 2) figure out a way to stop people from long pressing
### Production Checklist
- [todo] private beta indoors for 3+ days
- [todo] public beta outdoors (with & without sunlight) for 24+ hours
