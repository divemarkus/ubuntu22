# Ubuntu 22.04 Setup Guide for Machine Learning

This guide provides instructions to set up an Ubuntu 22.04 system optimized for machine learning tasks with NVIDIA GPU support.

## Table of Contents
1. [Prerequisites](#prerequisites)
2. [System Preparation](#system-preparation)
3. [Shell Customization](#shell-customization)
4. [NVIDIA Drivers and CUDA Setup](#nvidia-drivers-and-cuda-setup)
5. [Docker Installation](#docker-installation)
6. [LLM Runner Setup (Ollama)](#llm-runner-setup-ollama)
7. [Model Deployment](#model-deployment)
8. [Optional Tools and Projects](#optional-tools-and-projects)

---

## Prerequisites

### Remote Access Configuration
Enable SSH access to your system for remote management.

1. Update your system packages:
   ```bash
   sudo apt update && sudo apt upgrade
   ```

2. Install and enable the OpenSSH server:
   ```bash
   sudo apt install openssh-server -y
   sudo systemctl start ssh
   sudo systemctl enable ssh
   sudo systemctl status ssh
   ```

---

## System Preparation

### Basic Software Installation
Install essential tools for system monitoring and development:
```bash
sudo apt install curl git zsh wget btop nvtop htop neofetch konsole -y
```

---

## Shell Customization

Switch from Bash to Zsh for a more powerful shell experience.

1. Install Zsh:
   ```bash
   sudo apt install zsh -y
   ```

2. Change your default shell to Zsh:
   ```bash
   chsh -s $(which zsh)
   ```

3. Verify the change:
   ```bash
   echo $SHELL
   ```

4. Install Oh My Zsh and PowerLevel10k theme:
   - Visit [Oh My Zsh](https://ohmyz.sh/) for detailed instructions.
   - Clone the PowerLevel10k theme:
     ```bash
     git clone --depth=1 https://github.com/romkatv/powerlevel10k.git "$HOME/.oh-my-zsh/custom/themes/powerlevel10k"
     ```
   - Install Fonts:
     ```bash
     mkdir -p ~/.local/share/fonts
     cd ~/.local/share/fonts
     wget https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Regular.ttf
     wget https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold.ttf
     wget https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Italic.ttf
     wget https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold%20Italic.ttf
     ```

5. Configure Zsh settings in `~/.zshrc`:
   ```bash
   plugins=(git zsh-autosuggestions zsh-syntax-highlighting)
   ZSH_THEME="powerlevel10k/powerlevel10k"
   ```
   Apply changes:
   ```bash
   source ~/.zshrc
   fc-cache -fv
   p10k configure
   ```

---

## NVIDIA Drivers and CUDA Setup

### Install NVIDIA Drivers
```bash
sudo ubuntu-drivers install
nvidia-smi
```

### Install TensorRT (Optional)
```bash
sudo apt install tensorrt
```

Reboot your system to apply changes:
```bash
sudo reboot
```

---

## Docker Installation

Install Docker and necessary dependencies:
```bash
sudo apt update
sudo apt install -y ca-certificates curl gnupg lsb-release
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Add your user to the Docker group:
```bash
sudo usermod -aG docker $USER
```

---

## LLM Runner Setup (Ollama)

Install Ollama from their official website:
```bash
curl -fsSL https://ollama.ai/install.sh | sh
```

Run models locally using Docker:
- Example for a smaller model:
  ```bash
  docker exec -it ollama ollama run llama3.2
  ```
- Example for a larger model (requires sufficient resources):
  ```bash
  docker exec -it ollama ollama run deepseek-r1:14b
  ```

---

## Model Deployment

### Docker Deployment

Create a project directory and start your services:
```bash
mkdir -p ~/docker-stack && cd ~/docker-stack
```

Run the following command to deploy your containers:
```bash
docker compose up -d
```

Access your deployed services at:
- Open Web UI: `http://open-webui:8080`
- Frigate: `http://frigate:5000`
- Portainer: `http://portainer:9443`
- Netdata: `http://netdata:19999`
- Jellyfin: `http://jellyfin:8096`

---

## NVIDIA Container Toolkit

Install the NVIDIA Container Toolkit to leverage GPU resources in Docker:
```bash
curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg
curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#' | sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
sudo apt install -y nvidia-container-toolkit
sudo nvidia-ctk runtime configure --runtime=docker
sudo systemctl restart docker
```

Test GPU functionality in Docker:
```bash
docker run --rm --gpus all nvidia/cuda:12.3.2-runtime-ubuntu22.04 nvidia-smi
```

---

## Optional Tools and Projects

### Additional Commands
Monitor system resources:
```bash
watch -n 1 free -m
watch -n 1 nvidia-smi
htop
btop
nvtop
```

### Firewall Configuration (Internal Use Only)
```bash
sudo ufw status
sudo ufw allow ssh
```

---

## Projects

Install PyTorch and related libraries:
```bash
pip install torch torchvision torchaudio transformers
git clone https://github.com/yourusername/yourproject.git
cd yourproject && git checkout main
```

---

This guide provides a comprehensive setup for an Ubuntu 22.04 system tailored for machine learning tasks. Each section is designed to be clear and self-contained, allowing you to follow along easily.
