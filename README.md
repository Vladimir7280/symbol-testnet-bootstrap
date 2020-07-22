# Symbol Testnet Bootstrap (server 0.9.6.x)

Automated setup to deploy and manage Symbol testnet nodes.

## Update notes

*Warning*: This is for supporting 0.9.6.x server versions of the Symbol test network deployments. If you have been running a node on ANY previous version you need to start from a fresh environment and redeploy your new node from a clean state. With new network setups as usual any account(s) you might have been using on the old network will have no balance if moving to a new network.

To clean up your environment if moving from a previous test network setup you can follow these steps.

If you were running a peer node:

```
1) Change to peer-assembly directory
2) Stop running services (run command "docker-compose down")
3) Change to outside the testnet bootstrap tool directory
3) Delete directory  symbol-testnet-bootstrap/  OR catapult-testnet-bootstrap/  (if coming from the older generation) 
4) Delete your image cache by running "docker system prune -a"  (confirm "y" if prompted)
```

If you were running an api node:

```
1) Change to api-harvest-assembly directory
2) Stop running services (run command "docker-compose down")
3) Change to outside the testnet bootstrap tool directory
3) Delete directory  symbol-testnet-bootstrap/  OR catapult-testnet-bootstrap/  (if coming from the older generation) 
4) Delete your image cache by running "docker system prune -a"  (confirm "y" if prompted)
```

Over time as you upgrade to new versions old versions can take up space on disk.
If you run into disk issues b/c of this you can delete all old versions by running `docker system prune -a` which will ask you to confirm `y/n`. 

*Note*: This will delete all cached docker images so if you are doing any development with other images it will delete those as well and you will have to re-download.
 
## Environment requirements

The setup scripts are automated using docker. To run a test net node, you will need to have installed the following docker tools:

* [docker](https://docs.docker.com/install/#server)
* [docker-compose](https://docs.docker.com/compose/install/#install-compose)

*Note*:The release images target modern x86 architectures. It has been reported that errors are experienced on some older machines provided. If you run into any related issues, please report in the [slack group (#help)][slack].

## Installation

1. Download the [latest release](https://github.com/nemgrouplimited/symbol-testnet-bootstrap) of the package, or clone the repository directly using Git.

```
git clone https://github.com/nemgrouplimited/symbol-testnet-bootstrap.git
```

2. Choose the assembly distribution to install.

```
cd symbol-testnet-bootstrap/api-harvest-assembly
```

or...

```
cd symbol-testnet-bootstrap/api-assembly
```

or...

```
cd symbol-testnet-bootstrap/peer-assembly
```

In short, if you want to be able to interact with your node, you need to run the API assembly.
On the other hand, if you want a node dedicated exclusively confirm transactions, deploy the peer assembly.
You can read more about each assembly [here](node).

3. Run the node with docker-compose.

```
sudo docker-compose up --build --detach
```

You should see docker downloading the container images for the first time. Then it should run the setup and finally startup the service.

To stop all the running services, run ``sudo docker-compose down`` in the same directory you executed the ``up`` command.

## Peer assembly 

The Peer assembly will set up a [Peer](https://nemtech.github.io/concepts/node.html#peer-node) only node.

*Note*: The server needs to have port 7900 open and available to connect to else it will not be able to connect with other nodes in the network.

## API harvest assembly 

The API harvest assembly will set up a Dual purpose [API](https://nemtech.github.io/concepts/node.html#api-node) and [Peer](https://nemtech.github.io/concepts/node.html#peer-node) node, as well as the [REST gateway](https://nemtech.github.io/concepts/node.html#rest-gateway) that transactions can be submitted to and data read from.

You can verify that the node is running by opening a new browser tab with the following URL: ``localhost:3000/chain/height``.

*Note*: The software should expose the port ``3000`` by default. If you cannot access the REST Gateway from outside, it might mean that the port is closed by default by your machine or hosting provider so you will have to open it in order to access from outside the machine.

## API assembly

The API assembly will set up an api node that just serves as a gateway for transaction submissions and information requests from the network.

## Contributing

Contributions are welcome and appreciated. 
Check [CONTRIBUTING](CONTRIBUTING.md) for information on how to contribute.

## Getting help

- [symbol-testnet-bootstrap documentation][docs]
- Join the community [slack group (#sig-testing)][slack] 
- If you found a bug, please [open a new issue][issues]

## License

Copyright 2019-present NEM Foundation

Licensed under the [Apache License 2.0](LICENSE)

[self]: https://github.com/nemgrouplimited/symbol-testnet-bootstrap
[docs]: http://nemtech.github.io/guides/network/running-a-test-net-node.html
[node]: https://nemtech.github.io/concepts/node.html
[issues]: https://github.com/nemgrouplimited/symbol-testnet-bootstrap/issues
[slack]: https://join.slack.com/t/nem2/shared_invite/enQtMzY4MDc2NTg0ODgyLWZmZWRiMjViYTVhZjEzOTA0MzUyMTA1NTA5OWQ0MWUzNTA4NjM5OTJhOGViOTBhNjkxYWVhMWRiZDRkOTE0YmU
