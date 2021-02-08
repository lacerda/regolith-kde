# Regolith under KDE (i3wm & Plasma)

![Screenshot of Regolith running on KDE](https://github.com/lacerda/regolith-kde/blob/master/img/screenshot.png?raw=true)

Regolith is a fantastic i3wm experience, particularly for those who don't want to set it up from scratch like myself.

However, I'm partial to KDE otherwise, and was not happy with the Gnome experience. This is my current set up, using Regolith with a KDE base.

This is not to be considered stable and you should be willing to debug and fiddle with config files. I might provide some help, but you are ultimately on your own. That said, I am very happy with this as my daily driver.

## Installation

1. Install core Regolith packages:

```
add-apt-repository ppa:regolith-linux/release
apt update
apt install i3-gaps i3-gaps-session i3-gaps-wm i3ipc-python i3xrocks regolith-compositor-picom-glx regolith-look-lascaille regolith-styles remontoire feh
```

2. Copy files from this repo accordingly:

- /usr/bin/
- /usr/share/xsessions/
- /etc/regolith/
- ~/.config/

It is important that this is done *after* the above packages are installed, as we will be overwriting some scripts.

3. Set up your plasma panel. 

Make sure you set the "Windows Go Below" property. Map the Application Launcher to Meta+Space.

Add the ~/.config/regolith/post-plasma.sh script to your KDE Autostart list. This will prevent i3bar from misaligning with the Plasma panel.

4. Set the Splash Screen to `None`.

5. Finally, disable any KDE/Plasma shortcuts that might interfere with i3wm. I recommend going through the list and changing them according to your use case.

6. Log out, choose the "Plasma with i3" session and log in again. Your will now be in Regolith with Plasma.

## Usage

Pressing Meta will show i3bar on top of Plasma panel.
Regolith can be configured as usual, with overrides in `~/.config/regolith/{i3, Xresources, picom}`.
When in doubt, consult the cheat sheet with `Meta+Shift+?`

## Known issues

- Searching in the 'Add Widgets...' screen rarely works. Workaround: scroll manually.
- Regolith updates may overwrite certain files.
- Multi monitor: Always set KDE to extend monitors side-by-side, never on top of each other, as this causes strange and inconsistent behavior with i3wm window resizing and positioning.

## Changes to Regolith code

- Replaced calls to Gnome services in `/etc/regolith/i3/config` and `/usr/bin/regolith-look`. Not 100% done, but enough for my usage.
- i3bar is transparent and autohides, overlaying the Plasma panel as necessary.
- `/usr/bin/remontoire-toggle` based on `conky-toggle`.
- Xresources compilation is done in `/etc/regolith/kde-session-init.sh`.
- XSession calls /usr/bin/i3-regolith, which starts i3wm with Regolith's i3 config after compiling Xresources.
- Plasma window rules for i3wm, found around the web.

