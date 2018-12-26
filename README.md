.tmux
=====

Self-contained, pretty and versatile `.tmux.conf` configuration file.

Installation
------------

Requirements:

  - tmux **`>= 2.1`** running inside Linux, Mac, OpenBSD, Cygwin or WSL (Bash on
    Ubuntu on Windows)
  - outside of tmux, `$TERM` must be set to `xterm-256color`

To install, run the following from your terminal: (you may want to backup your
existing `~/.tmux.conf` first)

```
$ cd
$ git clone https://github.com/gpakosz/.tmux.git
$ ln -s -f .tmux/.tmux.conf
$ cp .tmux/.tmux.conf.local .
```

Then proceed to [customize] your `~/.tmux.conf.local` copy.

[customize]: #enabling-the-powerline-look

If you're a Vim user, setting the `$EDITOR` environment variable to `vim` will
enable and further customize the vi-style key bindings (see tmux manual).

If you're new to tmux, I recommmend you read [tmux 2: Productive Mouse-Free
Development][bhtmux2] by [@bphogan].

[bhtmux2]: https://pragprog.com/book/bhtmux2/tmux-2
[@bphogan]: https://twitter.com/bphogan



Features
--------

 - `C-a` acts as secondary prefix, while keeping default `C-b` prefix
 - visual theme inspired by [Powerline][]
 - [maximize any pane to a new window with `<prefix> +`][maximize-pane]
 - SSH aware username and hostname status line information
 - mouse mode toggle with `<prefix> m`
 - automatic usage of [`reattach-to-user-namespace`][reattach-to-user-namespace]
   if available
 - laptop battery status line information
 - uptime status line information
 - optional highlight of focused pane (tmux `>= 2.1`)
 - configurable new windows and panes behavior (optionally retain current path)
 - SSH aware split pane (reconnects to remote server, experimental)
 - copy to OS clipboard (needs [`reattach-to-user-namespace`][reattach-to-user-namespace]
   on macOS, `xsel` or `xclip` on Linux)
 - [Facebook PathPicker][] integration if available
 - [Urlview][] integration if available

[Powerline]: https://github.com/Lokaltog/powerline
[maximize-pane]: http://pempek.net/articles/2013/04/14/maximizing-tmux-pane-new-window/
[reattach-to-user-namespace]: https://github.com/ChrisJohnsen/tmux-MacOSX-pasteboard
[Facebook PathPicker]: https://facebook.github.io/PathPicker/
[Urlview]: https://packages.debian.org/stable/misc/urlview

The "maximize any pane to a new window with `<prefix> +`" feature is different
from builtin `resize-pane -Z` as it allows you to further split a maximized
pane. It's also more flexible by allowing you to maximize a pane to a new
window, then change window, then go back and the pane is still in maximized
state in its own window. You can then minimize a pane by using `<prefix> +`
either from the source window or the maximized window.

