xrandr
===

An X Window System configuration management tool.

## Supplemental Information

**xrandr** (Rotate and Resize) is an X Window System extension that allows clients to dynamically adjust (scale, rotate, flip) the screen. **xrandr** is the official RandR extension configuration tool.

### Syntax

```shell
xrandr (options) (parameters)
```

### Options

```shell
--auto      # Output at the system's maximum resolution
--off       # Set the specified device to off
--output    # Specify output device
--mode      # Set resolution
--rate      # Set refresh rate
--right-of  # Place output to the right of the primary display
--left-of   # Place output to the left of the primary display
--above     # Place output above the primary display
--below     # Place output below the primary display
```

### Parameters

* Display device ID

### Examples

Test configuration, listing available devices and their information:

```shell
xrandr
Screen 0: minimum 320 x 200, current 3200 x 1080, maximum 8192 x 8192
VGA-1 disconnected (normal left inverted right x axis y axis)
HDMI-1 connected primary 1920x1080+0+0 (normal left inverted right x axis y axis) 531mm x 299mm
   1920x1080     59.93 +  60.00*   50.00    59.94  
   1920x1080i    60.00    50.00    59.94  
   1680x1050     59.88  
…
```

Clone screens:

```shell
xrandr --output HDMI-1 --auto
```

Multi-display setup: Turn off the one not needed:

```shell
xrandr --output HDMI-1 --off --output HDMI-2 --auto
```

Specify resolution and refresh rate:

```shell
xrandr --output HDMI-1 --mode 1920x1080 --rate 60
```

VGA1 positioned to the left of HDMI1, both using optimal resolution, split screen display:

```shell
xrandr --output VGA1 --auto --output HDMI1 --auto --right-of VGA1
```
