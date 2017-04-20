# Linux virtual machine for training on Microsoft Azure 

This virtual machines is preconfigured for Linux training purposes.

## Virtual Machine content

 Type | Description 
------------ | -------------
 1 x ??? GB Harddrive | OS Disk
 3 x 128 GB Harddrives | Raid devices or use with LVM 
 1 x 14 GB Harddrive | Swap device |
 /opt/azure-linux-training-master | This repository with training files 


## SSH Key Generation

1. Windows - https://www.digitalocean.com/community/tutorials/how-to-create-ssh-keys-with-putty-to-connect-to-a-vps
2. Linux - https://help.ubuntu.com/community/SSH/OpenSSH/Keys#Generating_RSA_Keys
3. Mac - https://help.github.com/articles/generating-ssh-keys/#platform-mac

## Create the virtual machine
### Create the  virtual machine on the Azure Portal

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fderdanu%2Fazure-linux-training%2Fmaster%2Fazuredeploy.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>
<a href="http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2Fderdanu%2Fazure-linux-training%2Fmaster%2Fazuredeploy.json" target="_blank">
    <img src="http://armviz.io/visualizebutton.png"/>
</a>

### Create the virtual machine with powershell

```powershell
New-AzureRmResourceGroupDeployment -Name <DeploymentName> -ResourceGroupName <RessourceGroupName> -TemplateUri https://raw.githubusercontent.com/derdanu/azure-linux-training/master/azuredeploy.json
```

### Create the virtual machine with azure cli
```
azure group deployment create <RessourceGroupName> <DeploymentName> --template-uri https://raw.githubusercontent.com/derdanu/azure-linux-training/master/azuredeploy.json
```

## Docker Image 

### Run the Ubuntu container

```
docker run -it dfalkner/azure-linux-training:ubuntu /bin/bash
```

### Run the Centos container

```
docker run -it dfalkner/azure-linux-training:centos /bin/bash
```

# Scenario validation
This image comes with a utility to train certain scenarios which are common for Linux related certification such as Linux Foundation Certified Systemadministrator (LFCS). The container version of this image has limited support for this validation as the required infrastrcuture is not available. To make full use of the validation use the virtual machine.

## Scenarios
ID | Description 
------------ | -------------
SA-BR-001 | Create a backup '/opt/alt/exams.tar.gz' with the recursive content of '/opt/alt/exams'
SA-FP-001 | Create a directory '/opt/alt/exams' which is readable/writeable by its owner and by users of the group 'learners'
SA-FP-002 | Create the file '/opt/alt/README' and set the immutable flag
SA-UM-001 | Create a group with the name 'learners'
SA-UM-002 | Add a user with the name 'student1'
SA-UM-003 | Add user 'student1' to the group 'learners' while leaving the primary group unchanged
LS-RA-001 | Add a new sudo rule to allow user 'student1' to run '/sbin/ifconfig' without providing a password
SA-BR-001 | Create a backup '/opt/alt/exams.tar.gz' with the recursive content of '/opt/alt/exams'
FS-LM-001 | Create a new LVM volume group 'vg0' with the physical volumes '/dev/sdc' and '/dev/sdd'
FS-LM-002 | Create a 1GB logical volume 'exams' in volume group 'vg0‘
FS-LM-003 | Create two 1GB logical volumes 'raid1' and 'raid2'  in volume group 'vg0'
FS-FS-002 | Create a swap partition off '/dev/md0'
SA-FP-002 | Create the file '/opt/alt/README' and set the immutable flag