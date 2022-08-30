install according to doc
```
cargo install --git https://github.com/casper-network/casper-node/ --tag private-1.4.6 global-state-update-gen
sudo cp /home/ubuntu/.cargo/bin/global-state-update-gen /usr/bin/
cd /usr/bin
sudo chmod 755 /usr/bin/global-state-update-gen

sudo -u casper global-state-update-gen generate-admins  \
--data-dir /var/lib/casper/casper-node/mynetwork   \
--state-hash e0729172d1411bc634e3e7a1295d55cc1bee55678e48ec3f2bde00a819d306c0   \
--admin 0124f6d669b8b231b60e1616662f74e887f6ec75ede61257b93bed8de027bb7b22,1000000000000001>/tmp/global_state.toml
```


1.0.2 version:


casper-client transfer \
--id 1 \
--transfer-id 123456789012345 \
--node-address http://localhost:7777 \
--amount 2500000000 \
--secret-key /Users/jh/keys/test1/secret_key.pem \
--chain-name casper \
--target-account 01230de4bd0922cd08e190fd0c87cc36ee5dd0282d5289a7422efcdd44f683df69 \
--payment-amount 10000


admins:
0152836c51eac04205bb7febe9d92da50758178b0bf388bd03e1da13147b99e2c5,
balance: 1000000000000000000000026138374205
0193b3800386aefe11648150f6779158f2c7e1233c8e9b423338eb71b93ae6c5a9
balance: 999999999999999999996016526756255

validators:
"public_key": "0124f6d669b8b231b60e1616662f74e887f6ec75ede61257b93bed8de027bb7b22", 1
"public_key": "01867a43b8a73dd47a58eb605f651e24f4bc531522cc9663879607821cdc454dd6", 3
"public_key": "019d6115e57ec65c1d53b52fec83ac9d5b019c99f6f225ab065f440a959b2735eb", 2


git push heroku main
heroku logs --tail

curl -s http://mypn.herokuapp.com//mynetwork/protocol_versions



unzip:
tar -xf public/mynetwork/1_0_0/config.tar.gz -C test/v1
update configs
...
zip:
tar -czvf public/mynetwork/1_0_0/config.tar.gz  -C test/v1 .

test
tar -xf public/mynetwork/1_0_0/config.tar.gz -C testcheck/v1