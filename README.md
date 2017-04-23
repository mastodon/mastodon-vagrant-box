# A VirtualBox image for Mastodon development

This VirtualBox base image contains all the required packages and configuration for running/instantiating a Mastodon instance for development. It is build using [Hashicorp's Packer](https://packer.io), the provisioning is done with Ansible through a dedicated git submodule called [mastodon-ansible](https://github.com/moritzheiber/mastodon-ansible). The tests are using [ServerSpec](https://serverspec.org). The image is build continuously using [Hashicorp Atlas](https://atlas.hashicorp.com).

_Note: Some of the content of the scripts in `scripts/` is borrowed from the [Bento](https://github.com/chef/bento) project._

## Prerequisites (for building on your own)

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

Just execute:

```sh
$ packer build packer.json
```

_Note: It will take at least roughly 5 - 10 minutes for the ISO to get preseeded ("pre-provisioned") by the Debian installer, hence the rather long timeout/waiting period before packer actually starts provisioning. If you're unsure whether there is any progress change the values `headless` in the `packer.json` from `true` to `false` and re-run the process. This will give have VirtualBox show you the output of the console the ISO is running on._

This will preseed the Ubuntu ISO image for Ubuntu Xenial 64bit with a couple of sane defaults and packages. Afterwards, the Ansible provisioner is run using the playbooks from the [mastodon-ansible](https://github.com/moritzheiber/mastodon-ansible) repository.

In the end you should have a box in `builds/` with all the required components installed you can run directly in Vagrant.

## Submitting to Atlas

tbd

## Testing

TODO
