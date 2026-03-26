beep
===

A command-line tool to control the PC speaker to emit beeps.

## Introduction

`beep` is a command-line utility for precise control of the PC speaker to emit beeps. It can generate beeps of different frequencies, durations, repetitions, and delays, supports combining multiple tones into sequences, or triggering beeps based on newlines/characters from standard input (stdin). This tool is commonly used in shell or Perl scripts to provide audio alerts to users when specific events occur.

**Note**: `beep` requires PC speaker hardware support, usually needs the `pcspkr` kernel module loaded, and requires write permission to the output device.

## Installation
Debian/Ubuntu:
```bash
sudo apt install beep
```

RedHat/Centos/Fedora:
```bash
sudo yum install beep
```

## Syntax
```bash
beep [global options] [tone options] [-n|--new tone options...]...
beep [-h|--help]
beep [-v|-V|--version]
```

## Options

### Information Options
| Option            | Description                               |
|----------------|-----------------------------------|
| `-h, --help`   | Display help information and exit.                 |
| `-v, -V, --version` | Display version information and exit.           |

### Global Options
| Option                       | Description                                                         |
|---------------------------|-------------------------------------------------------------|
| `-e, --device=DEVICE`     | Explicitly specify the device used for beep output. If not specified, `beep` will try an internal list of devices until successful. |
| `--debug, --verbose`      | Enable detailed output, showing debug information.                                 |

### Tone Options
Each tone can be defined by a combination of the following options. If not specified, default values are used.

| Option                | Description                                                                 |
|--------------------|---------------------------------------------------------------------|
| `-f FREQ`          | Set beep frequency (unit: Hz). Must satisfy 0 < FREQ < 20000. Floating point numbers are accepted, but the kernel API will round them to integers. Default: 440 Hz. |
| `-l LEN`           | Set beep duration (unit: ms). Default: 200 ms.                          |
| `-r REPEATS`       | Set the number of repetitions for the current tone (including delays). Default: 1 (only once, no repetition).    |
| `-d DELAY`         | Set the delay between repetitions (unit: ms), **not** adding delay after the last repetition. Default: 100 ms. |
| `-D DELAY`         | Set the delay between repetitions (unit: ms), **and** adding the delay after the last repetition. Default: no delay. |
| `-n, --new`        | Start defining a new tone. Each `-n` can be followed by a new set of tone options; the new tone inherits all default values until overridden by explicit options. |
| `-s`               | Put `beep` in input processing mode: read data from stdin, emit the currently defined tone once for every **newline** encountered, while copying the input data to stdout as is. |
| `-c`               | Similar to `-s`, but triggers a beep for every **character** encountered.                  |

**Note**:
- Difference between `-d` and `-D`: `-r 3 -d 100` produces: beep, delay, beep, delay, beep (end); `-r 3 -D 100` produces: beep, delay, beep, delay, beep, delay (end).
- In a sequence of multiple tones connected by `-n`, **only one tone** can have `-s` or `-c`. `beep` will first play all tones before that tone, then enter input processing mode, repeat that tone according to input until EOF, and finally play any remaining tones.
- If an option appears multiple times on the command line, the later one overrides the earlier one.

## Environment Variables
| Variable Name            | Description                                                                 |
|------------------|---------------------------------------------------------------------|
| `BEEP_LOG_LEVEL` | Set log level (range -999 to 999). If `--debug` is not used on the command line, this value is used as the default log level. |

## Files
`beep` tries to open the following devices in order until successful:
- `/dev/input/by-path/platform-pcspkr-event-spkr` (using evdev API)
- `/dev/tty0` (using console API)
- `/dev/vc/0` (using console API)

## Exit Status
| Status Code | Meaning                     |
|--------|--------------------------|
| 0      | Successful execution                 |
| Non-zero    | Error occurred (e.g., device cannot be opened, invalid parameters, etc.) |

## Notes

### Device and Permissions
- **Non-root users**: By default, `/dev/tty0` and `/dev/vc/0` require root privileges or ownership of the current TTY. It is recommended to use the evdev device `/dev/input/by-path/platform-pcspkr-event-spkr`, where appropriate permissions can be set via udev rules so that normal users can also use `beep`.
- `beep` **does not support** running as setuid root or via `sudo`. Please authorize through file permissions or udev rules.
- If the command does not execute correctly, please check if the `pcspkr` module is loaded.

