# Omarchy on a VM

A linux distro on a Proxmox VM to host VS Code Server for web access. Chose Omarchy because I don't have any other use for the discreet GPU on my single node Proxmox machine.

VM specs:

* 2 CPU cores (host has i5 with 4 cores)
* 16GB memory (out of 32GB)
* 100GB disk
* Display: Virtu???
* Added PCI device: discrete GPU
* Mapped Thinkpad Trackpoint USB device to VM (with trackball)

## Performance improvements

### SSH

Enable sshd

sudo systemctl enable sshd
sudo systemctl start sshd
sudo ufw allow 22/tcp
sudo ufw reload
sudo ufw status
sudo tailscale set --ssh

### Disable SWAP

This is consumer grade hardware and swapping seemed to cause massive degradation of performance. It is not strictly necessary for always on system. Suspend and hibernated are disabled, althoug I believe they would use a different swap disk.

sudo systemctl --type swap
sudo systemctl mask --now dev-zram0.swap

Uninstall zram-generator

### Make all windows opaque

nano ~/.config/hypr/looknfeel.conf

Add:

windowrule = opaque on, match:class ^(.*)$

It automatically reloads on save

### Mirror monitors to keep Virtual monitor for VNC

Install hyprmon and choose to mirror displays on TUI. I'm sure this can be done in some config file too.

nano ~/.config/hypr/monitors.conf

Set Virtual Display size to match physical display (1080p):

monitor= Virtual-1,1920x1080@60,auto,1

Didn't figure out how to change resolution for Virtual display without restarting the machine.

### Dropbox selective sync

Dropbox required restarting the machince before I could connect it to my account.

No need to sync all files from Dropbox into a VM disk

dropbox-cli exclude add *
dropbox-cli exclude list
dropbox-cli exclude remove Notes

## Install software from Omarchy install

* tailscale
* nano
* VS Code
* 1Password
* Dropbox

## Claude Code on iPad

ssh into this over tailscale and type claude.

## VS Code Server 

code tunnel

Follow instructions to open vscode web session

## TODO

### Keyboard shortcuts

-[ ] ctrl + a / e should go start and end of line
-[ ] More Mac like keyboard shortcuts?
-[ ] Chromium and Terminal: Super + T should create new tab
-[ ] VS Code: Super + S should save 

### Terminal

-[ ] zsh
-[ ] oh-my-zs
-[ ] scm_breeze
-[ ] dotfiles
-[ ] try kitty or ghostty

### Settings

-[ ] VS Code settings sync
-[ ] ssh via tailscale ip√only
-[ ] GPG key to gpgagent
