# swayinit -- like `xinit`, but for `sway`

If you're switching to sway from i3wm launched via xinit, you may have a hard time due to, say, your configuration depending on things being set or run in `/etc/profile` or `~/.xinitrc`.
Just launching sway via the provided `.desktop` unit will not execute anything in these files.
The solution is a small script that loads the profile you're used to, then runs sway; as well as a `.desktop` unit for it.

In detail, the `swayinit` script 
1. Reads `/etc/profile`
2. Reads `$XDG_CONFIG_HOME/profile.d/*.sh`. If `$XDG_CONFIG_HOME` is not set, default to `$HOME/.config`.
3. Sets the environment as specfied by `environment.d` files. (See [environment.d(5)](https://man.archlinux.org/man/environment.d.5).)
4. Looks for the following initialisation files and runs the first one found
   1. `$XDG_CONFIG_HOME/sway/swayinitrc`
   2. `$HOME/.config/sway/swayinitrc`
   3. `$HOME/.swayinitrc`
   4. `/etc/sway/swayinitrc`
5. Starts `sway`.

## Installation

Put `swayinit` somewhere on your `$PATH` and `swayinitrc.desktop` where your display manager can find it.
The paths in this repo work on, at least, Arch and Ubuntu.
