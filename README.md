# About

`debian-base` is an ansible repository designed to deploy a base debian VM image with secure and sane defaults. Often times, spinning up a new VM from scratch can be a laborious task with many considerations.

This repository handles the following.

- Passwordless SSH
- Apt packages of your choosing
- Firewall (UFW) configuration (both UDP and TCP ports), with sane defaults and override possibility
- Intrustion detection system (AIDE)
- Logrotate
- Docker (if desired)

### How it works

Ansible works by connecting to a remote system, and configuring it. An easy way to use this script is by installing ansible on your local machine, and pointing it at a cloud VM with a strong password. Other clever, automated solutions are possible, such as using github actions runners and/or terraform to trigger this script.

## Depedencies

You must have bash, python3 and ansible core installed on your system. This repo is tested with GNU bash version 5.2.32, Python 3.11.5 and Ansible core 2.17.4. This may work with older versions, but it is neither tested nor verified.

## Scripts

### init

Run this script after you create a VM with your public SSH key added to it for the root user.

1. Install ansible on the system that will bootstrap the VM
1. Create VM via the cloud provider of your choice, with a valid SSH key for the root user.
1. Run the following command `./scripts/init <ip_address> <path_to_ssh_priv_key>`

### configure

This script depends on the above `init` script being run successfully first. It will configure the VM, install desired `apt` packages, open desired firewall ports, etc.

1. Add a `./vars.yml` file to the root of this repository. Use the `./vars.yml.example` file for reference
2. Run `./scripts/configure`

## Warning !!!

This repo is still in its early stages. It SHOULD NOT be used on your production systems without verification, scrutiny, and caution. Your servers are **your** responsibility. Please submit issues and feature requests in this repository.

### Contributing

Open an issue before contributing, and have a brief discussion with the author about whether or not your feature is in alignment with the author's wishes. If it does, then go ahead and open a PR.

#### Future features

- Adding multiple servers to the init process
- Database administration options (postgres, mysql, sqlite)
- Email configuration for logwatch
- Docker compose setup
- User mgmt and access controls
- Package this as a role for ansible galaxy
- Setup to for easy plug-n-play with Rails deploy tool, Kamal