![Maximize pane](https://cloud.githubusercontent.com/assets/553208/9890858/ee3c0ca6-5c02-11e5-890e-05d825a46c92.gif)

Mouse mode allows you to set the active window, set the active pane, resize
panes and automatically switches to copy-mode to select text.

![Mouse mode](https://cloud.githubusercontent.com/assets/553208/9890797/8dffe542-5c02-11e5-9c06-a25b452e6fcc.gif)

Bindings
--------

tmux may be controlled from an attached client by using a key combination of a
prefix key, followed by a command key. This configuration uses `C-a` as a
secondary prefix while keeping `C-b` as the default prefix. In the following
list of key bindings:
  - `<prefix>` means you have to either hit <kbd>Ctrl</kbd> + <kbd>a</kbd> or <kbd>Ctrl</kbd> + <kbd>b</kbd>
  - `<prefix> c` means you have to hit <kbd>Ctrl</kbd> + <kbd>a</kbd> or <kbd>Ctrl</kbd> + <kbd>b</kbd> followed by <kbd>c</kbd>
  - `<prefix> C-c` means you have to hit <kbd>Ctrl</kbd> + <kbd>a</kbd> or <kbd>Ctrl</kbd> + <kbd>b</kbd> followed by <kbd>Ctrl</kbd> + <kbd>c</kbd>

This configuration uses the following bindings:

 - `<prefix> e` opens `~/.tmux.conf.local` with the editor defined by the
   `$EDITOR` environment variable (defaults to `vim` when empty)
 - `<prefix> r` reloads the configuration
 - `C-l` clears both the screen and the tmux history

 - `<prefix> C-c` creates a new session
 - `<prefix> C-f` lets you switch to another session by name

 - `<prefix> C-h` and `<prefix> C-l` let you navigate windows (default
   `<prefix> n` and `<prefix> p` are unbound)
 - `<prefix> Tab` brings you to the last active window

 - `<prefix> -` splits the current pane vertically
 - `<prefix> _` splits the current pane horizontally
 - `<prefix> h`, `<prefix> j`, `<prefix> k` and `<prefix> l` let you navigate
   panes ala Vim
 - `<prefix> H`, `<prefix> J`, `<prefix> K`, `<prefix> L` let you resize panes
 - `<prefix> <` and `<prefix> >` let you swap panes
 - `<prefix> +` maximizes the current pane to a new window

 - `<prefix> m` toggles mouse mode on or off

 - `<prefix> U` launches Urlview (if available)
 - `<prefix> F` launches Facebook PathPicker (if available)

 - `<prefix> Enter` enters copy-mode
 - `<prefix> b` lists the paste-buffers
 - `<prefix> p` pastes from the top paste-buffer
 - `<prefix> P` lets you choose the paste-buffer to paste from

Bindings for `copy-mode-vi`:

- `v` begins selection / visual mode
- `C-v` toggles between blockwise visual mode and visual mode
- `H` jumps to the start of line
- `L` jumps to the end of line
- `y` copies the selection to the top paste-buffer
- `Escape` cancels the current operation

Configuration
-------------

While this configuration tries to bring sane default settings, you may want to
customize it further to your needs. Instead of altering the `~/.tmux.conf` file
and diverging from upstream, the proper way is to edit the `~/.tmux.conf.local`
file.

Please refer to the default `~/.tmux.conf.local` file to know more about
variables you can adjust to alter different behaviors. Pressing `<prefix> e`
will open `~/.tmux.conf.local` with the editor defined by the `$EDITOR`
environment variable (defaults to `vim` when empty).

### Configuring the status line

Contrary to the first iterations of this configuration, by now you have total
control on the content and order of `status-left` and `status-right`.

Edit the `~/.tmux.conf.local` file (`<prefix> e`) and adjust the
`tmux_conf_theme_status_left` and `tmux_conf_theme_status_right` variables to
your own preferences.

This configuration supports the following builtin variables:

 - `#{battery_bar}`: horizontal battery charge bar
 - `#{battery_percentage}`: battery percentage
 - `#{battery_status}`: is battery charging or discharging?
 - `#{battery_vbar}`: vertical battery charge bar
 - `#{circled_session_name}`: circled session number, up to 20
 - `#{hostname}`: SSH aware hostname information
 - `#{hostname_ssh}`: SSH aware hostname information, blank when no SSH
   connection detected
 - `#{loadavg}`: load average
 - `#{pairing}`: is session attached to more than one client?
 - `#{prefix}`: is prefix being depressed?
 - `#{root}`: is current user root?
 - `#{synchronized}`: are the panes synchronized?
 - `#{uptime_d}`: uptime days
 - `#{uptime_h}`: uptime hours
 - `#{uptime_m}`: uptime minutes
 - `#{uptime_s}`: uptime seconds
 - `#{username}`: SSH aware username information
 - `#{username_ssh}`: SSH aware username information, blank when no SSH
   connection detected
