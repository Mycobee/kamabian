# About

`debian-base` is an ansible repository designed to deploy a base debian VM image with secure and sane defaults. Often times, spinning up a new VM from scratch can be a laborious task with many considerations.

This repository handles the following.

- Passwordless SSH
- apt packages
- Firewall (UFW) configuration (both UDP and TCP ports)
- Intrustion detection system (AIDE)


### How it works

Ansible works by connecting to a remote system, and configuring it. An easy way to use this script is by installing ansible on your local machine, and pointing it at a cloud VM with a strong password. Other clever, automated solutions are possible, such as using github actions runners and/or terraform to trigger this script.

## Usage

1. Install ansible on the system that will bootstrap the VM
1. Create VM via the cloud provider of your choice, with a valid SSH key for the root user.
1. Create a file `./.environment.yml` with your desired environment variables. This file is gitignored, and should NOT be committed to source code.
1. Run the following command `./scripts/bootstrap <ip_address> <password>`
