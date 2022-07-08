install
```
npm i
```

start

```
npm run start
```


hosting files are [here](public)

---
## Install instruction

Clean up

```
sudo systemctl stop casper-node-launcher.service
sudo apt remove -y casper-client
sudo apt remove -y casper-node
sudo apt remove -y casper-node-launcher
sudo rm /etc/casper/casper-node-launcher-state.toml
sudo rm -rf /etc/casper/1_*
sudo rm -rf /var/lib/casper/*
```

Setup Casper Labs repo for packages

```
echo "deb https://repo.casperlabs.io/releases" bionic main | sudo tee -a /etc/apt/sources.list.d/casper.list
curl -O https://repo.casperlabs.io/casper-repo-pubkey.asc
sudo apt-key add casper-repo-pubkey.asc
sudo apt update
```

Install casper-node-launcher, casper-client, and jq

```
sudo apt install -y casper-client casper-node-launcher jq
```

Customize your protocols and host them on your server

```
https://github.com/casper-network/docs/pull/557/files
```
for example -> [here](public)

Copy your conf to network_configs

```
cd /etc/casper/network_configs
sudo -u casper curl -JLO <your server>/<working path>/mynetwork.conf
```

Install all protocols
```
sudo -u casper /etc/casper/node_util.py stage_protocols <your network name>.conf
```


Validator Keys
If you do not have keys, you can create them

```
sudo -u casper casper-client keygen /etc/casper/validator_keys
```

Start the node

```
sudo /etc/casper/node_util.py rotate_logs
sudo /etc/casper/node_util.py start
```


refer to 
https://github.com/casper-network/casper-node/wiki/Mainnet-Node-Installation-Instructions#install-casper-node-launcher-casper-client-and-jq