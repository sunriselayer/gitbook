# Setup Cosmovisor

**For mainnet, it's recommended to use Cosmovisor to run your node.**

Setting up Cosmovisor is relatively straightforward. However, it does expect certain environment variables and folder structure to be set.\
Cosmovisor allows you to download binaries ahead of time for chain upgrades, meaning that you can do zero (or close to zero) downtime chain upgrades. It's also useful if your local timezone means that a chain upgrade will fall at a bad time.\
Rather than having to do stressful ops tasks late at night, it's always better if you can automate them away, and that's what Cosmovisor tries to do.

## Install

First, go and get cosmovisor (recommended approach):

```Bash
# to target a specific version:
go install github.com/cosmos/cosmos-sdk/cosmovisor/cmd/cosmovisor@v1.0.0
```

### Add environment variables to your shell

Some environment variables must be set to appropriate values for each node and each network.

```Bash
echo "export CHAIN_REPO=https://github.com/sunriselayer/sunrise" >> ~/.bash_profile
echo "export CHAIN_REPO_BRANCHE=main" >> ~/.bash_profile
echo "export TARGET=sunrised" >> ~/.bash_profile
echo "export TARGET_HOME=.sunrise" >> ~/.bash_profile
# This value will be different for each node.
echo "export MONIKER=<your-moniker>" >> ~/.bash_profile
# This value is example of mainnet.
echo "export CHAIN_ID=sunrise-1" >> ~/.bash_profile
echo "export GENESIS_FILE_URL=https://raw.githubusercontent.com/sunriselayer/network/main/sunrise-1/genesis.json" >> ~/.bash_profile
echo "export SETUP_NODE_CONFIG_ENV=TRUE" >> ~/.bash_profile
echo "export SETUP_NODE_ENV=TRUE" >> ~/.bash_profile
echo "export SETUP_NODE_MASTER=TRUE" >> ~/.bash_profile
echo "export DAEMON_NAME=\$TARGET" >> ~/.bash_profile
# This value will be different for each node.
echo "export DAEMON_HOME=$HOME/.sunrise" >> ~/.bash_profile
echo "export DAEMON_ALLOW_DOWNLOAD_BINARIES=true" >> ~/.bash_profile
echo "export DAEMON_LOG_BUFFER_SIZE=512" >> ~/.bash_profile
echo "export DAEMON_RESTART_AFTER_UPGRADE=true" >> ~/.bash_profile
echo "export UNSAFE_SKIP_BACKUP=true" >> ~/.bash_profile
```

Then source your profile to have access to these variables:

```Bash
source ~/.bash_profile
```

### Set up folder structure

```Bash
mkdir -p $DAEMON_HOME/cosmovisor
mkdir -p $DAEMON_HOME/cosmovisor/genesis
mkdir -p $DAEMON_HOME/cosmovisor/genesis/bin
mkdir -p $DAEMON_HOME/cosmovisor/upgrades
```

### Set up genesis binary

Cosmovisor needs to know which binary to use at genesis. We put this in `$DAEMON_HOME/cosmovisor/genesis/bin`

Check [our Github](https://github.com/sunriselayer/network) to know the binary version of genesis.

```Bash
wget https://github.com/sunriselayer/sunrise/releases/download/<version>/sunrised
cp sunrised $DAEMON_HOME/cosmovisor/genesis/bin
```

### Set up service

Commands sent to Cosmovisor are sent to the underlying binary. For example, `cosmovisor version` is the same as typing `sunrised version`. Nevertheless, just as we would manage `sunrised` using a process manager, we would like to make sure Cosmovisor is automatically restarted if something happens, for example, an error or reboot. First, create the service file:

```Bash
sudo vi /lib/systemd/system/cosmovisor.service
```

Change the contents of the below to match your setup

```Bash
[Unit]
Description=Cosmovisor daemon
After=network-online.target
[Service]
Environment="DAEMON_NAME=sunrised"
Environment="DAEMON_HOME=/home/<your-user>/.sunrise"
Environment="DAEMON_RESTART_AFTER_UPGRADE=true"
Environment="DAEMON_ALLOW_DOWNLOAD_BINARIES=true" // Recommend
Environment="DAEMON_LOG_BUFFER_SIZE=512"
Environment="UNSAFE_SKIP_BACKUP=true"
User=<your-user>
ExecStart=/home/<your-user>/go/bin/cosmovisor start
Restart=always
RestartSec=3
LimitNOFILE=infinity
LimitNPROC=infinity
[Install]
WantedBy=multi-user.target
```

{% hint style="info" %}
A description of what the environment variables do can be found [here](https://docs.cosmos.network/main/run-node/cosmovisor.html). Change them depending on your setup.
{% endhint %}

### Start Cosmovisor

{% hint style="warning" %}
If syncing from a snapshot, do not start Cosmovisor yet. Download the snapshot and extract it to `$HOME/.sunrise/data`. Finally, enable the service and start it.
{% endhint %}

```Bash
sudo systemctl daemon-reload
sudo systemctl restart systemd-journald
sudo systemctl enable cosmovisor
sudo systemctl start cosmovisor
```

Check it is running using:

```Bash
sudo systemctl status cosmovisor
```

If you need to monitor the service after launch, you can view the logs using:

```Bash
sudo journalctl -u cosmovisor -f -o cat
```
