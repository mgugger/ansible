# Ansible Archlinux Install

This ansible script install archlinux through ssh'ing into the live media. The goal is to create a working archlinux image on btrfs to use in azure.

# Creating Image and Uploading to Azure
## Create Hyper-V Machine
Download the archlinux install image, boot a hyper-v machine from the iso with an attached harddisk and get the ip from the virtual machine.

## Access from WSL to a machine running in hyper-v
In case that ssh access does not work from wsl to the hyper-v machine:
````
Get-NetIPInterface | where {$_.InterfaceAlias -eq 'vEthernet (WSL)' -or $_.InterfaceAlias -eq 'vEthernet (Default Switch)'} | Set-NetIPInterface -Forwarding Enabled
```

## Provision VM
```
ansible-playbook install-playbook.yml -i root@{IP},
```

## Convert VHDX Image to VHD
From powershell with administrator rights, run:
```
Convert-VHD -Path 'C:\Users\Public\Documents\Hyper-V\Virtual hard disks\Archlinux.vhdx' -DestinationPath 'C:\Users\Public\Documents\Hyper-V\Virtual hard disks\ArchlinuxVHD.vhd'
```