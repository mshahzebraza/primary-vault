---
original_path: Notes/Tech Learning/linux-pc-setup/Tools to install Post Linux Install.md
base: TechLearning
path_area: linux-pc-setup
categories:
- '[[TechLearning]]'
tags:
- linux-pc-setup
---
Create a script to setup all the applications

- How to make own script: https://www.youtube.com/watch?v=dePp5JFCyZ4
- Dev Env Setup: https://www.youtube.com/watch?v=hKGPH9C-EFc

| **Category**            | **Software**                | **Why Engineers Use It**                                      |
| ----------------------- | --------------------------- | ------------------------------------------------------------- |
| **API Testing**         | **Postman** or **Insomnia** | Testing your backend endpoints without a frontend.            |
| **DB Management**       | **DBeaver**                 | A "Swiss Army Knife" for seeing what's inside your databases. |
| **Notes/Documentation** | **Obsidian** or **Notion**  | Keeping track of complex engineering logic.                   |
| **System Monitor**      | **btop** or **htop**        | A much more powerful version of Windows Task Manager.         |
| **Communication**       | **Slack** / **Discord**     | Standard industry collaboration.                              |
| Password Management     | Keypass, BitWarden          |                                                               |
| Browser                 | Chrome, Brave, Zen          |                                                               |
| App Distribution        | Flatpack                    |                                                               |
| Terminal                | Bash, Warp, Zsh, Tmux       |                                                               |


```bash
#!/bin/bash

# Update and install system essentials
sudo apt update && sudo apt upgrade -y
sudo apt install -y git curl wget build-essential jq htop tldr zsh ufw

# Install VS Code
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > vscode.gpg
sudo install -o root -g root -m 644 vscode.gpg /etc/apt/trusted.gpg.d/
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'
sudo apt update && sudo apt install code -y

# Install Docker
sudo apt install -y docker.io
sudo usermod -aG docker $USER

# Install NVM (Node Version Manager)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

# Create an organized Workspace
mkdir -p ~/dev/{projects,lab,scripts}


# Finishing Things Up (Removing unnecessary packages and cached files)
## System Update and Upgrade
sudo apt update
sudo apt install --fix-missing -y
sudo apt upgrade --allow-downgrades -y
sudo apt full-upgrade --allow-downgrades -y
## System Clean Up
sudo apt install -f
sudo apt autoremove -y
sudo apt autoclean
sudo apt clean

```


- slack
- mongodb compass
- figma
- cursor
- work repo config and git linking (possible a cli)
- setup envs (preferably store in aws/gcloud secrets and download through cli)
- obsidian
- obsidian vaults/repo config and git-linking
- warp
- ghostty
- configure terminal
- brave
- postman
- git
- gh cli
- aws cli
- gcloud cli
- claude desktop
- termius
- docker
- node
- configure and setup secrets and credentials (e.g aws creds/ ssh profiles/ pat tokens etc) in obsidian (don't push to git; but create example files)
- tailscale
- anydesk
- antigravity
- bun
- pnpm
- mongotools