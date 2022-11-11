New Validators are going to take effect at era n.

Instruction:

```
.Wait until era n starts.
.Read the state root hash from the last block in era n-1.
.Stop the network.
.Generate global_state.toml using the state root hash from the last block of era n-1.
.Set the chainspec activation point and last_emergency_restart to era n, and hard_reset to true (it's usually set this way by default) - this would make the network revert to the end of era n-1 when it is restarted with the upgrade.
.Stage the upgrade (that is, copy the chainspecs, configs and binaries for new version(for example, 1.0.1) where they should be) - still while the network is down.
.Restart the network with nodes staged for the upgrade.
```
Step1:

.Wait until era n starts.

Step2:

.Read the state root hash from the last block in era n-1.

Step3:

.Stop the network (stop all nodes).

Step4: 

.Issue the following command on one node and put it on xx/public/mynetwork/1_0_1/config.tar.gz. This file should be exactly the same on each node.

For example:
```
sudo ./global-state-update-gen validators \
-d /var/lib/casper/casper-node/mynetwork \
-s d4aa05afc7475472a5f038fac9776c31cd37c606c9abda08931f5a9e471f0abc \
-v "0124f6d669b8b231b60e1616662f74e887f6ec75ede61257b93bed8de027bb7b22,1000000000000001" \
-v "019d6115e57ec65c1d53b52fec83ac9d5b019c99f6f225ab065f440a959b2735eb,1000000000000002" \
-v "01867a43b8a73dd47a58eb605f651e24f4bc531522cc9663879607821cdc454dd6,1000000000000003" \
-v "0104fdfc180afc5fb007e428d17f058ddd15aa9036e3cccd31e4215f3efcdbc591,1000000000000004"> /tmp/global_state.toml
```

note:

```
-s : the state-root-hash of era n-1
-v : all the validators in era n
```

Location: put it the same location with the staged files.

For example:
```
ubuntu@worker1:/etc/casper/1_0_1$ ls -l
total 52
-rw-r--r-- 1 casper casper   904 Aug 30 12:54 accounts.toml
-rw-r--r-- 1 casper casper 11492 Aug 30 14:14 chainspec.toml
-rw-r--r-- 1 casper casper 12818 Aug 30 12:54 config-example.toml
-rw-rw-r-- 1 casper casper 12820 Aug 30 14:33 config.toml
-rw-rw-r-- 1 casper casper   734 Aug 30 14:37 global_state.toml
```

Step5:

.Set the chainspec activation point and last_emergency_restart to era n, and hard_reset to true.

For example:
```
version = '1.0.1'
hard_reset = true
activation_point = 1
last_emergency_restart = 1
```

Step6:

.Stage the upgrade (that is, copy the chainspecs, configs and binaries for new version(for example, 1.0.1) where they should be) - still while the network is down.


step7: 

.Restart the network with nodes staged for the upgrade.
