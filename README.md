# b9lab-final-exam-vm
The best way to work with, build and test etherum code & DApps is through a controlled linux vm
Here is one provided by the good folks over at https://b9lab.com/ during the certified ethereum dev course I took.
I found that you encounter less npm issues using a vm and all the good stuff like ganache-cli, npm, git & truffle are ready for you to use.

## Requirements
Install Virtual Box & Vagrant via Chocolately if on windows

https://www.virtualbox.org/

https://www.vagrantup.com/downloads.html

https://chocolatey.org/packages?q=vagrant

## clone the repository
`git clone https://github.com/theTechRebel/b9lab-final-exam-vm.git`

## cd into the repository
`cd b9lab-final-exam-vm`

## play with the vm
`vagrant up` - to bring up the virtual machine

`vagrant ssh` - to login to the vm

`exit` - to exit the virtual machine

`vagrant halt` - to shutdown the virtual machine
