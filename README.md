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

## Node Status

```bash
curl -s localhost:<RPCPORT>/status | jq .result.sync_info
```

## Checks Logs

```bash
journalctl -u 0gchaind -u geth -f
```

## Check Bloks
```bash
#!/bin/bash

# 0gchaind için config dosyasından RPC portunu çek
rpc_port=$(grep -m 1 -oP '^laddr = "\K[^"]+' "$HOME/.0gchaind/0g-home/0gchaind-home/config/config.toml" | cut -d ':' -f 3)

while true; do
  local_height=$(curl -s http://localhost:$rpc_port/status | jq -r '.result.sync_info.latest_block_height')
  network_height=$(curl -s https://0g-rpc-galileo.coinsspor.com/status | jq -r '.result.sync_info.latest_block_height')

  if ! [[ "$local_height" =~ ^[0-9]+$ ]] || ! [[ "$network_height" =~ ^[0-9]+$ ]]; then
    echo -e "\033[1;31mError: Invalid block height data. Retrying...\033[0m"
    sleep 5
    continue
  fi

  blocks_left=$((network_height - local_height))
  echo -e "\033[1;33mNode Height:\033[1;34m $local_height\033[0m \033[1;33m| Network Height:\033[1;36m $network_height\033[0m \033[1;33m| Blocks Left:\033[1;31m $blocks_left\033[0m"
  sleep 5
done
```


