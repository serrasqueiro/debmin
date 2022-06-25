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
