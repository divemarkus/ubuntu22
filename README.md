# Ubuntu22
- Ubuntu 22.04 Getting Started
- Assuming the system has NVIDIA GPU
- Focus on ML

### Remote access
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
- Warning: we are changing your default shell from bash to zsh
- Reverting back from zsh to bash and vice-versa is fairly easy
- Steps are to install ohmyzsh, nerdfonts, powerline10k theme, and edit source file '~/.zshrc'
```
fc-cache -fv
fc-list | grep -i "Nerd"
echo -e "\uf00c \uf015 \ue706 \uf17c"
p10k configure
source ~/.zshrc
```

### Drivers
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
```
sudo ufw allow ssh
sudo ufw enable
```

## Projects
```
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
git clone https://github.com/comfyanonymous/ComfyUI
https://github.com/virattt/ai-hedge-fund
```
