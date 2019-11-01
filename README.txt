# Arch Linux install steps

# check connection
# ping www.google.com

# check if efi boot is activated (should be)
ls /sys/firmware/efi/efivars

# show disk
lsblk

# open sdX disk to prepare it
cgdisk /dev/sdX
-> Name: boot, size 600 Mo, type: EFI System
-> Name: system, size: max - boot - swap, type: Linux filesystem
-> Name: swap, size: =RAM, type: Linux swap

# verif
lsblk

# format partitions
mkfs.fat -F32 /dev/sdX #boot
mkfs.ext4 /dev/sdX #system
mkswap /dev/sdX #swap
swapon /dev/sdX #swap

# mounting disk
mount /dev/sdX /mnt #system
mkdir /mnt/boot
mount /dev/sdX /mnt/boot #boot

# verif
df

# adapt mirror list
nano /etc/pacman.d/mirrorlist

# install base
pacstrap /mnt base base-devel
pacstrap /mnt git
?? pacstrap /mnt nano linux

# generate fstab
genfstab -U /mnt >> /mnt/etc/fstab

# verif
cat /mnt/etc/fstab

# chroot system
arch-chroot /mnt

# symlink for timezone
ln -sf /usr/share/zoneinfo/Europe/Paris /etc/localtime

# set hardware clock
hwclock --systohc

# uncomment alphabets you need
nano /etc/locale.gen

# and then generate
locale-gen

# set alphabet (assuming we uncommented us utf8)
echo "LANG=en_US.UTF-8" > /etc/locale.conf

# set machine's hostname
nano /etc/hostname # just type the name inside this file and save

# Configure /etc/mkinitcpio.conf
mkinitcpio -p linux

# set root password
passwd

# add and activate network
pacman -Syy networkmanager
systemctl enable NetworkManager

# add user and set password (can be done later)
# nano /etc/sudoers may be needed later for this user
useradd -g wheel -m pierre
passwd pierre

# install grub
pacman -S efibootmgr
pacman -S grub
grub-install /*--target=x86_64*/ --efi-directory=/boot --bootloader-id=GRUB

# if other OS on the disk, else do not need
pacman -S os-prober

# make grub config
grub-mkconfig -o /boot/grub/grub.cfg # should find linux image and initrd image in /boot/...

# resart computer
exit
umount -R /mnt
reboot


# log into user session and install yay
# install yay, aur package manager
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
# cd ..
# rm -r yay

# then use the script from the user sess as root
# curl -LO https://raw.githubusercontent.com/Pioterr/Arch_linux/master/install.sh
# sh install.sh

# installation:
# -cutter (binary to move in /bin)
# -hopper-v4
# (-vscode (material theme, +code base plugins))

# manually if needed
# verify nvidia config file '/etc/X11/xorg.conf'
# configure (disable) discord auto startup
