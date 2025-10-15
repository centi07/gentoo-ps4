## First of course, u have to download stage3 file from [gentoo download site](https://www.gentoo.org/downloads/)

In that case, we already have the distribution prepared.
1. ```sudo apt update && sudo apt upgrade```
2. ```sudo apt install gparted build-essential wget curl```
3. ```sudo gparted```  </br>
On your external SSD / Pendrive create fat32 partition sized 512mb and ext4 labeled psxitarch
4. ```sudo su```
0. ```mkdir /mnt/bootps4```
0. ```mount /dev/sdx1 /mnt/bootps4```
0. ```wget https://github.com/centi07/gentoo-ps4/raw/refs/heads/main/initramfs-bzimage/initramfs.cpio.gz -o /mnt/bootps4/initramfs.cpio.gz```
0. ```wget https://github.com/centi07/gentoo-ps4/raw/refs/heads/main/initramfs-bzimage/bzImage -o /mnt/bootps4/bzImage```
0. ```umount /dev/sdx2```
5. ```mkdir /mnt/gentoo```
6. ```mount /dev/sdx2 /mnt/gentoo```
7. ```tar xpf {localization of our stagefile} -C /mnt/gentoo --numeric-owner``` </br>
wait for extracting file into new root  
8. ```cp /etc/resolv.conf /mnt/gentoo/```
9. ```mount --types proc /proc /mnt/gentoo/proc```
10. ```mount --rbind /sys /mnt/gentoo/sys```
11. ```mount --make-rslave /mnt/gentoo/sys```
12. ```mount --rbind /dev /mnt/gentoo/dev```
13. ```mount --make-rslave /mnt/gentoo/dev```
14. ```mount --bind /run /mnt/gentoo/run```
15. ```mount --make-slave /mnt/gentoo/run```
16. ```cd /mnt/gentoo```
17. ```wget https://raw.githubusercontent.com/centi07/gentoo-ps4/refs/heads/main/portage-files/make.conf -o /mnt/gentoo/etc/portage/make.conf```
18. ```wget https://raw.githubusercontent.com/centi07/gentoo-ps4/refs/heads/main/portage-files/00cpu-flags -o /mnt/gentoo/etc/portage/package.use/00cpu-flags```
19. ```wget https://raw.githubusercontent.com/centi07/gentoo-ps4/refs/heads/main/portage-files/mesa -o /mnt/gentoo/etc/portage/package.mask/mesa```
20. ```wget https://raw.githubusercontent.com/centi07/gentoo-ps4/refs/heads/main/portage-files/gentoobinhost.conf -o /mnt/gentoo/etc/portage/binrepos.conf/gentoobinhost.conf```
22. ```wget https://raw.githubusercontent.com/centi07/gentoo-ps4/refs/heads/main/portage-files/xorg -o /mnt/gentoo/etc/portage/package.use/xorg```
23. ```wget https://raw.githubusercontent.com/centi07/gentoo-ps4/refs/heads/main/portage-files/ -o /mnt/gentoo/etc/portage/package.use/pipewire```
24. ```chroot .```
25. ```emerge-webrsync```
26. ```getuto```
27. ```emerge --sync```
28. ```emerge --ask --verbose eix eselect-repository dev-vcs/git networkmanager```
29. systemd: ```systemctl enable NetworkManager``` </br>
    openrc: ```rc-update add NetworkManager default```
30. ```wget https://github.com/feeRnt/ps4-linux-12xx/archive/refs/tags/v6.15.4__wifi_blkscrn.tar.gz -o /usr/src/ps4-linux.tar.gz```
31. ```tar xpf /usr/src/ps4-linux.tar.gz -C /usr/src/```
32. ```rm /usr/src/ps4-linux.tar.gz```
33. ```mv /usr/src/ (click tab) /usr/src/ps4-linux``` 
34. ```ln -s /usr/src/ps4-linux /usr/src/linux```  
36. ```eselect repository add ps4-overlay git https://github.com/centi07/ps4-overlay```
37. ```emaint sync -r ps4-overlay```
38. ```emerge -avDNu @world mesa libdrm xorg-drivers xorg-server```
39. ```passwd```
40. ```ln -sf /usr/share/zoneinfo/Yours/City /etc/localtime```
41. ```nano /etc/locale.gen```
42. ```locale-gen```
43. ```eselect locale list```
44. ```eselect locale set X```
45. ```emerge -a linux-firmware sysklogd chrony``` </br>
install only sysklogd if u use openrc desktop tarball
46.
    systemd: </br> 
        ```systemctl enable chronyd```  </br>
    openrc:  </br>
        1. ```rc-update add sysklogd default```  </br>
            2. ```rc-update add chronyd default```  </br>
47. ```useradd -m ps4linux```
48. ```usermod -aG wheel,audio,video,usb ps4linux```
49. ```passwd ps4linux```
50. ```emerge -a sudo```
51. ```echo "%wheel ALL=(ALL:ALL) NOPASSWD: ALL" >> /etc/sudoers``` </br>
well u can simply configure your system, on gentoo wiki you have more articles about installing xfce4 etc.