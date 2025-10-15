## First of course, u have to download stage3 file from [gentoo download site](https://www.gentoo.org/downloads/)
In that case, we already have the distribution prepared.
1. ```sudo apt update && sudo apt upgrade```
2. ```sudo apt install gparted build-essential```
3. ```sudo gparted```
### On your external SSD / Pendrive create fat32 partition sized 512mb and ext4 labeled psxitarch
4. ```sudo su```
5. ```mkdir /mnt/gentoo```
6. ```mount /dev/sdx /mnt/gentoo```
7. ```tar xpf {localization of our stagefile} -C /mnt/gentoo --numeric-owner```
### wait for extracting file into new root
8. ```cp /etc/resolv.conf /mnt/gentoo/```
9. ```mount --types proc /proc /mnt/gentoo/proc```
10. ```mount --rbind /sys /mnt/gentoo/sys```
11. ```mount --make-rslave /mnt/gentoo/sys```
12. ```mount --rbind /dev /mnt/gentoo/dev```
13. ```mount --make-rslave /mnt/gentoo/dev```
14. ```mount --bind /run /mnt/gentoo/run```
15. ```mount --make-slave /mnt/gentoo/run```
16. ```cd /mnt/gentoo```
17. ```wget -o etc/portage/make.conf```