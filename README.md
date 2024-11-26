# Kamabian

`Kamabian` is a repository designed to configure a Debian (or Ubuntu) server with secure and sane defaults. It is designed to work alongside the open source tool [Kamal](https://kamal-deploy.org), for deploying containerized applications on your own server or VM.

This repository handles the following.

- Passwordless SSH
- Apt packages of your choosing
- Firewall (UFW) configuration (both UDP and TCP ports), with sane defaults and override possibility
- Logrotate
- Docker

It creates a user named `kamal` for deploying your applications on your server.

## Setup

You must have the following things in place for this repository to work

1. A server with an IP address
2. Root access to the server via SSH (easily attained with most cloud providers)
3. Docker on your host system

## Usage

```bash
$ docker pull kamabian/kamabian:latest
$ docker run -v <path_to_your_priv_ssh_key>:/root/.ssh/privkey:ro -it kamabian/kamabian:latest /kamabian/scripts/bootstrap <your_server_ip>
```

That's it! Just replace the path to your SSH key, and let `Kamabian` handle the rest.

#### Where is my SSH Key?!

The point of this repo is to minimize the amount of DevOps you need to do, so if you don't know how to find the `<path_to_your_priv_ssh_key>` value, try this:

```
echo "$HOME/.ssh/$(ls ~/.ssh | grep -E '^id_(rsa|ed25519)$')"
```

### Using with Kamal

To use this with Kamal, the only setting needed is

```yaml
ssh:
  user: kamal
```

#### Overrides

To override settings, create a `./vars.yml` file based on `vars.yml.example`, and mount it with the docker flag `-v ./vars.yml:/kamabian`. This will allow you to set things like desired apt packages, firewall configs, and more.

## Warning !!!

This project is still in its early stages. If you plan to use this on your production systems, use scrutiny and caution. Your servers are **your** responsibility. Please submit issues and feature requests in this repository.

## Contributing

Open an issue before contributing and have a brief discussion with the author about whether or not your feature is in alignment with the author's wishes. If it does, then go ahead and open a PR.
