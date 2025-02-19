<h3>Setup Guide - Debian Sid</h3>

- Also applies to Sparky Rolling, Siduction, Nitrux which are rolling by default.


#### How to switch Debian 11 to Rolling/Sid.
```sh
1. Edit /etc/apt/sources.list:
sudo nano /etc/apt/sources.list

2. Edit sources.list to only use these repos:

deb http://deb.debian.org/debian/ sid main contrib non-free
deb-src http://deb.debian.org/debian/ sid main

3. Save the file and update your system to Sid (This will reboot your system):

sudo apt update && sudo apt full-upgrade && sudo reboot
```
- Optionally you can install `apt-listbugs apt-listchanges` to read the bugs and see if any of them will break your distro.

#### MPR and MPR helper
```sh
wget -qO - 'https://proget.hunterwittenborn.com/debian-feeds/makedeb.pub' | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/makedeb-archive-keyring.gpg &> /dev/null && echo 'deb [signed-by=/usr/share/keyrings/makedeb-archive-keyring.gpg arch=all] https://proget.hunterwittenborn.com/ makedeb main' | \
sudo tee /etc/apt/sources.list.d/makedeb.list && sudo apt update && sudo apt install makedeb git && git clone https://mpr.hunterwittenborn.com/una-bin.git && cd una-bin && makedeb -si
```

#### dwarfs and overlayfs
```sh
git clone https://mpr.makedeb.org/dwarfs-bin.git && cd dwarfs-bin && makedeb -si
sudo apt install fuse-overlayfs
```

#### aria2
```sh
sudo apt install aria2
```

#### graphics packages
```sh
# Universal (AMD/Intel/Nvidia)
sudo apt install libvulkan1 vulkan-tools
sudo apt remove amdvlk

# NVIDIA specific
sudo add-apt-repository ppa:oibaf/graphics-drivers
sudo apt install nvidia-driver-510 nvidia-settings libvulkan1 vulkan-tools

Add `nvidia-drm.modeset=1` as a kernel parameter for the best results.
```

- NVIDIA legacy: check [Nvidia's  website](https://nvidia.custhelp.com/app/answers/detail/a_id/3142) for details on which version is right for your GPU.


#### gamescope
```sh
git clone https://github.com/jc141x/gamescope-git.git && cd gamescope-git && makedeb -si
```
- Nvidia not supported yet, but coming soon. Meanwhile don't install it or it will get used and fail to boot games.

- Technically optional, highly recommended against alt-tab freezes and isolation from system display server.

#### other libraries
```sh
sudo apt install gstreamer1.0-plugins-bad gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-ugly jq libva2 zstd
```

#### multilib libraries
```sh
sudo dpkg --add-architecture i386
sudo apt install libva2:i386 alsa-utils:i386 libopenal1:i386 libpulse0:i386
```

#### optional packages

##### yuzu
```sh
una install yuzu-mainline-bin
```
