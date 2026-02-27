# ubuntu22
Ubuntu 22.04 Getting Started

# remote access
```
sudo apt update && sudo apt upgrade
sudo apt install openssh-server -y
sudo systemctl start ssh
sudo systemctl enable ssh
sudo systemctl status ssh
```

# basic installs
```
sudo apt install htop neofetch curl git-all zsh wget
```

# setup oh-my-zsh
+ https://ohmyz.sh/
```
fc-cache -fv
fc-list | grep -i "Nerd"
echo -e "\uf00c \uf015 \ue706 \uf17c"
p10k configure
source ~/.zshrc
```

# drivers
```
sudo ubuntu-drivers install
nvidia-smi
sudo apt install tensorrt
sudo reboot
```

# options
```
sudo apt install konsole

watch -n 1 free -m
watch -n 1 nvidia-smi

sudo apt install nvtop
nvtop

sudo apt install btop
btop
```

# firewall
```
sudo ufw allow ssh
sudo ufw enable
```

# projects
```
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
git clone https://github.com/comfyanonymous/ComfyUI
https://github.com/virattt/ai-hedge-fund
```
