# A VirtualBox box for Mastodon

This VirtualBox base box contains all the required packages and configuration for running/instantiating a Mastodon instance. It is build using [Hashicorp's Packer](https://packer.io), the provisioning is done with Ansible through a dedicated git submodule called [mastodon-ansible](https://github.com/moritzheiber/mastodon-ansible). The tests are using [ServerSpec](https://serverspec.org).

## Prerequisites

- VirtualBox >= 5.1.x
- Packer >= 1.0.0
- Python >= 2.x
- pip/python-pip >= 8.x

for testing purposes:

- Vagrant >= 1.9.3

## Setup

```sh
$ virtualenv env
$ source env/bin/activate
$ pip install -r requirements.txt
```

## Building the box

TODO

## Testing

TODO
