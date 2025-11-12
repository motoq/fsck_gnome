# fsck_gnome
fsck_gnome is used to repair the gnome desktop environment

The Windozification of the Linux user experience through the standardization of
systemd, PulseAudio, Wayland, and the Gnome desktop has been an unfortunate
development for Unix enthusiasts.  Disabling Wayland and installing a
proper window manager can go a long way towards enhancing the user experience.
When no control over administration of the system is possible, the best one
can do is attempt to fsck Gnome through proper configuration settings.  The
majority of these changes are made through the use of the **gsettings** command.


## command-not-found

The first step towards keeping one's sanity when working via the command
line on a *modern* linux distribution is to either **apt purge** or
**dnf remove** the **command-not-found** package.  This bit of nonsense
is not part of Gnome, but must surely have been conceived through the
same mental illness that has shaped the development of such a horrific
desktop.  The command-not-found package will take a simple command
line typo and suggest an alternative command.  Instead of instantly indicating
an error allowing the user to quickly recover, one must wait a short eternity
while this invaluable service searches and thinks about the command you
clearly intended to type or potential package that could be installed.  Even
Microsoft would envy the productivity crippling effect of such a terrible
behavior.  It is truly an enhancement for the incompetent.


## Configuration via gsettings


### Window Autosizing

To stop windows from automatically being maximized when they first appear:
```
gsettings set org.gnome.mutter auto-maximize false
```

To add minimize and maximize control buttons to windows title bar:
```
gsettings set org.gnome.desktop.wm.preferences button-layout ":minimize,maximize,close"
```
Why on earth these controls are often not visible by default is beyond
comprehension.


### Window and focus behavior due to Mouse Inputs

```
gsettings set org.gnome.desktop.wm.preferences action-middle-click-titlebar 'lower'
```


## Borders around windows

Gnome terminals can be difficult to distingush when many are open and
overlap.  Adding a thin border greatly improves upon this while not
taking up noticeable screen space.

First enable headerbar for ghome-terminal:
```
gsettings set org.gnome.Terminal.Legacy.Settings headerbar true
```
Next, create
```
~/.config/gtk-e.0/gtk.css
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
