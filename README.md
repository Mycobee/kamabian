# About

`debian-base` is an ansible repository designed to deploy a base debian VM image with secure and sane defaults. Often times, spinning up a new VM from scratch can be a laborious task with many considerations.

This repository handles the following.

- Passwordless SSH
- apt packages
- Firewall (UFW) configuration (both UDP and TCP ports)
- Intrustion detection system (AIDE)

### How it works

Ansible works by connecting to a remote system, and configuring it. An easy way to use this script is by installing ansible on your local machine, and pointing it at a cloud VM with a strong password. Other clever, automated solutions are possible, such as using github actions runners and/or terraform to trigger this script.


### Scripts

`./scripts/init` - Run this script after you create a VM with your public SSH key added to it for the root user.
`./scripts/bootstrap` - Run this script after you have initialized a new VM. The plan is for this script to be idempotent and able to be run on existing VMs if needed

## Usage

1. Install ansible on the system that will bootstrap the VM
1. Create VM via the cloud provider of your choice, with a valid SSH key for the root user.
1. Create a file `./.environment.yml` with your desired environment variables. This file is gitignored, and should NOT be committed to source code.
1. Run the following command `./scripts/bootstrap <ip_address> <password>`

## Warning

This repo is still in its early stages. It SHOULD NOT be used on your production systems without verification, scrutiny, and caution. Your servers are your responsibility. Please submit issues and feature requests in this repository.
