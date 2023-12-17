# Install Manjaro with proprietary drivers via GUI (stop wasting time)
- set network accessible for all users
- copy dot files
- install rustup
- install paru https://github.com/Morganamilo/paru
- install via pacman : firefox-developer-edition ttf-jetbrains-mono gdb base-devel picom dmenu fzf fish ripgrep libimobiledevice tree sxiv unclutter feh polybar zathura net-tools kitty xorg-xrandr fd emacs cmake docker gimp maim  xclip (nvidia-settings)
- insatll via paru : discord leftwm (leftwm-theme (& leftwm-theme update / install "Ascent" & add conf) or download conf from git & symlink Ascent conf as `current`) and run `leftwm-check`
- configure (disable) discord auto startup
- install jetbrains toolbox
- install doom https://github.com/doomemacs/doomemacs
- symlink doom executable in /bin: sudo ln -s ~/.config/emacs/bin/doom /bin/
- rustup component add rls rust-analyzer rust-analysis rust-src rustfmt clippy
- cargo install cargo-watch cargo-expand
- set git global email to empty (commiting email not authorized): git config --global user.email '<>' (cf. file: ~/.gitconfig)
- turn off notification sound
