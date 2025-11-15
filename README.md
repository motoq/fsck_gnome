# fsck_gnome
fsck_gnome is used to repair the gnome desktop environment

The Windozification of the Linux user experience through the standardization of
systemd, PulseAudio, Wayland, and the Gnome desktop has been an unfortunate
development for Unix enthusiasts.  Disabling Wayland and installing a
proper window manager can go a long way towards repairing the damage
that has been done by mentally challenged software developers catering
to the Microsoft Windows user.  When no control over administration of the
system is possible, the best one can do is attempt to fsck Gnome through
proper configuration settings.  The majority of these changes are made through
the use of the **gsettings** command.


## command-not-found

The first step towards keeping one's sanity when working via the command
line on a *modern* Linux distribution is to either **apt purge** or
**dnf remove** the **command-not-found** package.  This bit of nonsense
is not part of Gnome, but must surely have been conceived through the
same mental illness that has shaped the development of such a horrific
desktop.  The command-not-found utility will take a simple typo and suggest
an alternative command along with the option to install the associated package.
Instead of instantly indicating an error allowing the user to quickly recover,
one must wait a short eternity while this invaluable service searches and
thinks about the command you clearly intended to type.  Even Microsoft
would envy the productivity crippling effect of such a terrible behavior.
It is truly an enhancement for the incompetent.

If admin rights are not available, then adding the following to your
*~/.bashrc* file will get the job done.
```
# PackageKit disable
unset -f command_not_found_handle
```
This one simple upgrade should considerably lower your blood pressure.


## Configuration via gsettings


### Window Sizing

To stop some applications from automatically maximizing windows on
startup:
```
gsettings set org.gnome.mutter auto-maximize false
```
To stop windows from trying to maximize just because you dragged them to
the edge of your screen to get them out of the way:
```
gsettings set org.gnome.mutter edge-tiling false
```
Seriously, I'm moving the window to the edge of the screen to get it out
of the way and some idiot decided what I really want to do is expand it
to take up the entire screen.  These are probably the same morons who
have crippled sloppy focus.

To add minimize and maximize control buttons to window title bar:
```
gsettings set org.gnome.desktop.wm.preferences button-layout ":minimize,maximize,close"
```
Why on earth these controls are often not visible by default is beyond
comprehension.


### Window and Focus Behavior due to Mouse Inputs

The option to enable sloppy focus not available from the GUI
configuration.  While fixing this behavior, enable pushing a window to the
bottom of the stack through a middle mouse button click on the title
bar:
```
gsettings set org.gnome.desktop.wm.preferences focus-mode 'sloppy'
# Middle click on titlebar pushes window to the back
gsettings set org.gnome.desktop.wm.preferences action-middle-click-titlebar 'lower'
```
For some reason, not all windows abide by the lower option.  Disabling
Wayland can help with other window managers, but applications such as
Firefox under Gnome can remain stubborn.  Even worse, for those windows
that do submit to doing what they are told, they often retain focus once
pushed to the bottom of the stack.  It is just mind blowing what developers
from the MS Windows community have done to destroy the Linux desktop.  I can
only assume their mothers ingested too much alcohol during gestation.


## Borders around windows

Gnome terminals can be difficult to distinguish when many are open and
overlap.  Adding a thin border greatly improves upon this while not
taking up noticeable screen space.

First enable headerbar for gnome-terminal:
```
gsettings set org.gnome.Terminal.Legacy.Settings headerbar true
```
Next, create
```
~/.config/gtk-3.0/gtk.css
```
with the following text:
```
decoration {
  border: 1px solid gray;
}

VteTerminal, TerminalScreen, vte-terminal {
  padding: 10px 10px 10px 10px;
}
```
It will most likely be necessary to log out and log back in for the
change to take effect.


## Misc


```
# Stop Gnome auto updates if you prefer handling system changes manually
gsettings set org.gnome.software download-updates false
```

```
# Make selected background image tile, not stretch
gsettings set org.gnome.desktop.background picture-options "wallpaper"
```

```
# Disabling the lock screen is helpful when accessing Linux via a VM and
# the physical computer already has lock screen enabled.
gsettings set org.gnome.desktop.lockdown disable-lock-screen 'true'
gsettings set org.gnome.desktop.screensaver lock-enabled false
```
