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
sudo apt install htop neofetch curl git-all zsh wget btop nvtop
```

### [Setup oh-my-zsh](https://ohmyz.sh/)
- Give Robbie Russell a visit & tip
- https://github.com/ohmyzsh/ohmyzsh/wiki
- Steps are to install ohmyzsh, nerdfonts, powerline10k theme, and edit source file '~/.zshrc'
- It is also highly encouraged to install plugins, 'zsh-autosuggestions' and 'zsh-syntax-highlighting'
- Warning: we are changing your default shell from bash to zsh
```
chsh -s $(which zsh)
```
- Verify
```
echo $SHELL
```
- NerdFonts and PowerLevel10k has their own repo. Follow instructions to installs
- [PowerLevel10](https://github.com/romkatv/powerlevel10k?tab=readme-ov-file#oh-my-zsh)
- [NerdFonts](https://github.com/ryanoasis/nerd-fonts)
- Make sure both theme and fonts are installed
- Once installed, you will need to edit '~/.zshrc' to change theme from robbyrussell to powerlevel10k/powerlevel10k, and add plugins
```
#ZSH_THEME="robbyrussell"
ZSH_THEME="powerlevel10k/powerlevel10k"

plugins=(git zsh-autosuggestions zsh-syntax-highlighting)
```
- Then load the fonts, so your Terminal or Konsole can see them
- Click on Terminal or Konsole, your default profile and load the desired font (there's many, pick one)
```
fc-cache -fv
fc-list | grep -i "Nerd"
echo -e "\uf00c \uf015 \ue706 \uf17c"
p10k configure
source ~/.zshrc
```

### Drivers
- We are assuming you have NVIDIA graphics card
```
sudo ubuntu-drivers install
nvidia-smi
sudo apt install tensorrt
sudo reboot
```

### Options
```
sudo apt install konsole

watch -n 1 free -m
watch -n 1 nvidia-smi
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
