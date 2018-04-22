# A VirtualBox image for Mastodon development

This VirtualBox base image contains all the required packages and configuration for running/instantiating a Mastodon instance for development. It is build using [Hashicorp's Packer](https://packer.io), the provisioning is done with Ansible through a dedicated git submodule called [mastodon-ansible](https://github.com/moritzheiber/mastodon-ansible). The tests are using [ServerSpec](https://serverspec.org). It's made available through [Hashicorp's Vagrant Cloud](https://app.vagrantup.com) at [`mastodon/ubuntu-xenial64`](https://app.vagrantup.com/mastodon/boxes/ubuntu-xenial64).

_Note: Some of the content of the scripts in `scripts/` is borrowed from the [Bento](https://github.com/chef/bento) project._

## Prerequisites (for building on your own)

- VirtualBox >= 5.1.x
- Packer >= 1.0.0
- Python >= 2.x
- pip/python-pip >= 8.x

for testing purposes:

- Vagrant >= 2.0.3

## Setup

```sh
$ virtualenv env
$ source env/bin/activate
$ pip install -r requirements.txt
```

## Building the box locally

Just execute:

```sh
$ packer build packer.json
```

_Note: It will take at least roughly 5 - 10 minutes for the ISO to get preseeded ("pre-provisioned") by the Debian installer, hence the rather long timeout/waiting period before packer actually starts provisioning. If you're unsure whether there is any progress change the values `headless` in the `packer.json` from `true` to `false` and re-run the process. This will give have VirtualBox show you the output of the console the ISO is running on._

This will preseed the Ubuntu ISO image for Ubuntu Xenial 64bit with a couple of sane defaults and packages. Afterwards, the Ansible provisioner is run using the playbooks from the [mastodon-ansible](https://github.com/moritzheiber/mastodon-ansible) repository.

In the end you should have a box in `builds/` with all the required components installed you can run directly in Vagrant.

## Publishing to Vagrant Cloud

_Note: You need a valid access token to submit new versions of the box to Vagrant Cloud. It will not work otherwise. There is a organization called `mastodon` which is responsible for the Vagrant boxes under the same namespace. If you think you can/want to contribute send me a message on @moritzheiber@mastodon.social and I'll add your to the organization._

If you have a valid `VAGRANT_CLOUD_TOKEN` you can use the `vagrant-cloud` post-processor to upload a new version to Vagrant Cloud. It'll be done automatically if the token is set:

```
$ VAGRANT_CLOUD_TOKEN="my-token" packer build packer.json
```

## Testing

TODO