### API Description
- **evdev**: Uses the input event device driver via `write()` operations. Opening the device takes about 20ms, so to play a melody, it's recommended to use multiple tones in a single `beep` command (via `-n`) rather than multiple calls to `beep`.
- **console**: Uses the old `KIOCSOUND ioctl` interface, which is only available without root when the user is logged into a virtual console (e.g., `/dev/tty4`) and owns that terminal. Not applicable for users logged in via SSH or a graphical interface.

### Concurrent Calls
`beep` does not support concurrent execution. The PC speaker hardware has only one sound generator; multiple `beep` processes will interfere with each other. For example, while a long beep process is running, another short beep process will interrupt it, and the former will silently turn off the speaker afterwards, leading to unexpected silence.

### Volume Control
- Independent PCs usually use piezo buzzers, whose volume is frequency-dependent and loudest near the resonance frequency (about 2000 Hz). Try around 2050 Hz for maximum volume.
- Laptops may route PC speaker output to built-in speakers; in this case, the volume can be adjusted via the "Beeper" or "PC Speaker" channel in the sound card mixer.

### Frequency Reference Table
Below is the relationship between musical notes and frequencies.

| Note | Octave 3 | Octave 4 | Octave 5 | Octave 6 |
|------|--------|--------|--------|--------|
| C    | 131    | 262    | 523    | 1047   |
| C#   | 139    | 277    | 554    | 1109   |
| D    | 147    | 294    | 587    | 1175   |
| D#   | 156    | 311    | 622    | 1245   |
| E    | 165    | 330    | 659    | 1319   |
| F    | 175    | 349    | 698    | 1397   |
| F#   | 185    | 370    | 740    | 1480   |
| G    | 196    | 392    | 784    | 1568   |
| G#   | 208    | 415    | 831    | 1661   |
| A    | 220    | 440    | 880    | 1760   |
| A#   | 233    | 466    | 932    | 1865   |
| B    | 247    | 494    | 988    | 1976   |
| C    | 262    | 523    | 1047   | 2093   |

## Examples

### 1. Simple Beep
```bash
beep
```
Emits the default beep (440 Hz, 200 ms).

### 2. Specify Frequency and Duration
```bash
beep -f 800 -l 500
```
Emits an 800 Hz beep for 500 milliseconds.

### 3. Repeated Beeps
```bash
beep -f 600 -l 100 -r 3 -d 50
```
Repeats 3 times, 100 ms each, with a 50 ms interval, no delay after the last one.

```bash
beep -f 600 -l 100 -r 3 -D 50
```
Repeats 3 times, 100 ms each, with a 50 ms interval, and a 50 ms delay after the last one.

### 4. Two Different Tones
```bash
beep -f 400 -l 200 -n -f 800 -l 200
```
Emits a 400 Hz tone (200 ms), followed immediately by an 800 Hz tone (200 ms) with no additional delay between them.

### 5. Adding Delay Between Tones (via -D on the previous tone)
```bash
beep -f 400 -l 200 -D 100 -n -f 800 -l 200
```
Emits a 400 Hz tone, then delays for 100 ms (because `-D` appends a delay to that tone), then emits an 800 Hz tone.

### 6. Beep on Each New Line
```bash
tail -f /var/log/syslog | beep -s
```
Emits the currently defined tone (default 440 Hz) whenever a new line is written to the log.

### 7. Beep for Each Character Entered (Typewriter effect)
```bash
cat /dev/stdin | beep -c
```
Emits a beep for every key pressed (including Enter) in the terminal; the input content is also displayed.

### 8. Using a Custom Device
```bash
beep -e /dev/input/by-path/platform-pcspkr-event-spkr -f 1000
```
Emits a 1000 Hz beep by specifying the evdev device.

### 9. Complex Sequence: Play a series of tones, then repeat a tone based on input, and finish
```bash
beep -f 523 -l 200 -n -f 659 -l 200 -n -f 784 -l 200 -n -s -f 440 -l 100 -r 3 -n -f 523 -l 400
```
First plays C5 (523 Hz), E5 (659 Hz), G5 (784 Hz) for 200 ms each (no delay between them); then enters input processing mode, playing A4 (440 Hz) three times (100 ms each, default 100 ms interval) for every newline; after input ends (Ctrl+D), finally plays a long C5 (523 Hz, 400 ms).

## Related Documentation
For more detailed information, refer to the `man` page:
```bash
man beep
```
