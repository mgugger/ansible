# Ansible

## Requirements
* Azure CLI for the ansible azure inventory to work and the required ansible packages

## Create Archlinux VHD Image
```
packer build -var "username=$(whoami)" -var "user_ssh_public_key=$(cat ~/.ssh/id_rsa.pub)" archlinux-packer.json
```


# Local Testing in Hyper-V
An easy way to test these playbooks is by running vms in hyper-v and run these playbooks from wsl.

## Create Hyper-V Machine
### Archlinux
Download the archlinux install image, boot a hyper-v machine from the iso with an attached harddisk and get the ip from the virtual machine.

### Ubuntu
Install by creating a new vm and selecting the ubuntu template in the hyper-v manager.

## Access from WSL to a machine running in hyper-v
In case that ssh access does not work from wsl to the hyper-v machine:
````
Get-NetIPInterface | where {$_.InterfaceAlias -eq 'vEthernet (WSL)' -or $_.InterfaceAlias -eq 'vEthernet (Default Switch)'} | Set-NetIPInterface -Forwarding Enabled
```

## Provision VM
```
ansible-playbook install-playbook.yml -i root@{IP},
```