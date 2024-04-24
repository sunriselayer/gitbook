# Development Environment

This is development environment to run Sunrise software.
This environment can be used for development, building binaries, and running nodes.

## Install Dependencies

### Ubuntu

```bash
sudo apt update
sudo apt install -y tar wget aria2 clang pkg-config libssl-dev jq build-essential git make ncdu
```

### Install Golang

Install Golang

```bash
wget https://go.dev/dl/go1.22.2.linux-amd64.tar.gz
sudo rm -rf /usr/local/go && sudo tar -C /usr/local -xzf go1.22.2.linux-amd64.tar.gz
rm go1.22.2.linux-amd64.tar.gz
echo "export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin" >> $HOME/.bashrc
source $HOME/.bashrc
```

Check Go version

```bash
go version
```
