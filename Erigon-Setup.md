# Installation and Setup Guide

[Official CDK Github Repository](https://github.com/0xPolygonHermez/cdk-erigon)
[Official CDK Documentation](https://docs.polygon.technology/cdk/getting-started/cdk-erigon/deploy-cdk-erigon/)

This guide provides step-by-step instructions to set up your development environment with the necessary tools and start an Erigon node using Docker.

## Table of Contents

1. [Install Required Tools](#install-required-tools)
   - [Install C Compiler](#install-c-compiler)
   - [Install Wget](#install-wget)
   - [Install Go](#install-go)
   - [Install Docker and Docker Compose](#install-docker-and-docker-compose)
2. [Start Erigon Node using Binary](#clone-the-repo)
3. [Start Erigon Node using Docker](#start-erigon-node-using-docker)
4. [Access Your Container](#access-your-container)
5. [Stop The Docker Container](#stop-the-docker-container)
6. [Start Erigon Node Using Docker Compose](#start-erigon-node-using-docker-compose)
7. [View Logs of Docker Compose Service - Erigon](#view-logs-of-docker-compose-service---erigon)
8. [Stop Docker Compose Service](#stop-docker-compose-service)


## Install Required Tools

### Install C Compiler
1. **Update packages:**
   ```bash
   sudo apt update
   ```
2. **Install build-essential:**
   ```bash
   sudo apt install build-essential
   ```
3. **Verify the Installation:**
   ```bash
   gcc --version
   ```

### Install Wget
1. **Update packages:**
   ```bash
   sudo apt update
   ```
2. **Install Wget:**
   ```bash
   sudo apt install wget -y
   ```

### Install Go

#### Install Go version 1.19
1. **Download:**
   ```bash
   wget https://go.dev/dl/go1.19.linux-amd64.tar.gz
   ```
2. **Remove Previous installation:**
   ```bash
   sudo rm -rf /usr/local/go
   ```
3. **Extract the archive:**
   ```bash
   sudo tar -C /usr/local -xzf go1.19.linux-amd64.tar.gz
   ```
4. **Setup the Go Path:**
   ```bash
   echo "export PATH=\$PATH:/usr/local/go/bin" >> ~/.bashrc 
   source ~/.bashrc
   ```
5. **Check version:**
   ```bash
   go version
   ```


## Start Erigon Node using Binary
1. **Clone The Repository:**
   ```bash
   git clone https://github.com/0xPolygonHermez/cdk-erigon
   ```
2. **CD into the cloned Repository:**
   ```bash
   cd cdk-erigon/
   ```
3. **Checkout to the latest or recommended tag:**
   ```bash
   git checkout tags/<latest version>
   ```
4. **Install the relevant libraries for your architecture by running:**
   ```bash
   make build-libs
   ```
5. **Check version:**
   ```bash
   go version
   ```
6. **Build the node with the following command:**
   ```bash
   make cdk-erigon
   ```
6. **Setup the relevant Config file and execute the below command {network is either cardona or mainnet} use the example file as guide:**
   ```bash
   ./build/bin/cdk-erigon --config="./hermezconfig-{network}.yaml"
   ```

#### Install Go version 1.21
1. **Download:**
   ```bash
   wget https://go.dev/dl/go1.21.0.linux-amd64.tar.gz
   ```
2. **Remove Previous installation:**
   ```bash
   sudo rm -rf /usr/local/go
   ```
3. **Extract the archive:**
   ```bash
   sudo tar -C /usr/local -xzf go1.21.0.linux-amd64.tar.gz
   ```
4. **Setup the Go Path:**
   ```bash
   echo "export PATH=\$PATH:/usr/local/go/bin" >> ~/.bashrc 
   source ~/.bashrc
   ```
5. **Check version:**
   ```bash
   go version
   ```

### Erigon Node with Docker & Docker Compose:
#### Install Docker 
1. **Update your package:**
   ```bash
   sudo apt update
   ```
2. **Install prerequisite packages:**
   ```bash
   sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
   ```
3. **Add Docker’s official GPG key:**
   ```bash
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
   ```
4. **Add the Docker repository:**
   ```bash
   echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   ```
5. **Update your package index again and install Docker:**
   ```bash
   sudo apt update
   sudo apt install docker-ce -y
   ```
6. **Verify that Docker is installed:**
   ```bash
   sudo docker --version
   ```
7. **(Optional) Run Docker without sudo:**
   ```bash
   sudo usermod -aG docker $USER
   newgrp docker
   ```
#### Install Docker Compose
1. **Download the Docker Compose binary:**
   ```bash
   sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   ```
2. **Make the Docker Compose binary executable:**
   ```bash
   sudo chmod +x /usr/local/bin/docker-compose
   ```
3. **Verify the installation:**
   ```bash
   docker-compose --version
   ```

## Start Erigon Node using Docker
To start the Erigon node, run the following command:
#### For testnet
```bash
sudo docker run -d -p 8545:8545 -v ./cdk-erigon-data/:/data/erigon/testnet hermeznetwork/cdk-erigon --config="./cardona.yaml" --zkevm.l1-rpc-url=https://rpc.sepolia.org
```
#### For mainnet
```bash
sudo docker run -d -p 8545:8545 -v ./cdk-erigon-data/:/data/erigon/mainnet hermeznetwork/cdk-erigon  --config="./mainnet.yaml" --zkevm.l1-rpc-url=https://rpc.eth.gateway.fm
```

## Access Your Container
To access your running Docker container, use:
```bash
sudo docker exec -it <container-id> /bin/sh
```

## Stop The Docker Container
To stop the running Docker container, use:
```bash
sudo docker kill <container-id>
```

## Start Erigon Node Using Docker Compose File
Set the environment variables and edit/rename/copy docker-compose-example.yml to docker-compose-{network}.yml accordingly:
#### For testnet
```bash
NETWORK=cardona 
L1_RPC_URL=https://rpc.sepolia.org
sudo docker-compose -f docker-compose-cardona.yml up -d
```
#### For mainnet
```bash
NETWORK=mainnet 
L1_RPC_URL=https://rpc.eth.gateway.fm
sudo docker-compose -f docker-compose-mainnet.yml up -d
```

## View Logs of Docker Compose Service - Erigon
To view the logs of the Erigon service, use:
```bash
sudo docker-compose logs erigon
```

## Stop Docker Compose Service
To stop the Docker Compose service, run:
```bash
sudo docker-compose down
```

