# Description

This is a quick script that helps Hyprland automatically recognize when a screen
was tilted in order to rotate the screen automatically.

This is meant to be used with 2-in-1 laptop devices that detect these changes.

# Installation/How to use

First, download the package used to detect accelerometer changes with your preferred package manager:

```bash
sudo pacman -S iio-sensor-proxy
```

And then test if it works with:

```bash
monitor-sensor
```

If you see output changing depending on how your screen is tilted, like:

```bash
❯ monitor-sensor
    Waiting for iio-sensor-proxy to appear
+++ iio-sensor-proxy appeared
=== Has accelerometer (orientation: undefined, tilt: undefined)
=== No ambient light sensor
=== No proximity sensor
=== No compass
    Accelerometer orientation changed: normal
    Tilt changed: vertical
    Tilt changed: tilted-down
    Tilt changed: vertical
    Tilt changed: tilted-down
    Accelerometer orientation changed: right-up
    Tilt changed: vertical
    Accelerometer orientation changed: normal
    Accelerometer orientation changed: left-up
    Accelerometer orientation changed: bottom-up
    Accelerometer orientation changed: left-up
    Accelerometer orientation changed: normal
    Tilt changed: tilted-down
    Tilt changed: vertical
^C
```

Then it is workig perfectly.

Now, install the script:

```bash
git clone https://github.com/winston142O/Auto-rotate-hyprland.git
cd Auto-rotate-hyprland
cp auto-rotate-hyprland.sh ~/.local/bin/auto-rotate.sh
```

If necessary, verify the name of the monitor you want to detect changes for with the
`hyprctl monitors` command and replace the value according in the script (`DISPLAY_DEVICE`). 

Once placed there, make it executable with:

```bash
chmod +x ~/.local/bin/auto-rotate.sh
```

Then, open your Hyprland configuration file:

```bash
nano ~/.config/hypr/hyprland.conf
```

And add this line among the other `exec-once` entries:

```bash
exec = ~/.local/bin/auto-rotate.sh &
```

Save the configuration file and reload:

```bash
hyprctl reload
```
