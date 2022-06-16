# ununifid Installation and Setup 

## Choose an Operating System
The operating system you use for your node is entirely your personal preference. You will be able to compile the junod daemon on most modern linux distributions and recent versions of macOS.
> For the tutorial, it is assumed that you are using an Ubuntu LTS release.
> If you have chosen a different operating system, you will need to modify your commands to suit your operating system.

## Install pre-requisites

***Update the local package list and install any available upgrades***
```
sudo apt-get update && sudo apt upgrade -y
```
***Install toolchain and ensure accurate time synchronization***
```
sudo apt-get install make build-essential gcc git jq chrony -y
```

***Install Go***
Please install Go v1.18 or later.
```
wget https://golang.org/dl/go1.18.2.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.18.2.linux-amd64.tar.gz
```

***Build Juno from source***
```
git clone https://github.com/CosmosContracts/juno
cd juno
git fetch
git checkout 3.0.0
make install
```
To confirm that the installation has succeeded, you can run:
```
junod version
```
If the result is *v3.0.0*, then you are finished setup and installed ununifid.
