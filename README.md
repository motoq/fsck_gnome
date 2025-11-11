# fsck_gnome
fsck_gnome is used to repair the gnome desktop environment


## Borders around windows

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
