---
layout: post
title: What's Jekyll?
---

[Jekyll](http://jekyllrb.com) is a static site generator, an open-source tool for creating simple yet powerful websites of all shapes and sizes. From [the project's readme](https://github.com/jekyll/jekyll/blob/master/README.markdown):

> Jekyll is a simple, blog aware, static site generator. It takes a template directory [...] and spits out a complete, static website suitable for serving with Apache or your favorite web server. This is also the engine behind GitHub Pages, which you can use to host your project’s page or blog right here from GitHub.

It's an immensely useful tool. Find out more by [visiting the project on GitHub](https://github.com/jekyll/jekyll).



buat partisi di hardisk
format partisi hardisk

=====singkatnya=====
mkdir --parents /mnt/gentoo
mount /dev/sda2 /mnt/gentoo (penyimpanan root)
date
chronyd -q
cd /mnt/gentoo
links www.google.com _cari gentoo download stage3 openrc amd64 hardened
tar xpvf stage3.tar.xz --xattrs-include='*.*' --numeric-owner
nano /mnt/gentoo/etc/portage/make.conf
ACCEPT_LICENSE
INPUT_DEVICES
VIDEO_CARDS
USE

mkdir --parents /mnt/gentoo/etc/portage/repos.conf
cp /mnt/gentoo/usr/share/portage/config/repos.conf /mnt/gentoo/etc/portage/repos.conf/gentoo.conf
cp --dereference /etc/resolv.conf /mnt/gentoo/etc/
mount --types proc /proc /mnt/gentoo/proc
mount --rbind /sys /mnt/gentoo/sys
mount --make-rslave /mnt/gentoo/sys
mount --rbind /dev /mnt/gentoo/dev
mount --make-rslave /mnt/gentoo/dev
mount --bind /run /mnt/gentoo/run
mount --make-slave /mnt/gentoo/run
chroot /mnt/gentoo /bin/bash
source /etc/profile
export PS1="(chroot) ${PS1}
mount /dev/sda1 /boot
emerge-webrsync
eselect news read
eselect profile list
eselect profile show
eselect profile set 1
emerge --ask --verbose --update --deep --newuse @world
emerge --ask app-portage/cpuid2cpuflags
echo "*/* $(cpuid2cpuflags)" > /etc/portage/package.use/00cpu-flags
echo "Asia/Jakarta" > /etc/timezone
emerge --config sys-libs/timezone-data
env-update
source /etc/profile
export PS1="(chroot) ${PS1}
emerge --ask sys-kernel/gentoo-sources sys-kernel/genkernel sys-kernel/linux-firmware
cd /usr/src/linux
make menuconfig
make && make modules_install && make install
genkernel --install --kernel-config=/usr/src/linux/.config initramfs
ls /boot/initramfs*
nano /etc/fstab
/dev/sda1 /boot vfat defaults 0 2
/dev/sda2 / xfs defaults,noatime 0 1
/dev/sda3 none swap sw 0 0

exho tux > /etc/hostname
nano /etc/hosts
127.0.0.1 tux.homenetwork tux localhost
passwd
useradd -m -G users.wheel,audio,video -s /bin/bash rezky
passwd rezky
emerge --ask sys-boot/grub
grub-install /dev/sda
grub-mkconfig -o /boot/grub/grub.cfg
exit
umount -l /mnt/gentoo/dev{/shm,/pts,}
umount -R /mnt/gentoo
reboot
cabut flashdisk
