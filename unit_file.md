# CDK Erigon Service

This repository contains a systemd service file for managing the CDK Erigon application. The service is configured to run the CDK Erigon executable with a specified configuration file, ensuring it restarts automatically on failure.

## Service File Overview

The service file is designed to be used with systemd, which is the default init system for many Linux distributions. Below is a brief overview of the key components of the service file.

### Service Configuration

- **Description**: A brief description of the service.
- **After**: This specifies that the service should start after the network is online.
- **Wants**: Ensures the network is online before starting the service.

### ExecStart

The command to start the CDK Erigon service, specifying the path to the executable and the configuration file:

```bash
ExecStart=/home/ubuntu/cdk-erigon/build/bin/cdk-erigon --config="/home/ubuntu/cdk-erigon/hermezconfig-cardona.yaml"
