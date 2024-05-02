<pre align="center">
  <h1><span>Kaspa / Kheavyhash</span> <img src="img/kaspa-logo.png" alt="Logo" width="25" height="25"></h1>
  <h>kaspa:qqlrk5y9kzdru9z3zngh2p9zn8zd5nccnl8rnpn3u35u72xf84qd7wtm7xnqe</h>
</pre>

## Wallets:

**Web-Wallet:** [Kaspanet](https://wallet.kaspanet.io/)

**Hot-Wallets:** [Official Wallet](https://kdx.app/), [Kaspium](https://kaspium.io/)


## Links:
[Kaspa Offical Website](https://kaspa.org/)

[Kaspa Github](https://github.com/kaspanet/kaspad)


## Node Setup:

### Step 1

1. Fresh installation of Ubuntu 20.04 LTS
2. VPS must have min 80GB Storage, 4GB Ram 2 VCPU
3. Wait to boot

### Step 2

1. SSH into VPS:
    ```bash
    ssh root@127.0.0.1
    ```
2. Update & Install requirements:
    ```bash
    sudo apt update
    sudo apt upgrade -y
    sudo apt-get install ca-certificates curl git
    gnupg
    sudo apt-get update
    sudo mkdir -p /etc/apt/keyrings

    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

    echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

    sudo apt update
    sudo apt upgrade -y
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
    ```

3. Installing the Node:
    ```bash
    sudo docker run --pull always -d --restart unless-stopped -p 16110:16110 -p 16111:16111 --name kaspad supertypo/kaspad:latest

    ```
4. Check the Progress:
    ```bash
     sudo docker logs -n 100 -f kaspad
    ```
### Step 3

1. Download Stratum Bridge:
    ```bash
    git clone https://github.com/onemorebsmith/kaspa-stratum-bridge.git
    
    cd kaspa-stratum-bridge
    ```
2. Setup Stratum Bridge with Grafana:
    ```bash
    sudo docker compose -f docker-compose-all.yml up -d
    ```
3. Visit Grafana:

    - ip-of-server:3000
    - Default creds: `admin-admin`

4. Mining:
    - IP: `stratum+tcp://ip-of-server:5555`