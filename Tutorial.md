# Vagrant Basics
## Create a Vagrant File
```commandline
vagrant init bento/ubuntu-16.04
```

## To run the vagrant bot
```commandline
vagrant up
```

## To check status
```commandline
vagrant status
```

## To check status on all machines
```commandline
vagrant global-status
```

## Remove a VM
```commandline
vagrant destroy 1a2b3c4d
```

## Stop a VM
```commandline
vagrant halt 1a2b3c4d
```

## SSH to VM
* this command should be run from the vm folder
```commandline
vagrant ssh
```

## Reload VM
* this command should be run from the vm folder
```commandline
vargrant reload
```

## To sync a folder on the PC to a folder in VM
* use line 46 in Vagrantfile
* uncomment line
* create folder in PC and reload the VM if running


## Port Forwarding/Exposing VM ports using Vagrant
* use line 26 or 31 to do this
* uncomment (26 or 31)
* reload the VM if not running

## To create a private Network
* use line 35 for a specific address
* or use line 36 for a dynamic address with dhcp

## To change the cpu or memory allocation of VM
* use line 57 in vagrant file to change memory
* to change cpu add the following
```
vb.cpus = 2
```

## To run gui
* uncomment line 54

## Install application to a vm on creation
* use line 66 to create in inline bash script execution
* to use a bash script created in your windows use the following
    * first create the bash and copy the path e.g emeka/script.sh
 ```bash
apt update && apt upgrade -y
apt install nginx -y
```
* now you can include the following on your vagrantfile
```markdown
 config.vm.provision "shell", path: "emeka/script.sh"
```
* script only runs once. to make it run for each boot use the following
```markdown
 config.vm.provision "shell", path: "emeka/script.sh", run: "always"
```

## Run two Vms using vagrant
* on line 15 add the following:
```markdown
config.vm.define "mongo" do |mongo|
    mongo.vm.box = "bento/ubuntu-16.04"
    mongo.vm.provider "virtualbox" do |vb|
        vb.memory = "512"
    end
    mongo.vm.network "private_network", ip: "192.168.20.11"
end

```

## To copy file
```markdown
config.vm.provision "file", source: "files/text.txt", destination: "~/text.txt"
```

## To view your current boxes
```commandline
vagrant box list
```

## To create a new box/VM
This command is executed on the PC terminal
```bash
vagrant package --vagrantfile Vagrantfile --output myfirstbox.box
vagrant box add myfirstbox.box

```

## To run the new created box
* create a new directory and cd to it
```commandline
vagrant init myfirstbox
vagrant up
```

## Take a snapshot of the box
```commandline
vagrant snapshot save pre_provision
```

## To view all snapshots
```commandline
vagrant snapshot list
```

## To restore to snapshot
```commandline
vagrant snapshot restore pre_position --no-provision
```