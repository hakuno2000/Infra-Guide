# Running as root user
`sudo -i`

# Install Go
```
wget https://golang.org/dl/go1.20.12.linux-amd64.tar.gz
tar -C /usr -xzf go1.20.12.linux-amd64.tar.gz
```

# Add to ~/.profile at end
```
export GOROOT=/usr/bin/go
export PATH=$PATH:/usr/go/bin:$HOME/go/bin
```

# Install node (for example is Cosmos)
compile from source
```
apt install make
apt install gcc
git clone https://github.com/cosmos/gaia
cd gaia
git checkout v14.1.0
make install
```
or download binary file
```
wget -O /root/go/bin/gaiad https://github.com/cosmos/gaia/releases/download/v14.1.0/gaiad-v14.1.0-linux-amd64
chmod +x /root/go/bin/gaiad
```

# Init node
```
gaiad init YOUR_MONIKER --chain-id cosmoshub-4
```
YOUR_MONIKER is the name you want to name your node

# Download genesis
```
wget -O genesis.json https://snapshots.polkachu.com/genesis/cosmos/genesis.json --inet4-only
mv genesis.json ~/.gaia/config
```

# Download addressbook
```
wget -O addrbook.json https://snapshots.polkachu.com/addrbook/cosmos/addrbook.json --inet4-only
mv addrbook.json ~/.gaia/config
```

# Get snapshot
```
wget -O cosmos_18331310.tar.lz4 https://snapshots.polkachu.com/snapshots/cosmos/cosmos_18331310.tar.lz4 --inet4-only
apt install lz4
lz4 -c -d cosmos_18331310.tar.lz4  | tar -x -C ~/.gaia
```
Without snapshot or statesync, you will have to run node from block 0 and need a lot of time to catch up current block.

# Start node
`gaiad start --p2p.laddr tcp://0.0.0.0:1000 --rpc.laddr tcp://127.0.0.1:1001 --grpc.address 127.0.0.1:1002 --grpc-web.address 127.0.0.1:1003`
