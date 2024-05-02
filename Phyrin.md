<pre align="center">
  <h1><span>Phyrin / Pyrinhash</span> <img src="img/pyrin-logo.png" alt="Logo" width="25" height="25"></h1>
  <h>pyrin:qz7s9fa544jg4lsmc5r4wlugdz3dx5acjqfpw2vu0x8gu5077arxufa3dlgu7</h>
</pre>

## Wallets:

**Web-Wallet:** [Pyrin-Web-Wallet](https://wallet.pyrin.network/)

**Hot-Wallets:** [Official Wallet](https://github.com/Pyrinpyi/pyrin-desktop-wallet)


## Links:
[Pyrin Offical Website](https://pyrin.network/)

[Pyrin Github](https://github.com/Pyrinpyi/pyipad)


## Node Setup:

### Step 1

1. Fresh installation of Ubuntu 22.04 LTS
2. VPS must have min 80GB Storage, 4GB Ram 2 VCPU
3. Wait to boot

### Step 2

1. SSH into VPS:
    ```bash
    ssh root@127.0.0.1
    ```
2. Update & Install requirements:
    ```bash
    sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y

    sudo apt install unzip screen -y
    ```

3. Installing the Node:
  ```bash
  wget https://github.com/Pyrinpyi/pyipad/release/download/pyipad-*.**.*-linux.zip 

  unzip pyipad-*.**.*-linux.zip -d /usr/local/bin
  ```

4. Setup the daemon:
  ```bash
  vim /etc/systemd/system/pyripad.service
  
  
  [Unit]
  Description=Pyipad Service
  After=network.service

  [Service]
  User=pyiadmin
  WorkingDirectory=/home/pyiadmin
  ExecStart=/usr/local/bin/pyipad --utxoindex
  # optional items below
  Restart=always
  RestartSec=3

  [Install]
  WantedBy=multi-user.target
  ```
  
5. Start the daemon:
  ```bash
  sudo systemctl daemon-reload

  sudo systemctl enable pyripad.service

  sudo systemctl start pyripad.service

  sudo journalctl -u pyipad.service -n 1000 -f
  ```

### Step 3
1. Download and setup Stratum Bridge:
  ```bash
  wget https://github.com/Lolliedieb/lolMiner-releases/files/13695402/lol_bridge_pyi.tar.gz

  tar xfv lol_bridge_pyi.tar.gz

  screen -S bridge ./lol_bridge_pyi
  ```

2. Mining:
  - IP: `stratum+tcp://ip-of-server:5555`


### Miner Setup:

**[lolminer](https://github.com/Lolliedieb/lolMiner-releases/releases):**
```bash
./lolMiner --algo PYRIN --pool stratum+tcp://ip-of-server --user YOUR_PYRIN_WALLET_ADDRESS.YOUR_WORKER_NAME
```

**[Rigel](https://github.com/rigelminer/rigel/releases):**
```bash
./rigel -a pyrinhash -o stratum+tcp://ip-of-server -u YOUR_PYRIN_WALLET_ADDRESS -w YOUR_WORKER_NAME --log-file logs/miner.log
```