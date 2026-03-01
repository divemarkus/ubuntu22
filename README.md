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
sudo apt install curl git zsh wget btop nvtop htop neofetch konsole
```

### Optional > [skip to Drivers](https://github.com/divemarkus/ubuntu22?tab=readme-ov-file#drivers)
#### [Setup oh-my-zsh](https://ohmyz.sh/)
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
- Once completed, you will need to load the font 'fc-cache' run 'p10 configure' to finalize the look and feel
- You can run 'p10 configure' as many times as you want, changing fonts/themes/etc
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

### LLM runner like Ollama or LM Studio
- There's several to discuss, but the easiest is Ollama
- Go to their Web site and install
```
curl -fsSL https://ollama.com/install.sh | sh
```
- https://lmstudio.ai

### Docker
- Install Docker
```
sudo apt update

sudo apt install -y \
ca-certificates \
curl \
gnupg \
lsb-release

sudo install -m 0755 -d /etc/apt/keyrings

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

sudo usermod -aG docker $USER
```

### NVIDIA Container Toolkit
- Install NVIDIA Container Toolkit
```
curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | \
sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg

curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | \
sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list

sudo apt install -y nvidia-container-toolkit

sudo nvidia-ctk runtime configure --runtime=docker

sudo systemctl restart docker
```
- Test GPU inside Docker
```
docker run --rm --gpus all nvidia/cuda:12.3.2-runtime-ubuntu22.04 nvidia-smi
```

### Docker Deployment
- Create project directory and change directory
```
mkdir -p ~/docker-stack
cd ~/docker-stack
```
- When everything is ready, feel free to clone or run docker-compose.yml file in this repo
```
docker compose up -d
```
- This may take sometime. Get your Web Browsers ready and test remote (using your ip address)
```
http://open-webui:8080
http://frigate:5000
http://portainer:9443
http://netdata:19999
http://jellyfin:8096
```

### Run models locally (preferred)
- You can pick list of models from Ollama's Web site
- Here's an example 'llam3.2'
```
docker exec -it ollama ollama run llama3.2
```
- Here's a bigger model. Heads-up, make sure you have enough RAM/VRAM
```
docker exec -it ollama ollama run deepseek-r1:14b
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

### Firewall
- For internal use, firewall can be disabled
- Segment this device, behind an enterprise-class or same feature sets
```
sudo ufw status
sudo ufw allow ssh
```

### Tools
+ https://geminicli.com/
+ https://opencode.ai/
+ https://claude.ai/
+ https://openclaw.ai/

### Projects
```
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
git clone https://github.com/comfyanonymous/ComfyUI
https://github.com/virattt/ai-hedge-fund
```
