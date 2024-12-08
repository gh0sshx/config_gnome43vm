# Parrot Sec OS 6

## INSTALL

**Change hostname**

    hostnamectl set-hostname ParrotSecOS

> change parrot -> WMParrotOS in /etc/hosts

**Update and change kernel**

    sudo apt update && sudo parrot-upgrade -y
>
    sudo apt autoremove

> check kernel

    uname -a
>
    sudo reboot
>
    sudo apt update && sudo parrot-upgrade -y

**Fix update kernel**

    sudo apt remove linux-headers-6.5.<version>parrot1-amd64
>
    sudo apt remove linux-headers-amd64
>
    sudo apt remove linux-image-6.5.<version>parrot1-amd64
>
    sudo apt remove linux-image-amd64
>
    sudo update-initramfs -c -k 6.5.<version>parrot1-amd64
>
    sudo update-grub
>
    sudo apt autoremove

**GNOME**

    sudo apt install evolution
>
    sudo apt install gnome-core
>
    sudo apt install gnome-tweaks

## FIRST

**UPDATE**

    sudo apt update && sudo parrot-upgrade -y
>
    sudo apt install tilix

**fix search in gnome**

> disable search in settings and change position of windows titlebars

**Move app between workspaces**

    gsettings set org.gnome.desktop.wm.keybindings move-to-workspace-right "['<Super><Alt>Right']"    
>
    gsettings set org.gnome.desktop.wm.keybindings move-to-workspace-left "['<Super><Alt>Left']"

**Switch workspaces**

    gsettings set org.gnome.desktop.wm.keybindings switch-to-workspace-left "['<Ctrl><Super>Left']"
>
    gsettings set org.gnome.desktop.wm.keybindings switch-to-workspace-right "['<Ctrl><Super>Right']"

> Change rest of shorcuts in settings

**Oh my zsh**

    sudo apt install zsh
>
    sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

**ZSH syntax and kali color**

    git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ~/.oh-my-zsh/plugins/zsh-syntax-highlighting
>
    nano ~/.oh-my-zsh/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
>
    ZSH_HIGHLIGHT_HIGHLIGHTERS=(main brackets pattern)
    ZSH_HIGHLIGHT_STYLES[default]=none
    ZSH_HIGHLIGHT_STYLES[unknown-token]=fg=white,underline
    ZSH_HIGHLIGHT_STYLES[reserved-word]=fg=cyan,bold
    ZSH_HIGHLIGHT_STYLES[suffix-alias]=fg=green,underline
    ZSH_HIGHLIGHT_STYLES[global-alias]=fg=green,bold
    ZSH_HIGHLIGHT_STYLES[precommand]=fg=green,underline
    ZSH_HIGHLIGHT_STYLES[commandseparator]=fg=blue,bold
    ZSH_HIGHLIGHT_STYLES[autodirectory]=fg=green,underline
    ZSH_HIGHLIGHT_STYLES[path]=bold
    ZSH_HIGHLIGHT_STYLES[path_pathseparator]=
    ZSH_HIGHLIGHT_STYLES[path_prefix_pathseparator]=
    ZSH_HIGHLIGHT_STYLES[globbing]=fg=blue,bold
    ZSH_HIGHLIGHT_STYLES[history-expansion]=fg=blue,bold
    ZSH_HIGHLIGHT_STYLES[command-substitution]=none
    ZSH_HIGHLIGHT_STYLES[command-substitution-delimiter]=fg=magenta,bold
    ZSH_HIGHLIGHT_STYLES[process-substitution]=none
    ZSH_HIGHLIGHT_STYLES[process-substitution-delimiter]=fg=magenta,bold
    ZSH_HIGHLIGHT_STYLES[single-hyphen-option]=fg=green
    ZSH_HIGHLIGHT_STYLES[double-hyphen-option]=fg=green
    ZSH_HIGHLIGHT_STYLES[back-quoted-argument]=none
    ZSH_HIGHLIGHT_STYLES[back-quoted-argument-delimiter]=fg=blue,bold
    ZSH_HIGHLIGHT_STYLES[single-quoted-argument]=fg=yellow
    ZSH_HIGHLIGHT_STYLES[double-quoted-argument]=fg=yellow
    ZSH_HIGHLIGHT_STYLES[dollar-quoted-argument]=fg=yellow
    ZSH_HIGHLIGHT_STYLES[rc-quote]=fg=magenta
    ZSH_HIGHLIGHT_STYLES[dollar-double-quoted-argument]=fg=magenta,bold
    ZSH_HIGHLIGHT_STYLES[back-double-quoted-argument]=fg=magenta,bold
    ZSH_HIGHLIGHT_STYLES[back-dollar-quoted-argument]=fg=magenta,bold
    ZSH_HIGHLIGHT_STYLES[assign]=none
    ZSH_HIGHLIGHT_STYLES[redirection]=fg=blue,bold
    ZSH_HIGHLIGHT_STYLES[comment]=fg=black,bold
    ZSH_HIGHLIGHT_STYLES[named-fd]=none
    ZSH_HIGHLIGHT_STYLES[numeric-fd]=none
    ZSH_HIGHLIGHT_STYLES[arg0]=fg=cyan
    ZSH_HIGHLIGHT_STYLES[bracket-error]=fg=red,bold
    ZSH_HIGHLIGHT_STYLES[bracket-level-1]=fg=blue,bold
    ZSH_HIGHLIGHT_STYLES[bracket-level-2]=fg=green,bold
    ZSH_HIGHLIGHT_STYLES[bracket-level-3]=fg=magenta,bold
    ZSH_HIGHLIGHT_STYLES[bracket-level-4]=fg=yellow,bold
    ZSH_HIGHLIGHT_STYLES[bracket-level-5]=fg=cyan,bold
    ZSH_HIGHLIGHT_STYLES[cursor-matchingbracket]=standout

