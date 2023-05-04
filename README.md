# Install Manjaro with proprietary drivers via GUI
- install firefox-developer-edition
- install rust via rustup
- uncommment in /etc/pacman.conf
      [multilib]
      Include = /etc/pacman.d/mirrorlist
- install paru https://github.com/Morganamilo/paru
- install via pacman : ttf-jetbrains-mono gdb picom dmenu fzf fish ripgrep libimobiledevice tree sxiv unclutter feh polybar zathura net-tools kitty (nvidia-settings)
- insatll via paru : discord leftwm leftwm-theme
- verify nvidia config file '/etc/X11/xorg.conf' (sudo nvidia-settings)
or /etc/X11/mhwd.d/nvidia.conf if using manjaro
- configure (disable) discord auto startup
- install jetbrains toolbox
- rustup component add rls rust-analyzer rust-analysis rust-src rustfmt clippy
- cargo install cargo-watch
- set git global email to empty (commiting email not authorized): git config --global user.email '<>' (cf. file: ~/.gitconfig)
