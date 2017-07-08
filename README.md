# FreeBSD 11 notebook installation cheat-sheet

## 1) Turn off the terrible, annoying console beep:
```
# sysctl -w hw.syscons.bell=0
# sysctl -w kern.vt.enable_bell=0
```

## 2) Make this permanent by editing /etc/sysctl.conf and adding these 2 lines:
```
hw.syscons.bell=0
kern.vt.enable_bell=0
```

## 3) Update the system using "pkg update" (install pkgng if asked to)

## 4) Install necessary console utilities / system tools:
```
pkg install bash screen irssi ncmpc vim mpg123 git tig
```


## 5) Install graphical environment and Xorg utilities:
```
pkg install xorg xfce xscreensaver audacious audacious-plugins firefox chromium
```

## 6) Generate /etc/machine-id
```
uuidgen | tr -d "-" > /etc/machine-id
```

## 7) Create a minimal ~/.xinitrc file:
```
setxkbmap de
exec startxfce4
```

## 8) Enable psm configuration interface for trackpad/trackpoint:
/boot/loader.conf:
```
hw.psm.synaptics_support=1
hw.psm.trackpoint_support=1
```

## 9) Speed up trackpoint motion:
/etc/sysctl.conf:
hw.psm.trackpoint.sensitivity=240

## 10) To enable i915 kernel mode setting:
/boot/loader.conf:
i915kms_load="YES"

## 11) Add your user to the "video" group

## 12) The following optional settings in sysctl.conf have been proposed:

# Enhance shared memory X11 interface
kern.ipc.shmmax=67108864
kern.ipc.shmall=32768

# Enhance desktop responsiveness under high CPU use (200/224)
kern.sched.preempt_thresh=224

# Bump up maximum number of open files
kern.maxfiles=200000

# Disable PC Speaker
hw.syscons.bell=0

# Shared memory for Chromium
kern.ipc.shm_allow_removed=1


vfs.usermount=1

## 13) Consider the following in /etc/profile

LC_ALL=en_US.UTF-8; export LC_ALL
CHARSET=UTF-8; export CHARSET

## 14) Consider the following in /boot/loader.conf

hw.psm.synaptics_support=1
hw.psm.trackpoint_support=1

i915kms_load="YES"

# Devil worship in loader logo
loader_logo="beastie"

# Boot-time kernel tuning
kern.ipc.shmseg=1024
kern.ipc.shmmni=1024
kern.maxproc=100000

# Load MMC/SD card-reader support
mmc_load="YES"
mmcsd_load="YES"
sdhci_load="YES"

# Access ATAPI devices through the CAM subsystem
atapicam_load="YES"

# Filesystems in Userspace
fuse_load="YES"

# Intel Core thermal sensors
coretemp_load="YES"

# AMD K8, K10, K11 thermal sensors
#amdtemp_load="YES"

# In-memory filesystems
tmpfs_load="YES"

# Asynchronous I/O
aio_load="YES"

# Handle Unicode on removable media
libiconv_load="YES"
libmchain_load="YES"
cd9660_iconv_load="YES"
msdosfs_iconv_load="YES"

snd_driver_load="YES"

15) If you want your laptop to suspend on lid close, use the following in /etc/sysctl.conf:

# suspend on lid close
hw.acpi.lid_switch_state=s3

If you want to be able to use the battery widget in KDE, be sure you have hald enabled.
To enable hald, add the following line to /etc/rc.conf:
hald_enable="YES"

# A useful FreeBSD 11 desktop installation guide I found:
https://cooltrainer.org/a-freebsd-desktop-howto/

# Real-Time Audio (DAW) in FreeBSD
A friend of mine wrote a very informative blog post about that topic and allowed me to link there (thanks, Meka!):
http://meka.rs/blog/2017/01/25/sing-beastie-sing/

