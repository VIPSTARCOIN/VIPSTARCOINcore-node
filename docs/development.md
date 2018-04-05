# Setting up Development Environment

## Install Node.js

Install Node.js by your favorite method, or use Node Version Manager by following directions at https://github.com/creationix/nvm

```bash
nvm install v4
```

## Fork and Download Repositories

To develop VIPSTARCOINcore-node:

```bash
cd ~
git clone git@github.com:<yourusername>/VIPSTARCOINcore-node.git
git clone git@github.com:<yourusername>/VIPSTARCOIN-lib.git
```

To develop VIPSTARCOIN or to compile from source:

```bash
git clone git@github.com:<yourusername>/VIPSTARCOIN.git
git fetch origin <branchname>:<branchname>
git checkout <branchname>
```
**Note**: See VIPSTARCOIN documentation for building VIPSTARCOIN on your platform.


## Install Development Dependencies

For Ubuntu:
```bash
sudo apt-get install libzmq3-dev
sudo apt-get install build-essential
```
**Note**: Make sure that libzmq-dev is not installed, it should be removed when installing libzmq3-dev.


For Mac OS X:
```bash
brew install zeromq
```

## Install and Symlink

```bash
cd bitcore-lib
npm install
cd ../bitcore-node
npm install
```
**Note**: If you get a message about not being able to download VIPSTARCOIN distribution, you'll need to compile VIPSTARCOINd from source, and setup your configuration to use that version.


We now will setup symlinks in `VIPSTARCOINcore-node` *(repeat this for any other modules you're planning on developing)*:
```bash
cd node_modules
rm -rf VIPSTARCOIN-lib
ln -s ~/VIPSTARCOIN-lib
rm -rf VIPSTARCOINd-rpc
ln -s ~/VIPSTARCOINd-rpc
```

And if you're compiling or developing VIPSTARCOIN:
```bash
cd ../bin
ln -sf ~/VIPSTARCOIN/src/VIPSTARCOINd
```

## Run Tests

If you do not already have mocha installed:
```bash
npm install mocha -g
```

To run all test suites:
```bash
cd VIPSTARCOINcore-node
npm run regtest
npm run test
```

To run a specific unit test in watch mode:
```bash
mocha -w -R spec test/services/VIPSTARCOINd.unit.js
```

To run a specific regtest:
```bash
mocha -R spec regtest/VIPSTARCOINd.js
```

## Running a Development Node

To test running the node, you can setup a configuration that will specify development versions of all of the services:

```bash
cd ~
mkdir devnode
cd devnode
mkdir node_modules
touch VIPSTARCOINcore-node.json
touch package.json
```

Edit `VIPSTARCOINcore-node.json` with something similar to:
```json
{
  "network": "livenet",
  "port": 3001,
  "services": [
    "VIPSTARCOINd",
    "web",
    "VIPSTARCOIN-api",
    "insight-ui",
    "<additional_service>"
  ],
  "servicesConfig": {
    "VIPSTARCOINd": {
      "spawn": {
        "datadir": "/home/<youruser>/.VIPSTARCOIN",
        "exec": "/home/<youruser>/VIPSTARCOIN/src/VIPSTARCOINd"
      }
    }
  }
}
```

**Note**: To install services [VIPSTARCOIN-api](https://github.com/VIPSTARCOIN/VIPSTARCOIN-api) you'll need to clone the repositories locally.

Setup symlinks for all of the services and dependencies:

```bash
cd node_modules
ln -s ~/VIPSTARCOIN-lib
ln -s ~/VIPSTARCOINcore-node
ln -s ~/VIPSTARCOIN-api
```

Make sure that the `<datadir>/VIPSTARCOIN.conf` has the necessary settings, for example:
```
server=1
whitelist=127.0.0.1
txindex=1
addressindex=1
timestampindex=1
spentindex=1
zmqpubrawtx=tcp://127.0.0.1:28332
zmqpubhashblock=tcp://127.0.0.1:28332
rpcallowip=127.0.0.1
rpcuser=user
rpcpassword=password
rpcport=18332
reindex=1
gen=0
addrindex=1
logevents=1
```

From within the `devnode` directory with the configuration file, start the node:
```bash
../VIPSTARCOINcore-node/bin/VIPSTARCOINcore-node start
```