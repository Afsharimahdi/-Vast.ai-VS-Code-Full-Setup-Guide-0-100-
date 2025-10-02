# 🚀 Full Guide: Connect Vast.ai GPU Instances to VS Code (0 → 100)

This repository contains a step-by-step guide (from zero to hero) on how to connect a **Vast.ai GPU instance** with **VS Code** using SSH.  
It includes full details, commands, configuration, and troubleshooting tips.  

---

## 📌 Table of Contents
1. Introduction
2. Step 1: Create an Instance on Vast.ai
3. Step 2: Prepare Local Environment
4. Step 3: Generate SSH Key
5. Step 4: Add SSH Key to Vast.ai
6. Step 5: Test SSH Connection
7. Step 6: Configure SSH Config File
8. Step 7: Connect with VS Code
9. Step 8: Install Python + Jupyter on Server
10. Step 9: Run Jupyter via Port Forwarding
11. Step 10: Manage Your Instance
12. Quick Checklist

---

## 📖 Introduction
Vast.ai provides GPU instances at affordable prices.  
To code efficiently, we connect the remote server directly to **VS Code** via SSH, so you can:  
- Run code on remote GPU 🚀  
- Edit files in VS Code 📝  
- Use Jupyter Notebook locally via port forwarding 📊  

---

## 🔹 Step 1: Create an Instance on Vast.ai
1. Go to [vast.ai](https://vast.ai).  
2. Sign up / log in.  
3. Navigate to **Create Instance**.  
4. Select GPU, RAM, CPU, Storage (e.g. RTX 3060 Ti, 8GB VRAM).  
5. Click **Rent**.  
6. Once created, check it under **Instances** → You'll see options like **SSH** and **Jupyter**.  

---

## 🔹 Step 2: Prepare Local Environment
### Install Tools on Windows
- [VS Code](https://code.visualstudio.com/)  
- [Git Bash](https://git-scm.com/download/win) (includes SSH)  

### Install VS Code Extensions
- **Remote - SSH**  
- **Jupyter** (optional)  

---

## 🔹 Step 3: Generate SSH Key
Open **Git Bash** and run:
```bash
ssh-keygen -t rsa -b 2048 -C "your_email"
```

- Save location → press Enter (default: `C:\Users\USERNAME\.ssh\id_rsa`).  
- Passphrase → press Enter (empty).  

Keys created:  
- `id_rsa` → private key (keep safe).  
- `id_rsa.pub` → public key (share with Vast.ai).  

View public key:
```bash
cat ~/.ssh/id_rsa.pub
```

---

## 🔹 Step 4: Add SSH Key to Vast.ai
1. Go to Vast.ai → **Account → SSH Keys**.  
2. Click **Add Key**.  
3. Paste the full content of `id_rsa.pub`.  
4. Save.  

---

## 🔹 Step 5: Test SSH Connection
From Vast.ai **Instances**, copy SSH command. Example:
```bash
ssh -p 28305 root@121.122.125.126
```

Run in Git Bash:  
- First time → type `yes` to trust host.  
- If key setup is correct → you’ll be logged in.  

Test GPU:
```bash
nvidia-smi
```

---

## 🔹 Step 6: Configure SSH Config File
📂 Path on Windows:  
```
C:\Users\USERNAME\.ssh\config
```

Add entry:
```ssh-config
Host vast
    HostName 121.122.125.126
    User root
    Port 28305
    IdentityFile C:/Users/USERNAME/.ssh/id_rsa
    LocalForward 8080 localhost:8080
```

---

## 🔹 Step 7: Connect with VS Code
1. Open VS Code.  
2. Press `Ctrl+Shift+P`.  
3. Select **Remote-SSH: Connect to Host**.  
4. Choose `vast`.  
5. A new VS Code window opens → connected to your server 🎉  

---

## 🔹 Step 8: Install Python + Jupyter on Server
Update & install pip:
```bash
apt update && apt install -y python3-pip
```

Install PyTorch:
```bash
pip install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu121
```

Install Jupyter:
```bash
pip install jupyterlab
```

---

## 🔹 Step 9: Run Jupyter via Port Forwarding
Start Jupyter:
```bash
jupyter lab --no-browser --port=8080
```

On your local browser:
```
http://localhost:8080
```

---

## 🔹 Step 10: Manage Your Instance
- After finishing → **Stop** or **Destroy** instance in Vast.ai.  
- Cost is billed **per active hour**.  
- Always save your work before stopping.  

---

## ✅ Quick Checklist
```bash
ssh-keygen -t rsa -b 2048 -C "your_email"
cat ~/.ssh/id_rsa.pub   # Copy to Vast.ai → Account → SSH Keys

ssh -p 28305 root@121.122.125.126
nvidia-smi   # Check GPU

# VS Code Config
Host vast
    HostName 121.122.135.426
    User root
    Port 28305
    IdentityFile C:/Users/USERNAME/.ssh/id_rsa
    LocalForward 8080 localhost:8080

# Python + Jupyter
apt update && apt install -y python3-pip
pip install torch torchvision torchaudio
pip install jupyterlab
jupyter lab --no-browser --port=8080
```