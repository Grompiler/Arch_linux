# Install Manjaro via GUI

- install rust via rustup # uncomment .bash_profile's rust line
- uncommment in /etc/pacman.conf
      [multilib]
      Include = /etc/pacman.d/mirrorlist
- install paru https://github.com/Morganamilo/paru
- verify nvidia config file '/etc/X11/xorg.conf' (sudo nvidia-settings)
or /etc/X11/mhwd.d/nvidia.conf if using manjaro
- configure (disable) discord auto startup
- rm -r .git (home folder)
- install jetbrains toolbox
- rustup component add rls rust-analysis rust-src rustfmt clippy
- cargo install cargo-watch
- set git global email to empty (commiting email not authorized): git config --global user.email '<>' (cf. file: ~/.gitconfig)
