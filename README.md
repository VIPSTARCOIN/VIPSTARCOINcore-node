VIPSTARCOINCORE Node
============

A VIPSTARCOIN full node for building applications and services with Node.js. A node is extensible and can be configured to run additional services.

## Install

```bash
npm install -g VIPSTARCOINcore-node
VIPSTARCOINcore-node start
```

## Configuration

VIPSTARCOINCORE includes a Command Line Interface (CLI) for managing, configuring and interfacing with your VIPSTARCOINCORE Node.

```bash
VIPSTARCOINcore-node create -d <data-dir> mynode
cd mynode
VIPSTARCOINcore-node install <service>
VIPSTARCOINcore-node install https://github.com/yourname/helloworld
```

This will create a directory with configuration files for your node and install the necessary dependencies. For more information about (and developing) services, please see the [Service Documentation](docs/services.md).

## Add-on Services

There are several add-on services available to extend the functionality of VIPSTARCOINCORE:

- [VIPSTARCOIN Insight API](https://github.com/VIPSTARCOIN/VIPSTARCOIN-api)

## Contributing



## License
