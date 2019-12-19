# trex-ansible
Series of Ansible playbooks for installation and basic configuration of TRex.

# High Level Goals
At a high level, these script target a vanilla Linux system, for TRex traffic simulator software installation.

It will:
1. Create a `trex` user with sudo permissions via `wheel` group and password `trex`.
1. Install the latest stable TRex into `/opt/trex`

# Getting Started
1. Know a bit of Ansible: https://www.ansible.com/resources/get-started
1. Update the hosts file (or copy/clone a new one and supply it to Ansible via --inventory-file='')
   (see below for details)
1. Execute the playbook as per https://docs.ansible.com/ansible/latest/intro_getting_started.html
```
ansible-playbook trex-sw-install.yaml
```

## Assumptions
1. All target TRex-generator hosts have a supported vanilla Linux OS already installed.
1. A sudo-capable user exists to perform these operations.

## Host Inventory User-Actions
1. Update list of hosts to install TRex onto.
  * Comment out `localhost` if you don't want TRex on Ansible server.
  * Uncomment example host and/or use as template to add additional hosts to install TRex onto.
1. Handle the remote user username by:
  * Update the ansible_user='' as required by the remote generator system. OR
  * Supply it to Ansible via --user ansible-playbook command option.
1. Handle the remote user password by:
  * Update the ansible_become_pass='' as required by the remote system for each host. OR
  * Supply it to Ansible via --ask-become-pass ansible-playbook command option. OR
  * Remote system allows for NOPASSWORD sudo access.

## Password Vaults
* If security is relevant in your deployment/scenario, change to vaults:
  https://docs.ansible.com/ansible/latest/vault.html
  (The example provided in the hosts.yaml file is simplistic and assumes that you're running in an
  internal environment and authentication to the TRex server is inconsequential.)

## Changing the TRex software version
* Override the version of TRex by overriding the role variable:
```
ansible-playbook trex-sw-install.yaml --extra-vars "trex_version=v2.40.tar.gz"
```
    
# Playbook Descriptions
* trex-sw-install.yaml: Basic TRex install.

# Role Definitions
* base_linux_platform_deps: Deals with basic OS dependencies.
* trex_generator_software: Installs TRex software.
 
# Future Extensions
* New roles could be introduced for bare metal performant tuning or low_end configurations.
