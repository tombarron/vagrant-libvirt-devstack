# vagrant-libvirt-devstack
Devstack in vagrant VM using vagrant-libvirt plugin

## Summary
Installs a CentOS 7 VM on your local machine with devstack and a local.conf for
manila with the CephFS with NFS back end.

The devstack VM mounts /opt/stack from the host so that (1) you can use an editor or IDE from the host machine to modify and stage code to the devstack machine, and (2) your changes are persisted between devstack VM deployments.

## Pre-requisites
You need various packages and to set up NFS service for /opt/stack on your host machine.  For Fedora 28 just run:

``` shell
sudo dnf install ansible
ansible-playbook prepare-host.yml
```
For other distros you can modify the install commands in prepare-host.yml or just run the corresponding commands manually.

## Install and provision the devstack VM
Run:
``` shell
vagrant up
```
Before running this command you may want to inspect Vagrantfile and adjust the resources deployed to the VM.
## Login to the devstack VM and set up devstack
Run:

``` shell
vagrant ssh
cd devstack
./stack.sh
```
Before you actually run stack.sh inspect and edit local.conf to your liking.

## Post-devstack
Before you can access horizon on the devstack VM you need to modify iptables there.  On the host machine, run:
``` shell
ansible-playbook post-devstack.yml
```
