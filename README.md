## 🚀 0G Galileo - Auto Install Script
This is an automated setup script for the 0G Galileo Validator Node, allowing you to run your node using any custom ports you want.
No manual configuration needed — the script does it all for you. 🛠️

## ⚙️ Version
v1.1.1 – Last updated: May 2025
Maintained by: coinsspor

🧩 One-Line Installation
Copy and paste this single line to begin installation:

```bash
bash <(wget -qO- https://raw.githubusercontent.com/coinsspor/0G-Galileo/main/autoinstal.sh)
```

## 🧠 The script handles everything — from installing dependencies to configuring ports and services.

## 📦 What This Script Does
Installs system dependencies (Go, git, curl, etc.)

Clones the official 0G Galileo repository

Initializes your node with a custom moniker

Sets up custom P2P and RPC ports

Configures the systemd service

Starts the validator node and displays logs

## Checks Logs

```bash
journalctl -u 0gchaind -u geth -f
```

## 