> enable plugin .zshrc

    plugins=(git sudo zsh-syntax-highlighting)

**keep directory**

    #inherit directory
        if [ $TILIX_ID ] || [ $VTE_VERSION ]; then
        source /etc/profile.d/vte.sh
    fi

>
    sudo ln -s /etc/profile.d/vte-2.91.sh /etc/profile.d/vte.sh

**Folders**

    mkdir {$HOME/VPN,$HOME/Machines}
>

**config  target**

    # set target
    function set_target(){
        read target
        echo $target > <path>
    }

**Configure Fonts**

> Download from https://www.nerdfonts.com/font-downloads

    unzip NerdFontsSymbolsOnly.zip -d NerdFonts
>
    mkdir ~/.local/share/fonts
>
    cp NerdFonts/* ~/.local/share/fonts
>
    fc-cache -f -v

**FIREFOX EXTENSION**

    foxyproxy
> 
    ublockorigin
> 
    darkreader
> 
    wappalyzer
> 
    simple translate
> 
    gnome extension

**GNOME EXTENSION**

    Caffeine
>
    Executor
>
    Just Perfection
>
    Workspace Indicator
>
    [QSTweak] Quick Setting Tweaker
>

**EXECUTOR**

> target

    if [[ $(cat /home/ghost/Machines/.target) == "" ]]; then echo "  ---.---.---.---"; else echo " 󰣉 " && cat /home/ghost/Machines/.target; fi && echo " | "

> VPN

    if [[ $(ip -4 addr show tun0 2>&1) == *"does not exist." ]]; then echo " tun0 󱘖 Offline"; else echo " tun0 󰌘 " && ip -4 addr show tun0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}'; fi && echo " | "    

> LAN0

    if [[ $(ip addr show dev eth0 | grep 'inet ' | awk '{print $2}' | cut -f1 -d'/') == "" ]]; then echo " eth0󰈂"; else echo " eth0 󰈀 " && ip -4 addr show eth0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}'; fi && echo " | "

> LAN1

    if [[ $(ip addr show dev eth1 | grep 'inet ' | awk '{print $2}' | cut -f1 -d'/') == "" ]]; then echo " eth1󰈂"; else echo " eth1 󰈀 " && ip -4 addr show eth1 | grep -oP '(?<=inet\s)\d+(\.\d+){3}'; fi && echo " | "    

> WIFI

    if [[ $(ip addr show dev wlan0 | grep 'inet ' | awk '{print $2}' | cut -f1 -d'/') == "" ]]; then echo " wlan0󰖪"; else echo " wlan0 󱚻 " && ip -4 addr show wlan0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}';fi && echo " "

> HOSTNAME

    echo "<OS-NERDFONT>"; cat /etc/hostname

**Disable network interface naming automapping**

> Edit file

    sudo nano /etc/default/grub

> find the line starting with 'GRUB_CMDLINE_LINUX_DEFAULT' and add at the end before closing the quotes

    net.ifnames=0
>
    sudo update-grub
>
    sudo ln -s /dev/null /etc/systemd/network/99-default.link1



## APPARIENCE

**MARBLE theme as Shell theme and Colloid as Legacy app theme**

**make file to save alias in zsh**

    mkdir -p ~/.config/zsh && touch ~/.config/zsh/alias.zsh

> edit ~/.zshrc and add**

    source ~/.config/zsh/alias.zsh

**color in ls**

    sudo apt install lsd

> edit ~/.zshrc and add**

    command -v lsd > /dev/null && alias ls='lsd --group-dirs first' && \
        alias tree='lsd --tree'

**color in nano**

    echo "include /usr/share/nano/*.nanorc\nset saveonexit" > ~/.nanorc

**color in cat with bat**

    sudo apt install bat
>
    batcat --generate-config-file

> add alias

    # Alias => batcat
    alias bcat="batcat"

> edit file generated by "--generate-config-file" and change to

    --paging=never

**Change FONTS**

> Download fonts.zip from this git in resources

> decompress

    unzip -d fonts fonts

> copy folder fonts and paste in $HOME/.local/share/

**FONT CONFIGURATION**

    Interface Text => SF Pro Display Regular 10
    Document Text => SF Pro Display Regular 10
    Monospace Text => FiraCode Nerd Font Mono Retina 10
    Legacy Window Titles => SF Pro Display Medium 11











