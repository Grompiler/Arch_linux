# Install Manjaro via GUI

# then use the script from the user sess as root
curl -LO https://raw.githubusercontent.com/Pioterr/Arch_linux/master/install.sh
sh install.sh

# manually if needed

- uncommment in /etc/pacman.conf
      [multilib]
      Include = /etc/pacman.d/mirrorlist
      
- verify nvidia config file '/etc/X11/xorg.conf' (sudo nvidia-settings)
or /etc/X11/mhwd.d/nvidia.conf if using manjaro
- configure (disable) discord auto startup
- rm -r .git (home folder)
- install rust # uncomment .bash_profile's rust line
- install jetbrains toolbox
- rustup component add rls rust-analysis rust-src rustfmt clippy
- set git global email to empty (commiting email not authorized): git config --global user.email '<>' (cf. file: ~/.gitconfig)
