# Proof of the Data Availability Layer

Sunrise's Data Availability Layer is validated by validators. Validators must validate data that may not be valid and send the proofs to chain.

This section describes how validators prove data.

## Proof

The only data that require proof are those that have been sent MsgSubmitInvalidity and the status has been changed to `CHALLENGING`.

The threshold for `CHALLENGING` is when MsgSubmitInvalidity is sent for 33% (the default in genesis) of the entire shards.

The validator is then validated. If more than a certain number of shards are proved, the status changes to `VERIFIED` as usual. If not, the status changes to `REJECTED`.

See [Data Availability](../../learn/sunrise/data-availability.md) for status and proof of data in the Data Availability Layer.

## Sunrise-Data for Validator

sunrise-data provides validators with the functions to monitor and prove data that has become `CHALLENGING`.

### Register proof deputy of your validator

Although validators can send tx themselves to send proof data, it is recommended to use a deputy address to prevent leakage of keys.

```bash
sunrised tx da register-proof-deputy <deputy_address> --from <your_validator_key>
```

To register you need to send a transaction with the validator key only once on `sunrised`.
Register the address of the deputy to be used on `sunrise-data`.

### How to set up

1. Running `sunrised` as a validator
See [Validator Node](../../node/types/consensus/validator-node.md) for setting up.

1. Clone sunrise-data repo

   ```bash
   cd ~
   git clone https://github.com/sunriselayer/sunrise-data.git
   cd sunrise-data
   make install
   ```

1. Create and edit `config.toml`

   ```bash
   cp config.default.toml config.toml
   vi config.toml
   ```

   To connect to a local IPFS daemon, leave the `ipfs_api_url` field empty

   Change `home_path` to your .sunrise directory, `proof_deputy_account` to your sunrised key's name and `validator_address` to your validator address.

   ```toml
   [api]
   port = 8000
   ipfs_api_url = ""
   ipfs_address_info = ""

   [chain]
   address_prefix="sunrise"
   home_path="/home/ubuntu/.sunrise"
   keyring_backend="test"
   sunrised_rpc="http://localhost:26657"
   
   [validator]
    proof_deputy_account="your_deputy_account"
    validator_address="sunrisevaloper1a8jcsmla6heu99ldtazc27dna4qcd4jyv75vcz"
    proof_fees="10000urise"
    proof_interval=5
   ```

### Run IPFS on local

1. Run IPFS

   ```bash
   wget https://dist.ipfs.tech/kubo/v0.31.0/kubo_v0.31.0_linux-amd64.tar.gz
   tar -xvzf kubo_v0.31.0_linux-amd64.tar.gz
   cd kubo
   sudo ./install.sh
   ipfs init --profile=lowpower
   ipfs daemon
   ```

1. Check the IPFS node ID and optionally share and add a remote peer

   ```bash
   ipfs id
   ```

### Start to proof data

On your sunrise-data directory,

```bash
sunrise-data validator
```

Or register as a service

```bash
vi /etc/systemd/system/sunrise-data.service
systemctl enable sunrise-data
systemctl start sunrise-data
```

```service
[Unit]
Description = sunrise-data validator daemon
After=network-online.target

[Service]
User=ubuntu
WorkingDirectory=/home/ubuntu/sunrise-data
ExecStart = /home/ubuntu/go/bin/sunrise-data validator
Restart=on-failure
RestartSec=3
LimitNOFILE=1400000

[Install]
WantedBy = multi-user.target
```

If the setup is successful, the display will look like this

```bash
$ sunrise-data validator
{"level":"info","time":"2025-02-19T18:32:52+09:00","message":"Starting validator task"}
{"level":"info","time":"2025-02-19T18:32:52+09:00","message":"validator: sunrisevaloper1a8jcsmla6heu99ldtazc27dna4qcd4jyv75vcz deputy: sunrise155u042u8wk3al32h3vzxu989jj76k4zcc6d03n"}
{"level":"info","time":"2025-02-19T18:32:52+09:00","message":"On-chain data is checked every 5 sec"}
```
