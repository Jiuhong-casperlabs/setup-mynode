## Clean up
```
sudo systemctl stop casper-node-launcher.service
sudo apt remove -y casper-client
sudo apt remove -y casper-node
sudo apt remove -y casper-node-launcher
sudo rm /etc/casper/casper-node-launcher-state.toml
sudo rm -rf /etc/casper/1_*
sudo rm -rf /var/lib/casper/*
```
## Setup Casper Labs repo for packages
```
echo "deb https://repo.casperlabs.io/releases" bionic main | sudo tee -a /etc/apt/sources.list.d/casper.list
curl -O https://repo.casperlabs.io/casper-repo-pubkey.asc
sudo apt-key add casper-repo-pubkey.asc
sudo apt update
```
## Install casper-node-launcher, casper-client, and jq
```
sudo apt install -y casper-client casper-node-launcher jq
```
## Install all protocols

*replace serverdomain with your domain name*

*replace mynetworkname with your network name*

*replace mynetwork.conf with your conf name*
```
cd /etc/casper/network_configs
sudo -u casper curl -JLO serverdomain/mynetworkname/mynetwork.conf
sudo -u casper /etc/casper/node_util.py stage_protocols mynetwork.conf
```
## Validator Keys
If you do not have keys, you can create them
```
sudo -u casper casper-client keygen /etc/casper/validator_keys
```

## CA certificates 

https://docs.casperlabs.io/workflow/setup-private-network/#network-access-control

For example:
config.toml
```
[network.identity]
tls_certificate = "/etc/casper/keys/node_1_cert.pem"
secret_key = "/etc/casper/keys/node_1.pem"
ca_certificate = "/etc/casper/keys/ca_cert.pem"
```
The certificates accessrights should be like this:
```
-rw-rw-r-- 1 casper casper 891 Oct 19 05:45 ca_cert.pem
-rw------- 1 casper casper 436 Oct 19 05:46 node_1.pem
-rw-rw-r-- 1 casper casper 774 Oct 19 05:47 node_1_cert.pem
```
The accessrights for path should be like this
```
drwxr-xr-x 7 casper casper 4096 Oct 21 02:47 keys
```

## Get a trusted hash

*replace 16.162.124.124 with your validator ip address*
```
sudo sed -i "/trusted_hash =/c\trusted_hash = '$(casper-client get-block --node-address http://16.162.124.124:7777 -b 20 | jq -r .result.block.hash | tr -d '\n')'" /etc/casper/1_0_0/config.toml
```
## Start the node
```
sudo /etc/casper/node_util.py rotate_logs
sudo /etc/casper/node_util.py start
```
## Monitor the node syncing
```
/etc/casper/node_util.py watch
```
