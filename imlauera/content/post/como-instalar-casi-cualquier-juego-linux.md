---
title: "Como correr casi cualquier juego en GNU/Linux"
date: 2022-11-16T05:46:20-03:00
---

Primero tenes plataforma como Lutris y PlayOnLinux que son facilmente instalables ejecutando 
```bash
sudo apt install -y lutris playonlinux
```
O en el caso de distros derivadas de Arch
```bash
sudo pacman -S lutris playonlinux
```
o en fedora usando el gestor de paquetes: dnf

Después tenés emuladores de PlayStation 2 (PCSX2),3(RPCS3) y emulador de Gamecube(Dolphin) (hay juegos que tiran mas fps en Dolphin (Gamecube) que en el emulador de PS2). Si con eso no te basta podes buscar "linux" en la categoría de Games en [1337x](https://1337x.to). Y te van a aparecer un listado de torrents de juegos hechos por un tipo de nickname johncena141, pero para correr estos juegos necesitas instalar dependencias y seguir el siguiente setup (aunque hay algunos que corren sin necesidad de hacer nada):


## jc141 setup guide
La Guia Oficial de JC141: https://github.com/jc141x/jc141-bash/tree/master/setup

Si no tenés GNU/Linux instalado la guía recomienda usar [EndeavourOS](https://discovery.endeavouros.com/installation/create-install-media-usb-key/2021/03/) que es una distro nueva basada en Arch, muchos la consideran mejor que Manjaro.

### Setup Guide - Arch 
  
- También sirve para EndeavourOS, Artix, ArcoLinux, Manjaro, cualquier distro basada de Arch.

#### agrega el repositorio rumpowered y el multilib
```sh
echo '

[rumpowered]
Server = https://jc141x.github.io/rumpowered-packages/$arch ' | sudo tee -a /etc/pacman.conf

sudo sed -i "/\[multilib\]/,/Include/"'s/^#//' /etc/pacman.conf

sudo pacman-key --recv-keys cc7a2968b28a04b3
sudo pacman-key --lsign-key cc7a2968b28a04b3

sudo pacman -Syyu
```

#### paquetes básicos
```sh
sudo pacman -S --needed rumpowered/dwarfs fuse-overlayfs wine-staging wine-mono openssl-1.1
```

#### paquetes gráficos
```sh
Vulkan drivers (AMD/INTEL/NVIDIA)
sudo pacman -S --needed lib32-vulkan-icd-loader vulkan-icd-loader 
```
```sh
AMD drivers
sudo pacman -S --needed lib32-vulkan-radeon vulkan-radeon
```
```sh
INTEL drivers
sudo pacman -S --needed lib32-vulkan-intel vulkan-intel
```
```sh
NVIDIA drivers
sudo pacman -S --needed lib32-libglvnd lib32-nvidia-utils libglvnd nvidia
```
- AMD: 
Asegúrese de no tener amdvlk instalado con `sudo pacman -R amdvlk`. Tenerlo instalado causará muchos problemas.

- NVIDIA: Agrega `nvidia-drm.modeset=1` como un parámetro del kernel para los mejores resultados.

#### varias bibliotecas requeridas por algunos juegos
```sh
sudo pacman -S --needed lib32-giflib lib32-gnutls lib32-libxcomposite lib32-libxinerama lib32-libxslt lib32-mpg123 lib32-v4l-utils lib32-alsa-lib lib32-alsa-plugins lib32-libpulse lib32-openal lib32-zlib giflib libgphoto2 libxcrypt-compat zlib gst-plugins-base gst-plugins-good gst-plugins-ugly gst-plugins-bad gstreamer-vaapi gst-libav
```

#### OPTIONAL - bindtointerface - bloquear actividad de red no-LAN port defecto
```
sudo pacman -S --needed rumpowered/bindtointerface
```

## Setup Guide - Debian Rolling/Sid

- Aplica también para distros como Sparky Rolling, Siduction, Nitrux que son rolling releases por defecto.

#### Switch to the Rolling/Sid repo for an optimal and up to date experience.
Note: Debian Stable repo is no longer compatible with latest DXVK, thus it is not supported.
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

#### MPR, MPR helper and wine repos
```sh
sudo dpkg --add-architecture i386
wget -qO - 'https://proget.hunterwittenborn.com/debian-feeds/makedeb.pub' | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/makedeb-archive-keyring.gpg &> /dev/null && echo 'deb [signed-by=/usr/share/keyrings/makedeb-archive-keyring.gpg arch=all] https://proget.hunterwittenborn.com/ makedeb main' | \
sudo tee /etc/apt/sources.list.d/makedeb.list && sudo apt update && sudo apt install makedeb git && git clone https://mpr.hunterwittenborn.com/una-bin.git && cd una-bin && makedeb -si
sudo mkdir -pm755 /etc/apt/keyrings
sudo wget -O /etc/apt/keyrings/winehq-archive.key https://dl.winehq.org/wine-builds/winehq.key
sudo wget -NP /etc/apt/sources.list.d/ https://dl.winehq.org/wine-builds/debian/dists/bullseye/winehq-bullseye.sources
```

#### core packages
```sh
git clone https://mpr.makedeb.org/dwarfs-bin.git && cd dwarfs-bin && makedeb -si
sudo apt install fuse-overlayfs winehq-staging
```

#### graphics packages
```sh
Vulkan drivers (AMD/INTEL)
sudo apt install libvulkan1 vulkan-tools
```
```sh
NVIDIA drivers
sudo wget -O- https://developer.download.nvidia.com/compute/cuda/repos/debian11/x86_64/3bf863cc.pub | gpg --dearmor | sudo tee /usr/share/keyrings/nvidia-drivers.gpg

echo 'deb [signed-by=/usr/share/keyrings/nvidia-drivers.gpg] https://developer.download.nvidia.com/compute/cuda/repos/debian11/x86_64/ /' | sudo tee /etc/apt/sources.list.d/nvidia-drivers.list

sudo apt update && sudo apt upgrade -y

sudo apt install nvidia-driver nvidia-settings nvidia-smi nvidia-xconfig nvidia-opencl-icd nvidia-opencl-common nvidia-detect linux-image-amd64 linux-headers-amd64
```

- NVIDIA: Add `nvidia-drm.modeset=1` as a kernel parameter for the best results.

#### various libraries required by some games
```sh
sudo apt install libva2 giflib-tools libgphoto2-6 libxcrypt-source libva2:i386 alsa-utils:i386 libopenal1:i386 libpulse0:i386 gstreamer1.0-plugins-bad gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-ugly gstreamer1.0-vaapi gstreamer1.0-libav
```


#### [Fedora and Rawhide](fedora.md)
#### Setup Guide - Fedora

#### core packages
```sh
sudo dnf copr enable jc141/DwarFS && sudo dnf install fuse-overlayfs dwarfs wine wine-mono
```

#### graphics packages

```sh
# Universal
sudo dnf install vulkan vulkan-loader

# NVIDIA specific
sudo dnf install https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm && sudo dnf install xorg-x11-drv-nvidia akmod-nvidia

Add `nvidia-drm.modeset=1` as a kernel parameter for the best results.
```

- Fedora does not provide wine-staging. Unexpected issues can occur.

#### other libraries
```sh
sudo dnf install libxcrypt zlib alsa-lib alsa-plugins fluidsynth pulseaudio openal
```
#### [OpenSUSE Tumbleweed](opensuse.md)
### Setup Guide - OpenSUSE Tumbleweed

#### core packages
```sh
sudo zypper ar https://download.opensuse.org/repositories/home:/jc141/openSUSE_Tumbleweed/home:jc141.repo
sudo zypper refresh
sudo zypper install dwarfs fuse-overlayfs wine-staging wine-mono
```

#### graphics packages
```sh
Vulkan drivers
sudo zypper install libvulkan1 vulkan-tools
AMD drivers
sudo zypper install libvulkan_radeon libvulkan_radeon-32bit
INTEL drivers
sudo zypper install libvulkan_intel libvulkan_intel-32bit
NVIDIA drivers (guide incomplete for now)
sudo zypper install libglvnd-32bit libglvnd
```
- NVIDIA: Add `nvidia-drm.modeset=1` as a kernel parameter for the best results.

#### various libraries required by some games
```sh
sudo zypper install giflib-devel-32bit libXcomposite-devel-32bit libXinerama-devel-32bit libxslt-devel-32bit mpg123-devel-32bit mpg123-openal-32bit zlib-devel-32bit libpulse-devel-32bit giflib-devel libgphoto2-6 zlib-devel libva2 gstreamer-plugins-base gstreamer-plugins-good gstreamer-plugins-ugly gstreamer-plugins-bad gstreamer-plugins-vaapi gstreamer-plugins-libav
```

### not supported distros

Releases might work but we can't promise anything and don't want to waste time troubleshooting, for setup look at what most closely resembles your distro and use common sense. For example, if you use apt as your package manager you go for debian.

 - Ubuntu (malware)
   - And all distros based on it: Kubuntu, Lubuntu, Xubuntu, Mint, Elementary OS, Zorin OS, POP! OS, LXLE, KDE Neon 
 - SteamOS (malware, read-only, lack of packages)
 - Fedora Silverblue (read-only)

### hardware support

- The GPU/APU must have vulkan support otherwise hardly any releases with wine will run.

- The dwarfs mounting system requires modern speed standards from storing devices as well as RAM.

- [SteamDeck support on Arch](steamdeck.md)
## Setup Guide - SteamDeck

- Report issues you are having to us on matrix.
- SteamOS not supported or planned to be.

#### install any Arch distro. We recommend EndeavourOS.

1. Create a bootable usb drive with the distro iso. - [Guide](https://discovery.endeavouros.com/installation/create-install-media-usb-key/2021/03/)
2. Use a USB-C adapter to connect the drive to your deck.
3. Turn off your deck, hold 'Volume Down' and click the Power button, when you hear a sound let go of the volume button.
4. Select the usb efi device.
5. Follow installer steps. Pick KDE Plasma if you want to deal with least amount of issues. (online install)
6. Boot into new system and run `sudo pacman -Syyu` then reboot again.

#### add required repos

```sh
echo '

[rumpowered]
SigLevel = Never
Server = https://repo.rumpowered.org/$arch

[jupiter]
Server = https://steamdeck-packages.steamos.cloud/archlinux-mirror/$repo/os/$arch
SigLevel = Never

[holo]
Server = https://steamdeck-packages.steamos.cloud/archlinux-mirror/$repo/os/$arch
SigLevel = Never ' | sudo tee -a /etc/pacman.conf

sudo sed -i "/\[multilib\]/,/Include/"'s/^#//' /etc/pacman.conf

sudo pacman -Syyu
```

#### SteamDeck Hardware drivers

```sh
sudo pacman -S jupiter/linux-neptune jupiter/linux-neptune-headers jupiter/linux-firmware-neptune jupiter/jupiter-hw-support rumpowered/sc-controller
```

#### make new kernel default

```sh
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

Reboot and select the option with `linux neptune` using the arrow keys.


#### core packages
```sh
sudo pacman -S --needed rumpowered/dwarfs fuse-overlayfs wine-staging wine-mono openssl-1.1
```

#### graphics packages
```sh
sudo pacman -S --needed lib32-vulkan-icd-loader vulkan-icd-loader lib32-vulkan-radeon vulkan-radeon
```

#### various libraries required by some games
```sh
sudo pacman -S --needed lib32-giflib lib32-gnutls lib32-libxcomposite lib32-libxinerama lib32-libxslt lib32-mpg123 lib32-v4l-utils lib32-alsa-lib lib32-alsa-plugins lib32-libpulse lib32-openal lib32-zlib giflib libgphoto2 libxcrypt-compat zlib gst-plugins-base gst-plugins-good gst-plugins-ugly gst-plugins-bad gstreamer-vaapi gst-libav
```

#### post-setup
- On KDE Plasma, you might need to go into settings and set the correct screen position. On other DE's you might be stuck with no such options.



### running

```sh
cd "path to extracted game"
bash start.w.sh - or however the script is named.

To enable terminal output, add DBG=1 before bash command.
```
- settings.sh commands
```
bash settings.sh extract-dwarfs / unmount-dwarfs / mount-dwarfs / delete-dwarfs / compress-to-dwarfs
```

#### modding on dwarfs

- Adding mods is supported through groot-rw directory. Before mounting, any files included in it will go above the mounted image and override any of the files. The path required for the mod may need to be created manually.

- Games which are extracted do not require this method.

#### other notes

- The testing is done on Arch or EndeavourOS with EXT4, BTRFS or XFS filesystems.
