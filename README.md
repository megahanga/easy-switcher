# Easy Switcher
Easy Switcher is a keyboard layout switcher and input corrector for Linux.  
It runs as a daemon in your system, is independent from your desktop environment and windowing system, works with the keyboard directly via kernel input, so it is reliable and smooth.   

## What's New
### Version 0.4 (June 2025)
- Added support for converting selected text using the `Ctrl+Shift+Pause` key combination. This feature allows you to convert highlighted text between Russian and English layouts (e.g., `Ghbdtn` to `Привет`). Requires `xclip` for clipboard operations on X11 systems.  
  **Note**: For Wayland, manual configuration with `wl-clipboard` may be required (not yet supported out-of-the-box).

## How does it work?
Easy Switcher writes your keystrokes to an internal buffer. When you press a special key (`Pause/Break` by default), it erases the last word or phrase, changes the layout, and rewrites the correct input. Additionally, you can convert selected text using `Ctrl+Shift+Pause`.

## Usage
1. Install and configure the daemon (see below).
2. If you enter text in the wrong layout:
   - Press `Pause/Break` to convert the last word.
   - Press `Shift+Pause/Break` to convert the entire phrase.
   - Highlight text and press `Ctrl+Shift+Pause` to convert the selected text between Russian and English layouts.

## How to build
Easy Switcher is written in Pascal. It can be built with [Free Pascal Compiler (FPC)](https://www.freepascal.org/) or [Lazarus](https://www.lazarus-ide.org/).  

### To build with FPC:
- Install FPC version 3.0.4 or later:
  ```bash
  sudo apt install fpc
  ```
- Install `xclip` for selected text conversion:
  ```bash
  sudo apt install xclip
  ```
- Clone this repository or download the sources.
- Navigate to the source folder:
  ```bash
  cd <path-to-easy-switcher>
  ```
- Build Easy Switcher:
  ```bash
  fpc -O2 -Xs -XX easy-switcher.lpr
  ```

### To build with Lazarus:
- Install the latest version of Lazarus:
  ```bash
  sudo apt install lazarus
  ```
- Install `xclip`:
  ```bash
  sudo apt install xclip
  ```
- Download the sources or clone the repository.
- Open `easy-switcher.lpi` in Lazarus.
- Click `Run > Build` or press `F9` to compile.

## Installation
### Ubuntu & Debian
- Download the [latest `.deb` package](https://github.com/freemind001/easy-switcher/releases).
- Install the package:
  ```bash
  sudo dpkg -i <path-to-easy-switcher.deb>
  ```
- Install `xclip` for selected text conversion:
  ```bash
  sudo apt install xclip
  ```
- Configure:
  ```bash
  sudo easy-switcher -c
  ```
- Start the Easy Switcher daemon:
  ```bash
  sudo systemctl start easy-switcher
  ```

### Other Linux & Custom Builds
- Build Easy Switcher (see above) or download the [latest binary](https://github.com/freemind001/easy-switcher/releases).
- Copy the `easy-switcher` binary to `/usr/bin/`:
  ```bash
  sudo cp easy-switcher /usr/bin/easyswitcher
  sudo chmod +x /usr/bin/easyswitcher
  ```
- Install `xclip` for selected text conversion:
  ```bash
  sudo apt install xclip
  ```
- Configure:
  ```bash
  sudo easy-switcher -c
  ```
- Install and start Easy Switcher as a daemon:
  - For systems with systemd:
    ```bash
    sudo easy-switcher -i
    sudo systemctl enable easy-switcher
    sudo systemctl start easy-switcher
    ```
  - For systems without systemd, run as an "old-style" daemon:
    ```bash
    sudo easy-switcher -o
    ```
    Refer to your OS documentation for daemon setup.

## Configuring
Easy Switcher includes a built-in configuration tool. Run it with:
```bash
sudo easy-switcher -c
```
Follow the prompts to:
- Detect your keyboard.
- Set the layout switch key (e.g., `Ctrl+Shift`).
- Set the replace key (e.g., `Pause/Break`).
- Set the selected text conversion key (e.g., `Ctrl+Shift+Pause`).

For advanced tuning, edit `/etc/easy-switcher/default.conf` manually. Example:
```ini
convert-selection-key=29+42+119
```
This sets `Ctrl+Shift+Pause` for selected text conversion.

## Troubleshooting
- Check runtime errors in syslog:
  ```bash
  sudo tail -f /var/log/syslog | grep easy-switcher
  ```
- Run in debug mode for detailed logs:
  ```bash
  sudo easy-switcher -d
  ```
- Ensure `xclip` is installed for `Ctrl+Shift+Pause` functionality.
- Verify key codes with `xev` if `Ctrl+Shift+Pause` doesn't work:
  ```bash
  sudo apt install x11-utils
  xev
  ```

## Known bugs & issues
- Incompatible with key remappers like `keyd`.
- Works better with single-key shortcuts for layout switching. Consider adding a single-key shortcut in your system settings for improved performance.
- Selected text conversion (`Ctrl+Shift+Pause`) is X11-only. Wayland support requires `wl-clipboard` and code modifications.

## Tags
punto switcher for Ubuntu, xneur analog, gxneur alternative

## Original Project
This project is a fork of the original [Easy Switcher](https://github.com/freemind001/easy-switcher) by [freemind001](https://github.com/freemind001). Contributions are based on the original codebase with enhancements for additional functionality.