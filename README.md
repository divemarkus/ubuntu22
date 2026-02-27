# Ubuntu22
- Ubuntu 22.04 Getting Started
- Assuming the system has NVIDIA GPU
- Focus on ML

### Remote access
- Once you install, enable ssh, make sure to edit sshd_conf file to add line 'permitrootlogin no'
```
sudo apt update && sudo apt upgrade
sudo apt install openssh-server -y
sudo systemctl start ssh
sudo systemctl enable ssh
sudo systemctl status ssh
```

### Basic installs
```
sudo apt install htop neofetch curl git-all zsh wget btop nvtop konsole
```

### [Setup oh-my-zsh](https://ohmyz.sh/)
- Give Robbie Russell a visit & tip
- https://github.com/ohmyzsh/ohmyzsh/wiki
- Make sure you're working on '~/' directory so when you git clone, the files are on the correct path
- Steps are to install ohmyzsh, nerdfonts, powerline10k theme, and edit source file '~/.zshrc'
- It is also highly encouraged to install plugins, 'zsh-autosuggestions' and 'zsh-syntax-highlighting'
- Warning! we are changing your default shell from bash to zsh
```
chsh -s $(which zsh)
```
- Verify
```
echo $SHELL
```
- Install both plugins
```
git clone https://github.com/zsh-users/zsh-autosuggestions.git $ZSH_CUSTOM/plugins/zsh-autosuggestion
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
```
- NerdFonts and PowerLevel10k has their own repo. Follow instructions to installs
- [PowerLevel10](https://github.com/romkatv/powerlevel10k?tab=readme-ov-file#oh-my-zsh)
- [NerdFonts](https://github.com/ryanoasis/nerd-fonts)
- Here's what I did (see below, if you don't want to mess with reading both repo's above, skipping nerdfonts):
```
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git "${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k"

mkdir -p ~/.local/share/fonts\ncd ~/.local/share/fonts\n\nwget https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Regular.ttf\nwget https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold.ttf\nwget https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Italic.ttf\nwget https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold%20Italic.tt
```
- Make sure both theme and fonts are installed
- Once installed, you will need to edit '~/.zshrc' to change theme from robbyrussell to powerlevel10k/powerlevel10k, and add plugins
```
#ZSH_THEME="robbyrussell"
ZSH_THEME="powerlevel10k/powerlevel10k"

plugins=(git zsh-autosuggestions zsh-syntax-highlighting)
```
- Then load the fonts, so your Terminal or Konsole can see them
- Click on Terminal or Konsole, your default profile and load the desired font. If you only installed Meslo, then that's what you get
- Once completed, you will need to run 'p10 configure' to finalize the look and feel. You can run this as many times as you want, changing fonts/themes/etc
```
source ~/.zshrc
fc-cache -fv
fc-list | grep -i "Meslo"
echo -e "\uf00c \uf015 \ue706 \uf17c"
p10k configure
```

### Drivers
- We are assuming you have NVIDIA graphics card
```
sudo ubuntu-drivers install
nvidia-smi
sudo apt install tensorrt
sudo reboot
```

### Command-lines
- Some of our most used commands
```
watch -n 1 free -m
watch -n 1 nvidia-smi
htop
btop
nvtop
```

## Firewall
- For internal use, firewall can be disabled
- Segment this device, behind an enterprise-class or same feature sets
```
sudo ufw status
sudo ufw allow ssh
```

## Projects
```
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
git clone https://github.com/comfyanonymous/ComfyUI
https://github.com/virattt/ai-hedge-fund
```
