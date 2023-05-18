# UnUniFi Installation and Setup

Instruction to install the ununifid binary

## Choose an Operating System

The operating system you use for your node is entirely your personal preference. You will be able to compile the ununifid daemon on most modern linux distributions and recent versions of macOS
> For the tutorial, it is assumed that you are using an Ubuntu LTS release.
> If you have chosen a different operating system, you will need to modify your commands to suit your operating system.

## Requirements

Validator Node Server

- OS: Ubuntu 20.04
- Memory: 8 GB or more
- Storage: SSD 160 GB or more
- The following ports: `26656` must be open for peer to peer communication between nodes.

## Install pre-requisites

```Bash
# update the local package list and install any available upgrades
sudo apt update && sudo apt upgrade -y
# install toolchain and ensure accurate time synchronization
sudo apt install build-essential git jq -y
```

## Install Go

Follow the instructions [here](https://go.dev/doc/install) to install Go.
For an Ubuntu LTS, you can probably use:

```Bash
# Please install Go v1.19
# from $HOME dir
$ wget https://go.dev/dl/go1.19.linux-amd64.tar.gz
$ sudo rm -rf /usr/local/go
$ sudo tar -C /usr/local -xzf go1.19.linux-amd64.tar.gz
$ go version
go version go1.19 linux/amd64
```

Unless you want to configure in a non standard way, then set these in the `.bash_profile` in the user's `home` (i.e. ~/) folder.

```Bash
echo "export GOROOT=/usr/local/go" >> ~/.bash_profile
echo "export GOPATH=$HOME/go" >> ~/.bash_profile
echo "export GO111MODULE=on" >> ~/.bash_profile
echo "export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin" >> ~/.bash_profile
```

After updating your `~/.bash_profile` you will need to source it:

```Bash
source ~/.bash_profile
```

## Build UnUniFi from source

Clone the UnUniFi blockchain repository, check out the given branch, and build it with `make install` to build binaries.

```Bash
# from $HOME dir
git clone https://github.com/UnUniFi/chain chain_repo  
cd chain_repo
git checkout v2.0.0
make install
```

To confirm that the installation has succeeded, you can run:

```Bash
ununifid version
```
