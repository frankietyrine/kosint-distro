# K-OSINT.iso

## Build the ISO
### steps:
#### 1
``` bash
sudo apt update
sudo apt install git live-build cdebootstrap devscripts -y
git clone git://gitlab.com/kalilinux/build-scripts/live-build-config.git
cd live-build-config
```
#### 2 (check below) https://tools.kali.org/kali-metapackages
***$vi*** ``` kali-config/variant-default/package-lists/kali.list.chroot```
```
# You always want those
kali-linux-core

# Kali applications
kali-tools-information-gathering
kali-tools-reporting

# Graphical desktop
kali-desktop-xfce
```
#### 3 
***$vi*** ```kali-config/common/includes.binary/isolinux/install.cfg```
```
label install
    menu label ^Install Automated
    linux /install/vmlinuz
    initrd /install/initrd.gz
    append vga=788 -- quiet file=/cdrom/install/preseed.cfg locale=en_US keymap=us hostname=kali domain=local.lan
```

## Automatic installation process
### Packer
The VirtualBox Packer builder is able to create VirtualBox virtual machines and export them in the OVF format, starting from an ISO image. The builder builds a virtual machine by creating a new virtual machine from scratch, booting it, installing an OS, provisioning software within the OS, then shutting it down. The result of the VirtualBox builder is a directory containing all the files necessary to run the virtual machine portably.
- [packer-kali-linux/blob/master/kali.json](https://github.com/buffersandbeer/packer-kali-linux/blob/master/kali.json)

### Preceed
Preseeding provides a way to set answers to questions asked during the installation process, without having to manually enter the answers while the installation is running. This makes it possible to fully automate most types of installation and even offers some features not available during normal installations. If you are installing the operating system from a mounted iso as part of your Packer build, you will need to use a preseed file. [Example](https://www.debian.org/releases/stable/example-preseed.txt) 
- https://www.kali.org/dojo/preseed.cfg
- https://kali.training/topic/unattended-installations/
- [Full tutorial](https://www.debian.org/releases/stable/amd64/apb.en.html)
- [Automated Debian Install with Preseeding](https://www.youtube.com/watch?v=ndHi1sQWuH4)
- [preseed-kali-linux-from-a-mini-iso](https://medium.com/@honze_net/preseed-kali-linux-from-a-mini-iso-9ad622617241)

## Vagrant



### XFCE GUI
![](https://i.ytimg.com/vi/Twcm18oFmqs/maxresdefault.jpg)
After a research done, I came to the conclusion that xfce is probably the lightest and fasted gui. 
- [linux_distros/GUI_ram_consumption_comparison_updated](https://www.reddit.com/r/linux/comments/5l39tz/linux_distros_ram_consumption_comparison_updated/)
- [Power Use, RAM + Boot Times With Unity, Xfce, GNOME, LXDE, Budgie & KDE Plasma](https://www.phoronix.com/scan.php?page=article&item=ubu-1704-desktops&num=2)
- [Kali xfce](https://www.youtube.com/watch?v=Twcm18oFmqs)
- [Change from Gnome to xfce](https://www.youtube.com/watch?v=uIbG3SI5hd8)
- [How To Install Xfce4 & MATE Desktop Environments On Kali Linux](https://www.youtube.com/watch?v=hy9F87basCI)

## Links
- [create-kali-linux-iso](https://www.cybrary.it/blog/0p3n/create-kali-linux-iso/)
- [live-build-config-examples](https://gitlab.com/kalilinux/recipes/live-build-config-examples/-/blob/master/kali-linux-mate-top10-nonroot.sh)
- [dojo-mastering-live-build/](https://www.kali.org/docs/development/dojo-mastering-live-build/)
- [kali-metapackages](https://tools.kali.org/kali-metapackages)
- [creating-an-Ubuntu-VM-with-packer](https://kappataumu.com/articles/creating-an-Ubuntu-VM-with-packer.html)
- [how-to-use-packer-to-create-ubuntu-18-04-vagrant-boxes](https://www.serverlab.ca/tutorials/dev-ops/automation/how-to-use-packer-to-create-ubuntu-18-04-vagrant-boxes/)
- [whonix-kali](https://github.com/j7k6/vagrant-whonix-kali)
