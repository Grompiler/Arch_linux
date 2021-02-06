# Arch Linux install steps
# etcher tool for usb live creation with iso

# check connection
# ping www.google.com

# check if efi boot is activated (should be)
ls /sys/firmware/efi/efivars

# show disk
lsblk

# open sdX disk to prepare it
cgdisk /dev/sdX
-> Name: boot, size 300 Mo, type: EFI System
-> Name: system, size: max - boot - swap, type: Linux filesystem
#no need -> Name: swap, size: =RAM, type: Linux swap

# verif
lsblk

# format partitions
mkfs.fat -F32 /dev/sdX #boot
mkfs.ext4 /dev/sdX #system
# mkswap /dev/sdX #swap
# swapon /dev/sdX #swap

# mounting disk
mount /dev/sdX /mnt #system


# verif
df

# adapt mirror list
nano /etc/pacman.d/mirrorlist

# install base
pacstrap /mnt base base-devel
pacstrap /mnt git
pacstrap /mnt linux linux-firmware
pacstrap /mnt vim


# generate fstab
genfstab -U /mnt >> /mnt/etc/fstab

# verif
cat /mnt/etc/fstab

# chroot system
arch-chroot /mnt

# Use timedatectl to ensure the system clock is accurate
timedatectl set-ntp true
timedatectl status

# set timezone
timedatectl set-timezone "Europe/Paris"
timedatectl status

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

# set hosts
nano /etc/hosts
127.0.0.1	localhost
::1		localhost
127.0.1.1	myhostname.localdomain	myhostname

# Configure /etc/mkinitcpio.conf
# mkinitcpio -p linux

# set root password
passwd

# add and activate network
pacman -S networkmanager
systemctl enable NetworkManager

# add user and set password (can be done later)
# nano /etc/sudoers may be needed later for this user
useradd -g wheel -m pierre
passwd pierre

# install grub
pacman -S grub
pacman -S efibootmgr dosfstools mtools os-prober

mkdir /boot/EFI
mount /dev/sda1 /boot/EFI #boot

grub-install --target=x86_64-efi --bootloader-id=grub_uefi --recheck

# make grub config
grub-mkconfig -o /boot/grub/grub.cfg # should find linux image and initrd image in /boot/...

# resart computer
exit
umount -R /mnt
reboot

# then use the script from the user sess as root
curl -LO https://raw.githubusercontent.com/Pioterr/Arch_linux/master/install.sh
sh install.sh

# installation:
# -cutter (binary to move in /bin)
# -hopper-v4
# (-vscode (material theme, +code base plugins))

# manually if needed
# wine winetricks
-- uncommment in /etc/pacman.conf
      [multilib]
      Include = /etc/pacman.d/mirrorlist
# verify nvidia config file '/etc/X11/xorg.conf' (sudo nvidia-settings)
# configure (disable) discord auto startup
# rm -r .git (home folder)
# set theme in .config/gtk-3.0 #gtk-application-prefer-dark-theme=true
# install rust # uncomment .bash_profile's rust line
# install jetbrains toolbox
# installer vim plug
# curl -fLo ~/.local/share/nvim/site/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
# installer les composants pour coder en rust sous nvim
# rustup component add rls rust-analysis rust-src
# set git global email to empty (commiting email not authorized): git config --global user.email '<>' (cf. file: ~/.gitconfig)
# to see git diffs with vim -> git difftool <file> or git d <file>
# git config --global diff.tool vimdiff
# git config --global difftool.prompt false
# git config --global alias.d difftool
# haskell (sudo pacman -S ghc cabal-install stack) stack is to haskell what cargo is to rust + VSCode plugin
