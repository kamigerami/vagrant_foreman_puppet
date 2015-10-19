## Vagrant -> Installs foreman, puppet with ansible provisioner
Easy setup of Foreman and Puppetmaster as well as two agent hosts.


## Prerequisites
- [Vagrant] (https://www.vagrantup.com/downloads.html), Creates and configures lightweight, reproducable, and portable development environments.
- vagrant-hostmanager plugin, automatically ensure all DNS entries are consistent between guests as well as the host, in the '/etc/hosts' file.
- vagrant-vbguest plugin, keeps the vbguest tools updated.

```
vagrant plugin install vagrant-hostmanager
vagrant plugin install vagrant-vbguest
```

- Requires Ansible 1.7 or newer
- Expects CentOS 7.x host/s

RHEL7 version reflects changes in Red Hat Enterprise Linux and CentOS 7:
1. Network device naming scheme has changed
2. iptables is replaced with firewalld
3. MySQL is replaced with MariaDB


### Install

Clone the repository into the directory of your choosing. Run Vagrant up and wait for the provisioning to complete.

```
git clone https://github.com/kamigerami/vagrant_foreman_puppet.git
cd vagrant_foreman_puppet
vagrant up theforeman.example.com
```

Vagrant uses ansible as a provisioning tool. Provision the Foreman host `theforeman.example.com` first and then if you require more hosts, the agents `agent01.example.com, agent02.example.com`.

When the provisioning of theforeman.example.com is complete, note the output from Vagrant. The output provides the `admin` login password and URL for the foreman web interface.
Example output below.

```text
==> theforeman.example.com:   Success!
==> theforeman.example.com:   * Foreman is running at https://theforeman.example.com
==> theforeman.example.com:       Initial credentials are admin / changeme
==> theforeman.example.com:   * Foreman Proxy is running at https://theforeman.example.com:8443
==> theforeman.example.com:   * Puppetmaster is running at port 8140
==> theforeman.example.com:   The full log is at /var/log/foreman-installer/foreman-installer.log
```


## JSON Configuration File
The `Vagrantfile` retrieves multiple VM configurations from a separate `nodes.json` JSON file. All VM configuration is
contained in that JSON file. You can add additional VMs to the JSON file, following the existing pattern. The
`Vagrantfile` will loop through all nodes (VMs) in the `nodes.json` file and create the VMs. You can easily swap
configuration files for alternate environments since the `Vagrantfile` is designed to be generic and portable.

## Errors
**Error: Unknown configuration section 'hostmanager'.**
=> **Solution: **Install the `vagrant-hostmanager` plugin with `vagrant plugin install vagrant-hostmanager`

#### This project was modified to suit my needs - the original author (Gary A. Stafford) project using vagrant and shell scripts can be found at [github] (https://github.com/garystafford/foreman-vagrant) 
