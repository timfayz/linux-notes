# Linux Mint



## Packages
	apt upgrade

### Tools
* git
* dconf-editor
* xclip
* djview4
* build-essentials
* neovim:

	# install Plug
	curl -fLo ~/.local/share/nvim/site/autoload/plug.vim --create-dirs \
	    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim

### Apps
* vscode (external): sync settings from git
* telegram-desktop
* dropbox
* playonlinux
* vlc

## Configuration
* Nemo ->
	- View -> [] Show toolbar
    - Prefs -> Views ->
        * Icon View Defaults -> Zoom = 66%
        * View new folders = List view
    - org.nemo.desktop vertical-grid-adjust 0.8

* System Settings ->
	- Hot corners
	- Wifi (explain)
	- Set compose key
	- Add lang layouts & chache switch keys
	- Disable second monitor
	- Suspend on battery
	- Disable system sounds
	- Shortcuts: switch worspaces, move to ws, run terminal & browser
	- Window tiling: maximize on top, steal focus off
	- Worspaces: cycling on
	- Effects off
	- Login: disable guests, change GTK themes, disable idicators on login, disable grid
	- Configure weekly backup
	- Appearance: change theme to Mint-Y
	- Change start menu icon & change firefox icon
	- Smash startup apps
	- Go through Optimize SSD (https://sites.google.com/site/easylinuxtipsproject/ssd)
	- Go through Speedup Mint (https://sites.google.com/site/easylinuxtipsproject/3)

    #  General
    Disable compositing for full-screen windows: ON
    # vim /etc/bluetooth/main.conf
    AutoEnable=false
    # Put /tmp on tmpfs
    sudo cp -v /usr/share/systemd/tmp.mount /etc/systemd/system/
    sudo systemctl enable tmp.mount
    systemctl status tmp.mount
    # /etc/initramfs-tools/conf.d/resume
    RESUME=NONE or comment it

	- remove btrfs

    sudo apt purge btrfs-progs btrfs-tools
    sudo update-initramfs -ukall (optional)

