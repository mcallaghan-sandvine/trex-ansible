# trex-ansible
Series of ansible playbooks for installation and basic configuration of TRex

# High Level Goals

At a high level, these script target a vanilla Linux system, for TRex traffic simulator software installation.

It will:
1. Create a `trex` user with sudo permissions via `wheel` group and password `trex`.
1. Install the latest stable TRex into `/opt/trex`


# Getting Started
1. Know a bit of ansible: https://www.ansible.com/resources/get-started
1. Update the hosts file (or copy/clone a new one and supply it to ansible via --inventory-file='')
   (see below for details)
1. Execute the playbook as per https://docs.ansible.com/ansible/latest/intro_getting_started.html
```
ansible-playbook trex-sw-install.yaml
```

## Assumptions
* all target TRex-generator hosts have a supported vanilla Linux OS already installed
* a sudo-capable user exists to perform these operations

## Host Inventory User-Actions
1. Update list of hosts to install TRex onto.
  * (IP or HOSTNAME)
1. Handle the remote user username by:
  * update the ansible_user='' as required by the remote generator system, OR
  * supply it to ansible via --user
1. Handle the remote user password by:
  * update the ansible_become_pass=''as required by the remote generator system per host, OR
  * supply it to ansible via --ask-become-pass, OR
  * remote system allows for NOPASSWORD sudo access
    
## Password Vaults
* if security is relevant in your deployemnt/scenario, change to vaults:
  https://docs.ansible.com/ansible/latest/vault.html
  (the assumption of these simplisitc ansible is that you're running in an
  internal environment and authentication to the TRex server is inconsequential)
    
## Changing the TRex software version
* override the version of TRex by overriding the role variable:
```
ansible-playbook trex-sw-install.yaml --extra-vars "trex_version=v2.40.tar.gz"
```
    
# Playbook Descriptions
* trex-sw-install.yaml: the only playbook today, does the basic install

# Role Definitions
* base_linux_platform_deps: deals with basic OS dependencies
* trex_generator_software: installs TRex software
 
# Future Extensions
* new roles could be introduced for baremetal performant tuning or low_end configurations
