---
aliases:
- OpenClaw/Clawdbot Setup
categories:
- '[[TechLearning]]'
tags:
- open-claw
---
**Reference Video:** [ClawdBot - Full Tutorial & Setup Guide (SECURE)](https://www.youtube.com/watch?v=tnsrnsy_Lus)
**Reference Video 2:** [Moltbot Beginners Setup Guide and Alternative for Free? - Praison AI and Multi-Agent Framework](https://www.youtube.com/watch?v=PleO6KKkfVo)
- VPS Provider: KVM2

## OpenClaw Basic Installation
### 1. Update and Install Dependencies
Debian is "slim" by default, so we need to make sure you have the basics for OpenClaw to run.
```bash
apt update && apt upgrade -y
apt install -y curl git build-essential
```


### 2. Install Node.js 22 (Required)
OpenClaw 2026 requires Node.js 22+. The default Debian version is usually too old.
```bash
curl -fsSL https://deb.nodesource.com/setup_22.x | bash -
apt install -y nodejs
```
_Verify with `node -v`. It should say `v22.x.x`._

### 3. Install OpenClaw
Run the official installer. This will install the CLI globally.
```bash
curl -fsSL https://openclaw.ai/install.sh | bash
```

### 4. Setup Onboarding
Run the onboarding command. 
```bash
openclaw onboard  
```
Follow the Quick Start approach and use default options. No need for hooks/skills etc.

### 5. Open TUI
Once onboarding is complete, open the terminal UI
```bash
openclaw tui
```
You should be able to interact with the LLM.

### 6. Setup Web UI
The onboarding completion output would have logged a "Dashboard Ready" block section with the info on how to setup the Web UI..

To get into the Web UI from your home computer, follow these steps:
#### Step 1: **Open a NEW terminal** on your local machine 
Do **not** use the one already logged into the VPS.
#### Step 2: Paste and run the command: 
   The **SSH command** provided below is a **Local Port Forwarding tunnel**.
```bash
ssh -N -L 18789:127.0.0.1:18789 root@76.13.183.191
```
 It essentially creates a secure "bridge" between your physical computer and your VPS so that when you type `localhost:18789` in your home browser, it safely routes the data to the VPS.
**Breakdown of the Command:**
- **`-L 18789:127.0.0.1:18789`**: This is the "magic" part. It tells your computer to listen on port `18789` and forward everything to the server's `127.0.0.1:18789`.  
- **`-N`**: This tells SSH "do not execute a remote command". It keeps the connection open purely for the tunnel without opening a new terminal prompt.
- **`root@76.13.183.191`**: This is your server's login info.
*Note: the web UI stays active until the local-port forwarding stays active in the terminal (i.e. step 1)*
#### Step 3: **Enter your root password** when prompted.
- _Note: The terminal will appear to "hang" or do nothing. This is normal; it means the tunnel is active._
#### Step 4: **Open your browser** and go to `http://localhost:18789`.
#### Step 5: **Use the Gateway Token**
If it asks for a token, go back to your VPS terminal and run `openclaw gateway token` to copy it.
Normally if you copy the link with the token i.e. `http://127.0.0.1:18789/#token=abc`, you'd not need to provide the gateway token.

## Security Measures
### Step 1: Create a Non-Root User (Foundation)

Running everything as `root` is dangerous because if the bot is ever compromised, the attacker has full control of your VPS.
1. **Create the user**: `adduser clawadmin` (Choose a password and hit Enter for the defaults)
2. **Grant sudo rights**: `usermod -aG sudo clawadmin`

---
#### Phase A: Prepare the New User
1. **Switch to your new user**:
```bash
su - clawadmin
```
2. **Verify Node.js is available**:
```bash
node -v
```  
  _(If it says "command not found," you may need to add the Node path to this user's `.bashrc` or reinstall Node globally as root first)._
#### Phase B: Install & Onboard as `clawadmin`
1. **Run the installer as the new user**:
```bash
curl -fsSL https://openclaw.ai/install.sh | bash
```
2. **Run Onboarding with the `--install-daemon` flag**:
```bash
openclaw onboard --install-daemon
```
_Choose the same **OpenRouter** settings. This will create a fresh, perfectly-permissioned `.openclaw` folder in `/home/clawadmin/`._





----
## TODOs:
- Set up SSH keys and disable password-based logins for your new user?
- Setup Docker and 4-layer security as in the Ansible playbook (See if its required for VPS system)
- Setup the SSH config to only dis-allow SSH through ROOT

