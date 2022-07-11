## STEP1  Customize your protocols and host them on your server


https://github.com/casper-network/docs/blob/dev/source/docs/casper/workflow/staging-files-for-new-network.md

The file structure is like this 

```
└── mynetwork
    ├── 1_0_0
    │   ├── bin.tar.gz                -> source code of casper-node
    │   └── config.tar.gz             -> configuration files you have to customize. unzip -> customize -> zip
    ├── mynetwork.conf                -> the file to be copied in `Copy your conf to network_configs` of next step
    └── protocol_versions             -> version of your node. For new launch network, there is only 1 version.
```
*notes:*

*`mynetwork` is an example for network name, please replace with your network name.*

*`bin.tar.gz` and `config.tar.gz` are from https://github.com/casper-network/casper-node/releases/tag/private-1.4.6*

*mynetwork.conf*

```
SOURCE_URL= <your domain name of this server>
NETWORK_NAME=mynetwork
```

*protocol_versions*

```
1_0_0
```

### **You have to start your server before next step!**

Example for completed server: 

```
git clone https://github.com/Jiuhong-casperlabs/setup-mynode.git

cd setup-mynode

npm i

npm run start
```

Check if the server starts successfully:

Issue this command 
```
curl -s http://<domain name>/<network name>/protocol_versions
```
for example, `curl -s http://localhost:3000/mynetwork/protocol_versions`

output should be
```
1_0_0
```

---
## STEP2 Install private network node

Clean up

```
sudo systemctl stop casper-node-launcher.service
sudo apt remove -y casper-client
sudo apt remove -y casper-node
sudo apt remove -y casper-node-launcher
sudo rm /etc/casper/casper-node-launcher-state.toml
sudo rm -rf /etc/casper/*
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

Copy your conf to network_configs

```
cd /etc/casper/network_configs
sudo -u casper curl -JLO <your server>/<working path>/<your network name>.conf
```

Install all protocols 

For launching new network there should be only 1 protocol like 1_0_0

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
https://github.com/casper-network/casper-node/wiki/Mainnet-Node-Installation-Instructions