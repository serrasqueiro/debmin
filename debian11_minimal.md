# Debian 11 Minimal configuration
Here is the goal,
```
root@bell:~# cat /etc/os-release
PRETTY_NAME="Debian GNU/Linux 11 (bullseye)"
NAME="Debian GNU/Linux"
VERSION_ID="11"
VERSION="11 (bullseye)"
VERSION_CODENAME=bullseye
ID=debian
HOME_URL="https://www.debian.org/"
SUPPORT_URL="https://www.debian.org/support"
BUG_REPORT_URL="https://bugs.debian.org/"
```

## ISO installation
```
C:\TEMP>dir /od  debian-11.3.0-amd64-netinst.iso | grep iso$
File STDIN:
25/06/2022  14:00       396 361 728 debian-11.3.0-amd64-netinst.iso
```
ISO has approximately 400 Mb, it is the net installation.

# First aid to initial configuration
1. Set timezone, using the command line: **timedatectl set-timezone _geographical-zone_/_city_**
   + `timedatectl set-timezone Europe/Lisbon`
1. Put system is synchronizing NTP
   + `timedatectl set-ntp yes`
## About locale
Since I have used default United States configuration, locale is as follow next:
```
root@bell:~# locale
LANG=en_US.UTF-8
LANGUAGE=
LC_CTYPE="en_US.UTF-8"
LC_NUMERIC="en_US.UTF-8"
LC_TIME="en_US.UTF-8"
LC_COLLATE="en_US.UTF-8"
LC_MONETARY="en_US.UTF-8"
LC_MESSAGES="en_US.UTF-8"
LC_PAPER="en_US.UTF-8"
LC_NAME="en_US.UTF-8"
LC_ADDRESS="en_US.UTF-8"
LC_TELEPHONE="en_US.UTF-8"
LC_MEASUREMENT="en_US.UTF-8"
LC_IDENTIFICATION="en_US.UTF-8"
LC_ALL=
```
To show 24-hour in clock, use:
- `locale -a`
  + to display a list of all available locales.
- `localectl set-locale LC_TIME=en_GB.UTF-8`
  + this sets the actual system locale for the time clock.

# Expanding
## Swap space
Use a dedicated disk for the swap space, or a dedicated partition.
If you prefer to use a disk, you can also consider to divide that disk into two or more partitions.
```
root@bell:~# fdisk -l /dev/sdb
Disk /dev/sdb: 8 GiB, 8589934592 bytes, 16777216 sectors
Disk model: VBOX HARDDISK   
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes 
```
In this case I have adopted a relatively small (virtual) disk for this purpose.
`cfdisk` is simple to use, is ncurse/ text-menu based.
```
root@bell:~# fdisk -l /dev/sdb
Disk /dev/sdb: 8 GiB, 8589934592 bytes, 16777216 sectors
Disk model: VBOX HARDDISK   
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: A8BD7DCB-9733-234D-9AA5-6C008EAB3E90

Device       Start      End Sectors Size Type
/dev/sdb1     2048  8390655 8388608   4G Linux swap
/dev/sdb2  8390656 16777182 8386527   4G Linux swap 
```
1. `mkswap /dev/sdb1`
1. `mkswap /dev/sdb2`

# Maintenance
Please regularly update your server, using:
- `apt-get update`
```
Hit:1 http://security.debian.org/debian-security bullseye-security InRelease
Hit:2 http://deb.debian.org/debian bullseye InRelease
Get:3 http://deb.debian.org/debian bullseye-updates InRelease [39.4 kB]
Fetched 39.4 kB in 1s (47.5 kB/s)  
Reading package lists... Done 
```
